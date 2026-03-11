# Section 01 What is XSS?
Many attack types
- reflected XSS vs stored type
- DOM based vs source based
- blind XSS
- mutation XSS
- CSTI

## Reflected
means user input gets reflected 
- into an attribute of an HTML tag
- into the HTML page
- into the javascript context

- user input doesn't get stored into database
- user input is not properly sanitized
- user input can contain javascript code

- can occur with POST CALLS
	- add CSRF into the mix
## Stored XSS
- user input gets stored into the database
- database value gets reflected
	- into HTML page
	- into HTML Tag attribute
	- into the javascript context
	- ...
- user input is not sanitized properly
	- at input
	- and at write to the database
	- and at read from the database
- user input can contain malicious JS code

-   stored XSS Can be self XSS 

## DOM XSS
DOM is document object model,
- ex: a website can have a Document object model and a source code, this source code can sometimes be injected
- sometimes the code can be injected in the DOM itself by what is called DIM Sinks
	- ex:
		```js
- var search = document.getElementByid('search').value;
- var results = document.getElementByid('results');
- results.innerHTML = 'You seached for :' + seach;
- results.innerHTML <<< DOM Sink
```

DOM Sinks:
	where user input enters the document object model
	- Eval()
	- InnerHTML
	- ...

- you should not seach for DOM sinks manuallu, you can automate the finding and then try to exploit them manually

MOST Common sources for DOM XSS
- arises from windows.location
- usually in query string(?)
- or fragment portion of URL(#)
	- <span style="color:rgb(255, 192, 0)">the fragment is always reflected XSS</span> because the data never goes on the server and it is always read by the browser only

## DOM vs Source based
![[XSS Survival Guide-20250428232820053.webp]]
not really talked about that much


## Blind XSS
- relies heavily on out of band servers (<span style="color:rgb(255, 192, 0)">means you are working on already setup servers and waiting for callbacks</span>)
- <span style="color:rgb(255, 192, 0)">I implement the payloads but I can not see the results</span>
- later we get a call informing payload triggered (<span style="color:rgb(255, 192, 0)">means the result is later retrieved</span>)
- can be stored and reflected
	- reflected in case of knowing a page and parameter exist but no excess

## Mutation XSS
you insert a broken payload and wait for the browser to repair it for it to become then a full fledged XSS

## CSTI (Client Side Template Injection)
- sometimes <span style="color:rgb(255, 192, 0)">CLIENT SIDE TEMPLATING IS BEING USED</span> (I still need to understand what is being used to understand the effect of the injection)