# Session Spy - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166142801-ba33293c-c827-46a8-a729-9269f192f8cf.PNG)

For this challenge, a ZIP file is given. Let's extract it :

![unzip](https://user-images.githubusercontent.com/66923124/166142857-c52530f6-1848-4936-b474-2ccecd859c76.PNG)

We now have several folders of the Admin user, including Appdata :

![lss](https://user-images.githubusercontent.com/66923124/166142927-4c2798f8-c1f0-4c5b-9d79-205baff91202.PNG)

After some research, I found this very good article about RDP forensics and saw this :

![expli](https://user-images.githubusercontent.com/66923124/166143378-35a0065c-4008-4a8d-8694-a20dcec9a77a.png)
> you can find the article at this link : https://www.security-hive.com/post/rdp-forensics-logging-detection-and-forensics


Okay, let's see if we have something in this folder :

![see](https://user-images.githubusercontent.com/66923124/166143452-801239f4-6a23-4ab9-b77b-516954a0ca63.PNG)

Great ! To extract screenshots from the file, we can use this tool made by the ANSSI : https://github.com/ANSSI-FR/bmc-tools

Let's now use it to see if we can get something :

![bmc](https://user-images.githubusercontent.com/66923124/166143564-b60a7430-995d-44a2-a0e7-d7ef665236b9.PNG)

Last step is to search through the 2936 screenshots were our username is :

![imgs](https://user-images.githubusercontent.com/66923124/166143606-b4b99571-c3f5-462d-b608-8f3fe6d5da58.PNG)

After some digging into these images, we can see that a Powershell is opened with a command entered :

![good](https://user-images.githubusercontent.com/66923124/166143665-3582fb27-397b-4eae-9a78-974a23c6f003.PNG)

And if we try to reassemble the images, we get this :

![completed](https://user-images.githubusercontent.com/66923124/166144257-58bcf6dc-5768-4aa2-81dd-087d80348e21.png)

Since our flag is the username added, we then have the flag ! 

<strong> FLAG : PCTF{svc_admin} </strong>


