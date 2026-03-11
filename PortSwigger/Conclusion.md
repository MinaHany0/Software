Vulnerabilities Conclusion
1. if they expose an endpoint which you can trave back like
	1. /api/users/login
	2. you can try to expose the /api/users API
2. if they send a hidden parameter
	1. like sending a discount parameter along with the order making without protecting it
3. if they don't make an allowed list for HTTP methods on the website, so you find some endpoints where you can use POST or PUT, ....
4. check the robots.txt file for extra endpoints
5. you can try to find hidden endpoints by fuzzing the website
6. if you reach an authorization failure on a POST method, try to mimic it with a GET method, maybe it is not protected.