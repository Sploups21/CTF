# Exfil - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166146510-65376fca-7d1e-4def-aeb2-dc82ef8078e4.PNG)

For this challenge, a pcapng file is given. Let's look at it with Wireshark :

![wire](https://user-images.githubusercontent.com/66923124/166146594-2096593e-aa28-4ab2-9d5b-1c4c9e8f5996.PNG)

After some digging into the packets, the ICMP ones took my attention :

![hex](https://user-images.githubusercontent.com/66923124/166146654-0e47e0fc-8a81-4544-8345-abaa82929c46.png)

This looks like hex data. Let's put a filter to keep only the ICMP packets :

![icmp_example](https://user-images.githubusercontent.com/66923124/166146682-386ac6dd-b533-4d0c-956c-1c94b4038e9f.PNG)

After looking closely at the packets I noticed that the ICMP packets containing weird hex values are only the requests packets from the IP 192.168.18.128 to the IP 192.168.1.1 so let's make an awful filter to only keep these packets :

![awful_filter](https://user-images.githubusercontent.com/66923124/166146885-82d6d433-109e-4a49-a1c6-9d47ab77fab5.PNG)

Now that I have all the packets I want, I extract the data from these and obtain 40 raw files :

![packets](https://user-images.githubusercontent.com/66923124/166147023-1f64f3af-71fc-451a-aacc-3731af9911b7.PNG)

Let's look at the first file :

![schema](https://user-images.githubusercontent.com/66923124/166147186-457ff455-08f7-4dd2-b1da-c54f4dad3bec.png)

At this point I want to remove the 10 first bytes from each file to keep only the data framed in red and concatenate all into a single file.

To do that, I have made an ugly python script that does the job :

```
#!/usr/bin/python3

import os

#Remove the 10 first bytes of each file and output it in a new file (name of file with -out at the end)
for i in range(1,41):
	os.system("file=" + str(i) + " && dd if=$file of=$file-out ibs=10 skip=1")

#Create a new directory and move all the new files inside it
os.system("mkdir final && mv *-out final/")

#Concatenate all the new files into a single one
for i in range(1,41):
	os.system("cd final && cat " + str(i) + "-out >> output")
```

Let's launch the script :

![script](https://user-images.githubusercontent.com/66923124/166147494-3a59f631-a3e5-4af3-b609-e5e38293bdc6.PNG)

And show the final output :

![catfinal](https://user-images.githubusercontent.com/66923124/166147521-506555b6-4546-40b9-aa44-3e1595323a99.PNG)

Seems like it worked. Now, let's decode this output as hexadecimal with Cyberchef and obtain the flag :

![flag](https://user-images.githubusercontent.com/66923124/166147588-1ce0a688-e680-4734-98d6-0a0bdbdb7b3b.PNG)


<strong> FLAG : PCTF{n0t_4_v3ry_sn34ky_3xf1l} </strong>
