# Man from space - Write up

For this challenge we only have one text :
```
Mｅrcｉ pοｕr touｓ νｏｓ retοｕrs ｓur lｅ ｔraⅰleｒ ! Sі vοuｓ ne ｌ＇ａνeｚ pａs ｅｎｃore ｖu, ｆonｃｅｚ ！ Ｎ'ｈésⅰteｚpas [...]
```

The format of the text makes me think of <em>Twitter Secret Messages</em> : https://holloway.nz/steg/

I copy and paste the text into the website, and I obtain this :

![1](https://user-images.githubusercontent.com/66923124/164994994-4bdc01eb-7d54-4e6d-874b-cb637d15e209.png)

> https://tinyurl.com/mctfgrey

When we click on this tinyurl link, we are redirected to https://ibb.co/YLtvxXD and we can see a QR code :

![1](https://user-images.githubusercontent.com/66923124/164995064-78ec2848-27b3-4dcc-a252-b47bc8db74fb.png)

I download the image of the QR code and I scan it with <strong>zbarimg</strong> :

![1](https://user-images.githubusercontent.com/66923124/164995097-954278c9-a9f7-465b-8647-0da49480657f.png)

I get a new link : https://ibb.co/DtQKcvZ

<br>
On this new link, we can see a new image :

![1](https://user-images.githubusercontent.com/66923124/164995156-f66d640d-dc0e-4ef9-b8f6-280efc5bd989.png)

I download the image and start analyzing it with <strong>exiftool</strong> :

![1](https://user-images.githubusercontent.com/66923124/164995233-e5f491fb-32e8-4917-862a-61b75fc747e4.png)

<em>"It would be better in gray"</em>...mmmmh... let's try to play with the colors.

To do this, I use <strong>stegsolve.jar</strong>. After swapping between diferents filters, we find the Gray bits filter, and by the way the flag :

![1](https://user-images.githubusercontent.com/66923124/164996015-83b0853c-443a-4c8d-bf14-0a91f5827282.png)

<br>

<strong> FLAG : MCTF{qR_Cod3_1s_fUn} </strong>
