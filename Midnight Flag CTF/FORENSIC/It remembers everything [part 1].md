# It remembers everything [part 1]

For this challenge, we have a memory dump. The goal is to find the username and the computer name. <br />
> The format of the flag is : MCTF{username:computer_name}

First, let's determine the profile of the memory dump with Volatility :

![1](https://user-images.githubusercontent.com/66923124/164984798-9dbdde3d-7b6f-4862-be0a-7f63fd79f23e.png)

🡆 <strong>Win7SP1x64</strong>

Now to see the users of the machine, I dump the SAM database :

![1](https://user-images.githubusercontent.com/66923124/164984966-a5de75cc-458e-41d8-ab5e-506fd2800dcd.png)

🡆 username : <strong>h4ck3rM4n</strong>

Next, we do a <strong>hivelist</strong> to see the offset of a hive that contains the machine name. In our case, \REGISTRY\MACHINE\SYSTEM : 

![off](https://user-images.githubusercontent.com/66923124/164985094-b1c1d41d-3fa8-4af5-9b3f-d26f80c4edef.png)


The last thing to do is to extract the content of the key of the hive which contains the computer name :

![1](https://user-images.githubusercontent.com/66923124/164985220-28c2bcb4-ed19-4eba-b3b7-ae1fff9847a7.png)

🡆 computer name : <strong>H4CK3RC0MPU73R</strong>

<strong> FLAG : MCTF{h4ck3rM4n:H4CK3RC0MPU73R} </strong>
