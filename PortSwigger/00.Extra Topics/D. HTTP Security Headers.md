## 1)`Access-Control-Allow-Origin` — possible values

This header tells the browser **which Origin(s)** are allowed to read the response.

Common values:

1. **Single explicit origin**
    - Example: `https://example.com`
2. **Wildcard**
    - `*` (allows any origin **only** in certain cases; see credentials note below)
3. **(Less common / not standard for typical simple CORS)**
    - Some servers dynamically reflect the request `Origin` (e.g., respond with the same value as the incoming `Origin`).
    - This can be safe or unsafe depending on whether they properly validate it (relevant for security; don’t use “just reflect” blindly).

### Credentials interaction rule (very important)

- If you set `Access-Control-Allow-Credentials: true`, then you **cannot** use `Access-Control-Allow-Origin: *`.
- In that case the server must return the **actual origin** (not `*`).

**Keywords:** “origin allowlist”, “wildcard”, “credentials conflict with `*`”.

## 2) `Access-Control-Allow-Credentials`

Indicates whether the browser should expose the response to JS when **cookies / HTTP auth / client credentials** are involved.

Possible values:

- `true`
- `false` (often omitted instead of sending `false`)

Notes:

- If the browser request includes credentials (e.g. `fetch(..., { credentials: "include" })`), then the browser will require server approval via this header.
- Must be consistent with `Access-Control-Allow-Origin` (see rule above).

**Keywords:** “cookies included”, “credentialed request”.

---

## 3) Other important CORS-related headers (the “core set”)

### A) `Access-Control-Expose-Headers`

Tells the browser which response headers JS is allowed to read (beyond the safe default set).

- Example: `Access-Control-Expose-Headers: X-My-Header, X-Other`

If omitted, JS can only read a limited set of headers.

---

### B) `Access-Control-Allow-Methods`

Used mainly in **preflight** responses to tell the browser which HTTP methods are allowed.

- Example: `Access-Control-Allow-Methods: GET, POST, PUT`

---

### C) `Access-Control-Allow-Headers`

Used mainly in **preflight** responses to tell the browser which request headers are allowed.

- Example: `Access-Control-Allow-Headers: Content-Type, Authorization, X-Requested-With`

---

### D) `Access-Control-Max-Age`

How long (in seconds) the preflight result can be cached by the browser.

- Example: `Access-Control-Max-Age: 600`

---

### E) `Vary: Origin`

Not a CORS `Access-Control-*` header, but **crucial for security/caching correctness**.

When servers dynamically vary CORS by Origin, they should include:

- `Vary: Origin`

Without it, shared caches (CDNs/proxies) can mistakenly serve a response with one Origin’s CORS allowance to another Origin (can become a vulnerability depending on setup).

---

## 4) Related headers you’ll see in requests/responses

### Request header: `Origin`

- Browser sends `Origin: https://siteA.com`
- Server uses it to decide what to return in `Access-Control-Allow-Origin`.

### Request header: `Access-Control-Request-Method` (preflight)

- Example: `Access-Control-Request-Method: POST`

### Request header: `Access-Control-Request-Headers` (preflight)

- Example: `Access-Control-Request-Headers: Authorization, X-Custom`