# ResolveME - Write up

For this challenge, a pcap file is given. The goal is to find the exfiltrated data. 

I start by opening the file in Wireshark :

![1](https://user-images.githubusercontent.com/66923124/164985496-ee016cce-2bc3-453d-a23a-0a4e26a88a23.png)

That's a lot of packets 👀. Because I'm lazy, I directly check the HTTP objects. <br>
To do that, I go to : <strong>File --> Export objects --> HTTP </strong>

Looks like we have some interesting data here :

![1](https://user-images.githubusercontent.com/66923124/164985754-59b710d2-c019-4b87-bec2-9f8c0e05f86b.png)

I double click on the packet to access it. It seems like the data sent is base64 encoded :

![paquet](https://user-images.githubusercontent.com/66923124/164985787-5fe8057f-2f81-48e2-b087-6cda8e1e5a94.PNG)

I right click on the data and select <em>Export packet bytes</em> to save the base64 stream into a file :

![1](https://user-images.githubusercontent.com/66923124/164985979-df5823b5-8832-4b62-8ccd-2f1b409a57b7.png)

I tried to decode the file in the command line but it failed : <br>

![1](https://user-images.githubusercontent.com/66923124/164986237-d48beac9-7203-4f2b-9e99-a60f0c2fa69b.png)

So I came to this website to decode the base64 stream directly into a file : https://base64.guru/converter/decode/file 

And it worked pretty well :

![1](https://user-images.githubusercontent.com/66923124/164986406-b584e56e-24b9-434b-8982-09c11227dad7.png)


<strong> FLAG : MCTF{K1ND_3XF1LTR4T1ON_B4S3D_ON_DNS_PDF} </strong>
