# Flexi - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166144329-46ac9762-070b-471b-8f16-8752e3a6e0f1.PNG)

Let's extract the ZIP file given :

![unzip](https://user-images.githubusercontent.com/66923124/166144369-6e4f6ace-51ef-4446-802d-b9142a4bf272.PNG)

We have two files : <em>ntds.dit</em> and <em>system</em>. 
- ntds.dit is the Active Directory database that stores all the data of a domain, including passwords
- system is a registry file that is needed to dump the data of ntds.dit

Now that we have all the files needed, we can extract the password hashes from ntds.dit with <strong>secretsdump.py</strong>. <br>
We then obtain the flag in cleartext :

![flaaag](https://user-images.githubusercontent.com/66923124/166144827-796f0bf8-03b7-47e8-a93f-c3f27fbc9ee9.png)

<strong> FLAG : PCTF{CL34rT3xt_N3v3r_F3lt_S0_Gud} </strong>
