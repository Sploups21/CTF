# Le jeton de Catwoman - Write up

For this challenge, a file named <em>catwoman.pcap</em>. The goal is to find the password of catwoman.

Let's see the content of this capture with Wireshark :

![1](https://user-images.githubusercontent.com/66923124/164989892-60c450e1-4319-4106-a89a-baad086606df.png)

This is a small Kerberos exchange. So to find the password of catwoman, we will need to steal it's TGS and crack it 😺

To list quickly the credentials inside the packet, I use NetworkMiner :

![1](https://user-images.githubusercontent.com/66923124/164990651-7f413fd4-5b3f-427e-84a0-ed478a3ec128.png)

Let's copy the password hash, put it inside a file and crack it with <strong>john</strong> :

![1](https://user-images.githubusercontent.com/66923124/164990690-adfe1028-5d17-4e73-a41e-57680463a912.png)
![1](https://user-images.githubusercontent.com/66923124/164990829-aa4d437b-87d7-4621-be7b-c5e2fa1202e9.png)


<strong>FLAG : MCTF{ilovebatman}</strong>
