# Weird encryption 

For this challenge, the following cipher is given :

```
%96 p$rxx  4@56  567:?6D hc AC:?E23=6 492C24E6CD[  D@ 2 C@E2E :@? @7 92=7 Whc^a l cfX >2<6D :E  A@DD :3=6 E@ @3E2: ? 2 DJ>>6EC:42= 4:A96C[ D:>:=2C E@ #~% b W7@C E96 ae =6EE6CD @7 E96 2=A9236EX] %96 7=28 : D |r%uL7a622`e6h`g5h`gh363ega`adfacd`gegg)ddd42fhg3h57f33`agdca2fa`62c24N
```

Let's ask to our best friend https://www.dcode.fr/cipher-identifier if it has a clue : 

![1](https://user-images.githubusercontent.com/66923124/164987177-a8f9c037-e478-4ecb-a3fe-a21dcac6e7a9.png)

High probability of ROT47. Let's check if it brings something :

![1](https://user-images.githubusercontent.com/66923124/164987251-0765c546-39d4-413e-a723-d7245550d299.png)


Looks like we have found something good 😀... or not 😞 
<br> 

I tried to submit the following flag but it didn't worked :

```
MCTF{f2eaa16e918d9189beb682125724518688X555ca798b9df7bb128542a721ea4ac}
```

Let's analyze it more further. 

The following string seems to be in hexadecimal... (maybe a hash ?) :
```
f2eaa16e918d9189beb682125724518688X555ca798b9df7bb128542a721ea4ac
```

But if this string is in hexadecimal, why is there a X in the middle ?
```

f2eaa16e918d9189beb682125724518688 X 555ca798b9df7bb128542a721ea4ac

```

Let's try to remove this "X" and identify it's type : <br>

![1](https://user-images.githubusercontent.com/66923124/164987845-43595f64-0b3a-40a6-8f08-915bc335e732.png)

Some SHA256 ! Let's try to decrypt the hash with this website : https://md5decrypt.net/Sha256/

![1](https://user-images.githubusercontent.com/66923124/164987949-17b1ab47-371a-43dd-ae8d-e076ab8a4730.png)


<strong> FLAG : MCTF{carebears1} </strong>

