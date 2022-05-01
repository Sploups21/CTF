# Delayed Start - Write up

![Capture](https://user-images.githubusercontent.com/66923124/166145485-a1ad9e9b-367b-4359-8465-88005dded882.PNG)

Let's start by checking the command lines entered inside the memory dump :

![cmdline](https://user-images.githubusercontent.com/66923124/166145767-2e824b18-a50c-49c0-a4b7-16692bc3406b.png)

As we can see, we have a totally non-suspect process with the PID 568 here 🙃. Let's dump it :

![procdump](https://user-images.githubusercontent.com/66923124/166145831-22748f42-6f2a-4a08-b9bc-b88f5001e3fa.PNG)

Now that we have the executable, let's analyze it with IDA.

When we look at the imports, we can see that the Sleep function is used :

![imports](https://user-images.githubusercontent.com/66923124/166145887-c2026b01-054a-41af-9e18-bc7a381045f0.png)

Let's check the xrefs to see where it is called.

I double click on the function :

![func](https://user-images.githubusercontent.com/66923124/166145959-9d84417f-be79-4ab5-92f2-26e3a3bd5526.PNG)

And I press X on it :

![xrefs](https://user-images.githubusercontent.com/66923124/166145990-208a88c4-4779-4372-89cd-805df196e594.PNG)

Let's look at the last call, at <strong>sub_402964+2C</strong> (double click on it) :

![paramhex](https://user-images.githubusercontent.com/66923124/166146131-8708a45b-be7a-407d-9f43-17785a2cf3be.png)

We can see that the function takes the hex value <strong>0x493E0</strong> as a parameter, which corresponds to <strong>300000</strong> in decimal.

Since the Sleep function takes a parameter in milliseconds, our value is 300 seconds.
> https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-sleep

So we have our flag : <strong> PCTF{300} </strong>
