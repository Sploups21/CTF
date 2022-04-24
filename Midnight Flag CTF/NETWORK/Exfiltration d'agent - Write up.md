# Exfiltration d'agent - Write up

For this challenge, we have a file named <em>transmission.pcapng</em> and we need to find the exfiltrated data inside it.

Let's open the file with Wireshark first :

![1](https://user-images.githubusercontent.com/66923124/164988261-e4b90c15-aaa7-4cac-960f-f262e1cf0973.png)

I check the HTTP objects :

![1](https://user-images.githubusercontent.com/66923124/164988348-eccff135-9169-4df8-b90c-8ff37155a5d5.png)

Mmmh... A zip file, a password and the debian package of frackzip... <br>
Let's look at the two first objects :

![1](https://user-images.githubusercontent.com/66923124/164988434-752ec20d-9b0d-461b-a7a6-81da87b41718.png)
![1](https://user-images.githubusercontent.com/66923124/164988766-fa04314c-76d4-4513-9c92-862de1f9cb29.png)

I tried to access to the URL's that I have found, but no success, so I started looking somewhere else.

If we take a closer look to the ICMP packets, we can see that the two first packets are pretty big for a simple ping :

![1](https://user-images.githubusercontent.com/66923124/164988918-2ae7699c-f3dc-427a-a457-2bf364f25239.png)

Let's look the at the first ICMP request packet in detail. I click on it and select the data part. <br>Then, I right click on it and select <strong>Show packet bytes</strong> :

![1](https://user-images.githubusercontent.com/66923124/164989054-46e44f5d-96d1-415f-a823-196a380945fd.png)

![1](https://user-images.githubusercontent.com/66923124/164989191-c09255ac-f285-479b-bab8-1c93adf5e69d.png)

A zip file inside an ICMP packet ??? Let's extract it into a file with the option <strong>Export packet bytes</strong> and let's try to unzip it !

![1](https://user-images.githubusercontent.com/66923124/164989395-99ec4325-47e3-41b5-bc42-97ace9578477.png)

Of course, a password is required... fcrackzip wasn't here for nothing 👀 <br>
I'm going to use <strong>john</strong> to bruteforce this zipfile.

First, I use <strong>zip2john</strong> to extract the hash of the protected zip :

![1](https://user-images.githubusercontent.com/66923124/164989531-2d302bdb-e440-4c46-8c37-79e732848f48.png)

Then, I start the attack with the wordlist rockyou.txt :

![1](https://user-images.githubusercontent.com/66923124/164989661-07ad2108-ffe8-4151-b6a6-0f154675dbd1.png)

Perfect, the password for the archive is <em>G3ars0fwar</em> ! Let's extract the zip with this password and get the flag now :

![1](https://user-images.githubusercontent.com/66923124/164989725-3705f096-3013-41c2-9007-cde83eac88f3.png)




<strong> FLAG : MCTF{g00d_0ld_1cmp_pr070c0l} </strong>
