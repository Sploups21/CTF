# Trousse social - Write up

For this challenge an APK file named TrousseSocial.apk is given. Like the other Android challenge, the goal is to find the password of the app.

First we start by unzipping the APK :

![1](https://user-images.githubusercontent.com/66923124/164980705-76989b37-9422-437c-99b3-eb608c31b7f1.PNG)

Let's open the <em>classes.dex</em> file with <strong>Bytecode-Viewer.jar</strong> now :

![2](https://user-images.githubusercontent.com/66923124/164980739-fb295d00-4ddd-4487-9e75-421d30f68e02.png)


After some research inside the file, we can find the interesting part inside the <em>MainActivity$a</em> class : 

![bbb](https://user-images.githubusercontent.com/66923124/165310134-e0fc42f9-f6ae-4386-96eb-f46d3257f821.png)


After some analysis of the code we know that :

- we have a list of 12 integers, which corresponds to the ciphertext : <strong>{35, 117, 51, 75, 57, 49, 117, 201, 83, 127, 257, 17}</strong>
- we have a key : <strong>IMTHEBOSS</strong>
- a XOR is performed between the ciphertext and the key
- Finally, <strong>charAt() * 2 + 5</strong> is executed for each character of our ciphertext.

So we have something that looks like a decryption routine... 
 
I sent the code to a teammate who knows how to read well Java (this language gives me PTSD to be honest). He responded two minutes later with a beautiful Python script that reproduces the decryption routine :

![pepe](https://user-images.githubusercontent.com/66923124/164981857-244e4ecb-cd5e-41c7-bbae-16432e68a05e.png)

![5](https://user-images.githubusercontent.com/66923124/164981893-1baf63e5-6a75-4537-afbc-665ea233e109.PNG)

After execution of the script we have the flag (thank you stchvk !) :

![6](https://user-images.githubusercontent.com/66923124/164981926-a44e0840-7557-4901-971b-a2360d658adc.PNG)


<strong> FLAG : MCTF{FuCk_Tw1tt3R} </strong> 
