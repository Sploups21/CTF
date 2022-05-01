# Vrai Crypt - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166144949-18c3d726-597b-481d-919c-e14ca4e2b9cc.PNG)

For this challenge we have two files :
- an encrypted disk file, named <em>SecretBoi</em>
- a 7zip archive, named memory.7z

Let's extract the archive first :

![extraction](https://user-images.githubusercontent.com/66923124/166145035-05d13858-b726-4cdb-b688-59c69fe1194e.PNG)

We now have a memory dump. Let's see the profile with Volatility :

![volprofile](https://user-images.githubusercontent.com/66923124/166145050-8634b6fa-741a-47de-9d68-5504e5e6d649.PNG)
🡆 <strong>Win7SP1x64</strong>

Since we need to decrypt the disk file, let's retrieve the TrueCrypt master key from the memory and save it in the current directory :

![truecryptmasterkeyvol](https://user-images.githubusercontent.com/66923124/166145072-0de3f4f6-935f-44b9-8524-e05be6d5f09b.PNG)

Now, after some research I found a python script that will permit us to decrypt and mount our TrueCrypt encrypted disk file : <br>https://github.com/AmNe5iA/MKDecrypt

Let's create a folder that will be our mountpoint and launch the script :

![mkdir](https://user-images.githubusercontent.com/66923124/166145254-73b9a910-10fb-42a0-8a56-0276ea40c139.PNG)

![decryption](https://user-images.githubusercontent.com/66923124/166145261-98c9e587-651a-4377-bfef-3fa2b1d9f1bc.PNG)

- <strong> -r </strong> means read-only.
- <strong> -v </strong> means verbose.
- <strong> -m </strong> is the mountpoint.
- <strong> -X </strong> means that we give the key as a file.

Now that the volume is mounted, we just need to go inside it and find the flag :

![affichage_flag](https://user-images.githubusercontent.com/66923124/166145403-8daec2e0-f676-4b65-80fc-a18b8d1928f5.PNG)

<strong> FLAG : pctf{r1P_7rU3CrPY7} </strong>
