resources for study:
1. https://portswigger.net/web-security/web-cache-deception
2. talk about WCD : https://www.youtube.com/watch?v=mroq9eHFOIU

Mind map when studying web cache deception 
1. what is Web cache deception
2. what is cache ? (browser or server cache)
3. what is the role of CDN in cache service ?? (current)

<span style="color:rgb(0, 112, 192)">CDN vs cache vs load balancers and reverse proxy?</span>
- <span style="color:rgb(0, 176, 80)">cache : consider a book store where the owner keeps a shelf of the most requested books so he doesn't have to search the entire library for the book each time</span>
- <span style="color:rgb(255, 192, 0)">CDN: consier a library source in america and you're in egypt and egyptians request the same book, it would make sense for the book owners to open a new branch in egypt to serve the most bought books in egypt and if a book is not there then only in that case the branch in egypt requests it from the main branch and then serves it to the customer</span>
- <span style="color:rgb(0, 176, 80)">Load balancer: a load balancer is used to distribute the load equally between servers but also it is used to cache the application data to serve the data faster</span>
- <span style="color:rgb(255, 192, 0)">reverse proxy: is a server that sits between client devices and backend servers, forwarding client requests to the appropriate server and returning the server's response back to the client. It operates on behalf of the server, effectively acting as an intermediary.</span>

web cache deception is a type of data storing using the dynamic of cache systems
- cache is stored for static pages that don't change
- a page that contains your email and password is not a dynamic page and <span style="color:rgb(255, 192, 0)">should not</span> be stored, the keyword here is "<span style="color:rgb(255, 192, 0)">should not</span>"
- notice that the caching talked about here is not <span style="color:rgb(255, 192, 0)">browser caching</span> but <span style="color:rgb(255, 192, 0)">server caching</span> 
- so the web server using PHP or Django for example using regex to decipher the URL and return the meant page
	- so if the regex for example is containing profile like this "profile" it returns the profile page whether you request URL/profile or URL/profile/image.png
	- but if you put "profile$" it returns not found for any other page other than URL/profile because the $ sign means the end of line for this URL

<span style="color:rgb(255, 192, 0)">Conditions for WEB CACHE DECEPTION TO WORK</span> 
4. the caching server caches the content based on file extension and disregards caching header![[Web cache deception-20250101182536242.webp]] for sorry reasons , it is the customer preference to override their own server headers which the server service provided a way to override and then the attack condition can be met that the cache server will ignore the caching header
5. when accessing a page like "profile/none.css" it would return the same result as "profile"
6. notice that all these extensions can be caches![[Web cache deception-20250101183911819.webp]]
7. the user must be authenticated when accessing the deception URL for the first time

How to mitigate this attack
8. only cache file is their HTTP caching headers allow
9. store all static files in a designated directory
10. cache files by their content type
11. don't accept this : URL/home.php/nonexistant.css to return 200, instead return 302 or 404 instead
12. know all of the technologies meeting the conditions for web cache deception like : <span style="color:rgb(255, 192, 0)">Nginx , ASP.NET, PHP, Node.js, Ruby on Rails, java JSP servlets</span> 

you can also get web cache deception from delimiter using
- if you put a delimiting option that is only understood in server but not in proxy cache server
	- it will get delimited in server but cached in cache server

Encoded characters may also sometimes be used as delimiters. For example, consider the request `/profile%00foo.js`:
- The OpenLiteSpeed server uses the encoded null `%00` character as a delimiter. An origin server that uses OpenLiteSpeed would therefore interpret the path as `/profile`.
- Most other frameworks respond with an error if `%00` is in the URL. However, if the cache uses Akamai or Fastly, it would interpret `%00` and everything after it as the path

# delimiter discrepancies
due to inconsistent delimiters between different technologies, we get some WCD
- fr example ruby on rails uses the . char as a delimiter
	- so profile.css means return "profile", so if the server doesn't use the same delimiting symbol, then we can have web cache deception
	- the java spring framework uses the ; as a delimiter while the server may not do the same..............
- انت كدا محتاج تشوف حرف يكون شغال delimiter فى السيرفر ولكن بيتشاف مسار عادى فى الcache ف عليك انت تجرب اى هطل وتحط حروف مختلفة لجد ما يطلعلك الرد الطبيعى يبقى الديليميتر اشتغل
#### Note

Some delimiter characters may be processed by the victim's browser before it forwards the request to the cache. This means that some delimiters can't be used in an exploit. For example, browsers URL-encode characters like `{`, `}`, `<`, and `>`, and use `#` to truncate the path.

If the cache or origin server decodes these characters, it may be possible to use an encoded version in an exploit.

# Normalization discrepancies

if you have a <span style="color:rgb(255, 192, 0)">discrepancy between the origin server and the proxy server</span> in the decoding of the URL plus you have a <span style="color:rgb(255, 192, 0)">/static</span> request this may produce a web cache deception vulnerability
- notice that /static is a technique in many technologies to make the load less on the web server where if it gets any /static request, this simply means it needs some jpg, css or any other static file

so if you you give <span style="color:rgb(255, 192, 0)">/static/../profile</span> this is equivalent to <span style="color:rgb(255, 192, 0)">profile</span> and if you give it <span style="color:rgb(255, 192, 0)">/static/..%2fprofile</span> this is the same also but encoded
- so if the server decodes this correctly it would give the profile sensitive info
- if the cache server doesn't understand it <span style="color:rgb(255, 192, 0)">PLUS</span> it has a <span style="color:rgb(255, 192, 0)">rule of caching /static file</span>, then this would result in vulnerability

<span style="color:rgb(255, 192, 0)">what is normalization ? this means the resolving of the URL , meaning if you encoded chars, does it decode or try to fetch the URL as it is</span>
## how to check normalization in origin server
simply by changing the URL and checking the response of the server
if you have /profile
- try %2fprofile
- try /aaaa/../profile
- try /aaaa/..%2fprofile
all this just to see how the origin server responds to different encoding or symbolizing in the request


## how to check normalization in cache proxy server
simply get a cached request by checking with the proxy history
- find a cached photo 
- change the URL back and forth
- for ex: cached photo is /img/255.jpg
- <span style="color:rgb(255, 192, 0)">change it to /aaa/../img/255.jpg</span> -> if it responds with the same photo, this means it normalized the URL at the cache server and responded with the photo
- <span style="color:rgb(255, 192, 0)">check the encoding: /aaa/..%2f/img/255.jpg</span> -> if photo comes up, this means the cache server can decode
- if you checked with a photo that needs authentication to come up, you would be 100 percent sure that it was cached at the proxy server



# I am going to pause web cache deception for some time as it is hard for me to grasp it completely