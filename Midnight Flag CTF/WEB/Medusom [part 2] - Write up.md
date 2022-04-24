# Medusom [part 2] - Write up

For this challenge, the hint given was <em> .git/ Respect </em> or something like that so... Let's steal the .git folder and analyze it !

To do this, I use <strong>gitdumper.sh</strong> 😎 :

![aa](https://user-images.githubusercontent.com/66923124/164998127-b49cc48a-1fa0-4216-be68-a4aa9bac279d.png)

After the .git folder is downloaded, I do <strong>git log --patch --all </strong> to see all the files that were modified in the repo.<br>
I also grep the flag format during the operation and... we got it !

![aa](https://user-images.githubusercontent.com/66923124/164998224-ae88e3ff-a658-4895-a43f-bdb9d5dbfab7.png)

<strong> FLAG : MCTF{b4s1c_g1t_uns3cured} </strong>
