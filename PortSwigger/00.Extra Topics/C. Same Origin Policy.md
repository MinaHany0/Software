
# Explanation 1
video used : [The Same Origin Policy - Hacker History](https://www.youtube.com/watch?v=bSJm8-zJTzQ&ab_channel=LiveOverflow)

continuing this playlist [The History of XSS - YouTube](https://www.youtube.com/playlist?list=PLhixgUqwRTjyakFK7puB3fHVfXMinqMSi)

long before we used to have website written in http with multiple links of other websites which made navigation easier
![[Same Origin Policy-20241202160112739.webp]]

then came the forms in HTML which was used for banks and other stuff![[Same Origin Policy-20241202160849462.webp]]

then came the cookies to authenticate that the user who is dealing with the website is legit, here's how cookies were described to be used by the documentation![[Same Origin Policy-20241202160949906.webp]]

then came LiveScript (later JavaScript) ![[Same Origin Policy-20241202161111347.webp]] <span style="color:rgb(255, 192, 0)">which allowed scripting inside the HTML documents</span> using the `<script> tag` 

<span style="color:rgb(0, 176, 80)">This changed everythings</span>, the web had now event handlers, you could define objects which react with time, and more and more.
so now the web became <span style="color:rgb(0, 176, 80)">dynamic</span>

the websites before used lots of frames (predecessor of today's iframes)

![[Same Origin Policy-20241202161429250.webp]] here we have <span style="color:rgb(0, 176, 80)">two frames</span> in a HTML document with <span style="color:rgb(0, 176, 80)">different URLs</span>
this is how you can implement a navigation bar in content of a page

![[Same Origin Policy-20241202161545716.webp]] frames were really visible and implemented in the browser itself

and as in the JavaScript Documentation, you could now interact with frames![[Same Origin Policy-20241202161636054.webp]]

<span style="color:rgb(0, 176, 80)">so here is the ISSUE</span>
we have a webpage with two different frames, one is the form for some bank and the other is the attacker website
![[Same Origin Policy-20241202161805680.webp]]
 ![[Same Origin Policy-20241202161836200.webp]]and since the two frames can interact using JavaScript, the attacker URL could steal the credentials from the other frame easily using the following code
![[Same Origin Policy-20241202161945982.webp]]

so if you go to a <span style="color:rgb(0, 176, 80)">malicious</span> website, it could load your banking website in <span style="color:rgb(0, 176, 80)">one frame</span> and then use your <span style="color:rgb(0, 176, 80)">browser stored data</span> to login and then using <span style="color:rgb(0, 176, 80)">frames and JavaScript </span>could steal your <span style="color:rgb(0, 176, 80)">credentials</span> and send them to the attacker.

NOW NETSCAPE DEVELOPERS REALISED THIS ISSUE AND RELEASED A NEW VERSION WITH THE FIX

![[Same Origin Policy-20241202162437411.webp]]![[Same Origin Policy-20241202162453967.webp]] now we cannot access the forms data as an array as before or even get the cookie value

this is the fix documentation ![[Same Origin Policy-20241202162643266.webp]]

they prevented also the access of script to listing of local file on the PC![[Same Origin Policy-20241202162852485.webp]]
well we could still access the files but scripts themselves cannot (this not I don't really understand since all code is scripts but ok)


so later this became even more clear when they prevented scripts on one server from accessing properties of documents on another server
![[Same Origin Policy-20241202162837097.webp]] so they invented <span style="color:rgb(0, 176, 80)">Same Origin Policy</span> (SOP)

this was serious issue yes but <span style="color:rgb(0, 176, 80)">there was much more serious vulnerabilities needed to be taken care of </span> 

## Universal XSS
so came before what is now known as "universal XSS", as <span style="color:rgb(0, 176, 80)">we should know</span> XSS is known for <span style="color:rgb(0, 176, 80)">stored XSS</span> and <span style="color:rgb(0, 176, 80)">reflected XSS</span> 

keeping the story short, the same happened to Microsoft explorer with their version of dynamic java called Jscript![[Same Origin Policy-20241202205747386.webp]]

then came some guy named Georgi and reported many many vulnerabilities in IE![[Same Origin Policy-20241202210322012.webp]]
Georgi found another update with IE , with the opening of files inside each other using JavaScript![[Same Origin Policy-20241202211028205.webp]]apparently when opening a file inside another file, the browser keeps the contents of the old file until the second file finishes loading <span style="color:rgb(0, 176, 80)">(-ish :) )  </span> "anyway this is part of the history"

## <span style="color:rgb(0, 176, 80)">Conclusion</span> 
what Georgi and many more security researchers had in common is this , they exploited ways for malicious websites to take use of naive browsers to access more important websites and extract information for the attacker.![[Same Origin Policy-20241202211634540.webp]]
they were able to bypass the 
- cross-frame policy
- cross-frame vulnerability
and that's why it is called <span style="color:rgb(0, 176, 80)">UNIVERSAL</span> because it had nothing to do with the website itself, it was universal across all websites due to the <span style="color:rgb(0, 176, 80)">shortcomings of the browser</span> 



so before XSS (cross site scripting) became known as a thing, this issue was name cross frame vulnerability 
<span style="color:rgb(0, 176, 80)">because</span> what was happening is that a website could embed another website using <span style="color:rgb(0, 176, 80)">iframes</span> or open a new window with another website through JavaScript and by some way could get data from it to the attacker's side![[Same Origin Policy-20241202212721899.webp]]
so the victim's data was <span style="color:rgb(0, 176, 80)">crossing over</span> to the attacker's side

notice that this was starting to become an issue also to emails
as the emails could be opened in the browser and the could read HTML documents and execute JavaScript, so emails was a direct usage of universal XSS and a real danger to many companies.

so developers understood the issue and even talked about <span style="color:rgb(0, 176, 80)">reflected XSS</span>
![[Same Origin Policy-20241202220303999.webp]]
so this is a link that looks like it is going to microsoft but actually it is pointing to another wesbite foo.com with a vulnerable parameter id,
supposedly this parameter id is reflected onto the page.
which loads the malicious script on your website and executes it

<span style="color:rgb(0, 176, 80)">THIS IS WHERE THE NAME CROSS SITE SCRIPTING IS CONFUSING</span> 
because you are injecting a script and not a website

<span style="color:rgb(0, 176, 80)">BUT</span> 
the term was coming from a time when the <span style="color:rgb(255, 192, 0)">issue originated</span> from a <span style="color:rgb(255, 192, 0)">script</span> being loaded from <span style="color:rgb(255, 192, 0)">another website</span> or from <span style="color:rgb(255, 192, 0)">another frame</span> called <span style="color:rgb(0, 176, 80)">cross frame</span> 


# Explanation 2
Link: https://guptadeepak.com/customer-identity-hub/understanding-the-same-origin-policy-a-security-overview#introduction-to-the-same-origin-policy-sop

- The **Same-Origin Policy (SOP)** is a web security measure that prevents a document or script from one origin from accessing resources from a _different_ origin. It's like having separate fenced-off areas – one website can't just waltz into another's backyard and start poking around.

<mark style="background: #BBFABBA6;">What is an origin</mark>
- "Origin" is the scheme (like `https://`), hostname (domain name), and port number. So, `https://example.com:443` and `https://example.com:8080` are <mark style="background: #BBFABBA6;">_different_ origins</mark>, even though they're the same domain. Gotta watch those ports!
- It's those subtle differences that will get ya. A site is considered the same origin <span style="color:rgb(210, 127, 127)">only if _all three_ of these match _exactly_.</span>

	For example, `https://example.com` and `https://example.com/app1` are cool because they are the same origin, but `https://example.com` and `http://example.com`? Nope—different scheme, different origin.


- It also protects against **Cross-Site Request Forgery (CSRF)** attacks. <span style="color:rgb(255, 192, 0)">CSRF tricks a user's browser into sending unwanted requests to a server they're already authenticated with</span>. SOP makes it harder for attackers to exploit these vulnerabilities by restricting cross-origin requests.
- Think of "origin" as a website's identity card, the one that the internet's bouncer—the Same-Origin Policy—checks religiously.

- this origin stuff really matters when you are slinging around APIs. Your browser, acting as a vigilant guard, slams the door on JavaScript trying to grab data from a different origin. That's where **CORS (Cross-Origin Resource Sharing)** comes in; it is like a permission slip that tells the browser, "Hey, this cross-origin request is legit."
- الCORS  header بيعمل زى الكارت الى بيقول مسموح لل request دا يعدى الاسوار بين الorigins

<mark style="background: #BBFABBA6;">Next, we'll dive into the exceptions to the Same-Origin Policy and understand how CORS helps you bypass these security measures, when necessary. ??</mark>

بس عندنا بعض الexceptions عشان الدنيا تمشى صح
- **CORS** is a mechanism that uses **http headers** to let servers declare which origins are cool to access their resources. It's like the server saying, "Hey, I trust these guys; let them in."
- Think of it as a handshake. The server checks the `Origin` header in the request and then decides whether to respond with an `Access-Control-Allow-Origin` header that lists the allowed origins.
- what is a <mark style="background: #ADCCFFA6;">preflight request</mark> ?? That's where the browser sends an `OPTIONS` request to the server first. It's like asking, "Hey, can I do this?" before actually doing it. The server then says either "Yep, all good!" or "Nope, no way!"
- <span style="color:rgb(0, 176, 240)">This is an older trick, honestly. It uses the script tag to bypass SOP. See, the script tag _can_ load from anywhere, no questions asked. it's less secure than CORS. It's only supports GET requests and doesn't do those fancy preflight checks.</span>
- هنا انا مش فاهم دى بس تقريبا ال script ممكن يعمل get request على حاجة و بيعمل bypass ll CORS
- لما تكون بتconfigure الwebsite بتاعك و محتاج تعدى ال SOP same origin policyو عندك حلين الCORS cross origin resource sharing وال JSON padding (JSONP) وعشان تشوف الفرق دور على النت ولكن الفكرة ان دوا هدفهم اقدر افوت شوية فى ال SOP وانا بظبط الdomains بتاعتى

# Explanation 3 "Professor mode POE AI"
## 1) What enforces SOP: browser vs developer?

### **Same-Origin Policy (SOP) is enforced by the _browser_**

SOP is a **security mechanism implemented by user agents (browsers)**, not by front-end code you write and not by backend code.

- When your front-end JavaScript tries to read data from another origin, the **browser blocks access** (e.g., via the `Same-origin` restriction on reading responses).
- The developer code runs _inside the browser_, but it **cannot disable SOP** in normal circumstances because SOP is part of the browser’s security model.

**Key keywords**

- **Enforced by browser** (client-side security boundary)
- **Not configurable by app code**
- Applies to _read/inspect_ access of responses (not just “sending requests”)

---

## 2) “Is it applied by the front end or the backend?”

### SOP is mainly a **front-end/browser** rule.

Backend servers do not automatically “apply SOP” as a browser rule; however, backend controls can **influence whether cross-origin access is allowed** _at the HTTP level_.

There are two layers:

1. **Browser layer (SOP):**
    - Blocks your JS from reading cross-origin responses unless allowed.
2. **HTTP layer (CORS or other headers):**
    - Lets the browser know whether it should allow the JS to _read_ cross-origin responses.

**Key point:**

- Without browser permission, your JS cannot freely read `https://other-origin.com/...` responses, even if the request “goes out”.

---

## 3) Can the developer disable SOP?

### **No, not directly.**

A developer generally **cannot disable SOP** from:

- front-end JavaScript
- backend frameworks
- typical application configuration

Because SOP is enforced by the browser runtime itself.

### What developers _can_ do (the “allowed cross-origin” approach)

Instead of disabling SOP, developers use **CORS (Cross-Origin Resource Sharing)** to _permit_ certain cross-origin reads.

**How it works (high level):**

- Your JS makes a cross-origin request.
- Browser checks SOP.
- If server includes appropriate **CORS response headers**, browser allows access to the response in JS.

**Key keywords**

- **CORS**
- `Access-Control-Allow-Origin`
- `Access-Control-Allow-Credentials`
- Preflight: `OPTIONS` + `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`
- Credentials rules: wildcard origin + credentials = wrong / blocked

### Also important: “sending” vs “reading”

Even with SOP in place:

- The browser often still allows **sending** cross-origin requests (depending on what you’re doing: `img`, `form`, `script`, navigation, etc.).
- But SOP controls whether your JavaScript can **read the response**.

So developers don’t “turn off” SOP; they instead control **what the browser will allow you to read**.

---

## 4) Summary (exam-style)

- **SOP is enforced by the browser**, not the developer and not directly by backend.
- Developer **cannot disable SOP** for normal users.
- Developer can **design around it** using:
    - **CORS**
    - sometimes other mechanisms (tokens, same-site cookies, etc.)
- SOP primarily restricts **reading response data** from another origin.

---

## 5) Check understanding (answer these)

1. In your own words, who enforces SOP: **browser** or **backend server**?
2. If a front-end script requests a different origin, does SOP necessarily prevent the request from being sent, or does it mainly restrict _reading_ the response?
3. What mechanism do developers typically use to make cross-origin responses readable by the browser: **CORS**, **CSRF tokens**, or something else?