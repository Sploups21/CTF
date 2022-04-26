# Challenge de recrutement KGB - Write up

For this challenge, the file <em>challenge_recrutement_kgb.exe</em> is provided.

I start by analyzing the strings of the binary in IDA :

![1](https://user-images.githubusercontent.com/66923124/164982311-c5e7fd34-030d-4542-b98d-c0c1e349b5cf.png)

Looks like we have some interesting strings. I double click on one of these and I'm redirected here.

![2](https://user-images.githubusercontent.com/66923124/164982383-3fb3e684-e181-4ada-bee8-3f2ba6ca5db7.PNG)

Let's find the cross references for the <em>Congratulations</em> string. To do that, I select the string and press <strong>X</strong> :

![1](https://user-images.githubusercontent.com/66923124/164982532-ed2e4832-45e1-4157-8a43-1661aef5791d.png)

After clicking on the xref, it seems like we are in the main function :
![main](https://user-images.githubusercontent.com/66923124/164982610-59e4ffae-907f-4e0b-98c2-c8cf2b4485de.PNG)

Since the architecture of the binary is x64, we can generate pseudocode for the function in IDA Freeware with <strong>F5</strong> :
![pseudo](https://user-images.githubusercontent.com/66923124/164982739-99a1bdf7-b1bb-4338-a8d4-15a7711a1547.PNG)


This code basically checks if the user input is 24 characters long.
If it's not, we have this error message : <strong>No. This is not flag.</strong>

If it is, we enter in a loop :
- This loop compares each character of our input with the value of v8[i] XOR 0x42.
So if the first letter of our string is equal to the first character of the array v8 XORed with 0x42, it checks the next character and so on, till the end of the string.
If one character of our string is not equal to that, we get this error message : <strong>Wrong. You not have flag.</strong>

On the other hand, if the comparison is successful, we have a success message : <strong>Congratulations. Bravo. You have flag. Here: MCTF{<em>flag</em></strong>}

We saw in the last image that v8 corresponds to an address (![unk](https://user-images.githubusercontent.com/66923124/164983488-487eecd8-97d3-49fd-8a59-476c8b6c4b59.png)). Let's check it to see the values of the array :

![aa](https://user-images.githubusercontent.com/66923124/164983647-6ffed748-2b18-4ad7-9f52-f79408161924.png)

This corresponds to our array of hexadecimal values that are XORed with the key 0x42. 

Now that we have the items of the array, final step is to decode it ! On cyberchef, I write the content of the array and convert it to ASCII. I then XOR the result with the hex key 0x42, which gives me the flag :

![1](https://user-images.githubusercontent.com/66923124/164983883-dec59a4f-97b6-4d7c-95ed-0cc4c4347328.png)

<strong> FLAG : MCTF{N4tH4N_1S_Th3_B35t} </strong>

