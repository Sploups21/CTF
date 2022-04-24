# Admin Panel - Write up

For this challenge an APK file named <em>AdminPanel.apk</em> is given.

I first start to unzip it to get the file <em>classes.dex</em>, which contains the classes of the application :

![unzip](https://user-images.githubusercontent.com/66923124/164978630-d835033f-24e0-4e6a-833f-747ad946deab.png)

Now, I open it with <strong>Bytecode-Viewer.jar</strong> to see it's content :

![bytecode](https://user-images.githubusercontent.com/66923124/164978743-4f1808a1-007b-4044-a769-5ec49c9ace9d.png)

After some digging inside the file, we find the class LoginDataSource.class, which contains a login mecanism, and we can see something interesting inside it :

![login](https://user-images.githubusercontent.com/66923124/164978924-d9264a9b-1b68-497c-8c81-23e34ddc1f2f.png)

We obtain this string which looks like hexadecimal : <strong>3456614A653572655665525233496D3372506E304D</strong>

I go on cyberchef to decode it :

![reverse](https://user-images.githubusercontent.com/66923124/164979373-9716c794-b44c-4407-93d5-072d7a3eec58.png)

Mmmmh... looks like the string is inverted. Let's try to reverse it :

![reverse2](https://user-images.githubusercontent.com/66923124/164979741-9cd05dc6-a3f5-46b7-8305-226cb6005f8b.png)

Looks like we now have some valid french words ! This is our flag 😊

<strong> FLAG : MCTF{M0nPr3mI3RReVer5eJaV4} </strong>
