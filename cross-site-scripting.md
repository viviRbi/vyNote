# Cross site scripting
- Type: 
	- Stored XSS
	- Reflected XSS
	- DOM base
- Cross site scripting: Mostly Js, but can also be Java or Flash
- Stored XSS:
	- Persisted to server side data
	- Returned in a request
	- Affects any user, may not target a specific person
	- Unlikely to be detected
	- Ex: An attacker inject a payload into a forum post. That post then stored in database. Other user load the post which contains the payload. The browser execute the payload
- Reflected XSS:
	- Sent to server in request
	- Returned in the response
	- Affects any user following the link, more targeted than Stored XSS
	- Detected by war user
	- Ex: Attacker send a malicous link to user. The link might disguise the fact that there's a payload in it. When user click the link, it'll send malicous request to the server. If it is vulnerable, it'll response with the page containing the payload which will be executed
- The use of input sanitisation:
	- Untrusted data is frequently sanitised, such as <>'/"\;
	- Explicitly rejecting character is called a Black list. It easy to be incomplete
	- Explicily accepting only approved characters is called a White list approach. It is a lower rish approah

### BeEF
- BeEF : Browser Exploitation Framework, use to inject XSS. BeEF add an additional layer to the payload that gives greater flexibility, like to decide which kind of attack
