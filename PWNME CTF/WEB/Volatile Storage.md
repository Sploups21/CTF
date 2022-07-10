# Volatile Storage - Write up

![sc](https://user-images.githubusercontent.com/66923124/178142795-8f70412f-d384-45cc-8dec-1c5d9ea69aa2.png)

Pour ce challenge, on arrive sur un site web sur lequel on peut créer un compte uniquement avec un username :

![sc](https://user-images.githubusercontent.com/66923124/178142818-b58e3d5f-f008-4d3f-b602-452494b8f1cf.png)

Je créé donc un compte avec mon pseudo :

![sc](https://user-images.githubusercontent.com/66923124/178142857-7f0957bf-b944-4c9e-8ee4-641fcfed5aee.png)

Je possède ainsi une chaîne de caractère qui a l'air d'être encodée en Base64 et qui correspond à mon mot de passe :

![sc](https://user-images.githubusercontent.com/66923124/178142897-e5fb2771-a2c1-49ca-ac71-02566be054fe.png)

En décodant le Base64 avec <strong>Cyberchef.org</strong>, j'obtiens ce qui a l'air d'être de l'hexadécimal :

![sc](https://user-images.githubusercontent.com/66923124/178142958-c3630353-7042-4516-9686-378d6dec0605.png)

Je ne possède rien de concret en le décodant, donc peut-être qu'il s'agit d'un hash.
Pour en avoir le coeur net, je tente de hasher mon pseudo en MD5 et de voir le résultat afin de comparer :

![sc](https://user-images.githubusercontent.com/66923124/178143174-62e9c414-cf55-4127-a79c-b7476e29ac53.png)

Bingo ! On remarque une similitude entre les hashes. <br> 
En effet, si l'on regarde bien, on peut voir que le hash généré par le site web correspond simplement <strong> à la moitié du hash complet du pseudo ! </strong>


` ________aebfa206287d1352________ ` <br> 
` 9281bfa7aebfa206287d1352ce1abf28 `

Une fois que l'on a compris cela, on peut obtenir le mot de passe de l'admin sans problème.

Je génère donc le hash MD5 du username <em>admin</em>, choppe les 16 caractères du milieu de la chaîne, puis je la converti en Base64 en une commande, ce qui nous donne le mot de passe de l'admin :

![sc](https://user-images.githubusercontent.com/66923124/178143619-2eeab750-4eaa-497f-a162-e63504af710c.png)

Ainsi, en nous connectant avec ce mot de passe, on obtient bien le flag :

![flag](https://user-images.githubusercontent.com/66923124/178143669-b227b4e5-9836-413a-b4de-02d011c10abc.png)


<strong> FLAG : PWNME{G3Ner47i0n_fR0M_u53R_1nPu7_4r3_Pr3d1cTiBl3} </strong>



