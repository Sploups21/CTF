# Foxi - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166140556-945984b7-ebea-4a51-afac-fa64c6190b4b.PNG)

For this challenge, a ZIP file was given. Let's extract it :

![unzip](https://user-images.githubusercontent.com/66923124/166140920-10b1936a-1f74-48da-81a0-546ed2ed2633.PNG)
![ls](https://user-images.githubusercontent.com/66923124/166140952-b936a0ca-0ff7-4681-89d5-cf83de740eb5.PNG)


Seems like we have an appdata folder. Let's do a tree on it to find the Profile folder (this is were all Firefox user data is stored) :

![tree](https://user-images.githubusercontent.com/66923124/166140689-eab835ba-8697-43ec-8914-ac1ba73bef99.PNG)

<strong> 🡆 Profile folder : 3y1wxf49.default-release </strong>


Now that we have the Profile folder, we can dump all the passwords from it with this tool : https://github.com/unode/firefox_decrypt

I launch the script with the Profile folder as a target and get the flag :

![flag](https://user-images.githubusercontent.com/66923124/166140811-b32dc4ab-f787-42c9-8631-abddfb38594d.PNG)


<strong> FLAG : PCTF{Br0ws3rs_ar3_th3_b3st_P@ssw0rd_R3p0s} </strong>
