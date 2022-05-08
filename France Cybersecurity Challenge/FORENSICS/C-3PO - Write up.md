# C-3PO - Write up

# Enoncé :
![enonce](https://user-images.githubusercontent.com/66923124/167313300-adcb2be4-2ac5-495c-9388-80a691a97410.PNG)


# Résolution

Pour commencer, j'ouvre la capture réseau avec Wireshark et me balade dans celle-ci. <br>
Je découvre à un moment donné de la base64 dans un paquet :

![1](https://user-images.githubusercontent.com/66923124/167313717-9f007b4f-6bb0-4379-b21b-404c4c244ac5.png)

En regardant bien les détails du paquet, on peut voir que l'IP et le port de destination correspondent à <em>172.18.0.1:1338</em> :

![1](https://user-images.githubusercontent.com/66923124/167313811-aa0791b6-9692-44c2-9d35-99475ecd0d90.png)


J'applique donc un filtre sur Wireshark afin de garder uniquement les paquets TCP à destination de l'IP 172.18.0.1 via le port 1338 :

![1](https://user-images.githubusercontent.com/66923124/167313897-a7b6f771-dc30-44d3-800b-bfa3a75d9d7f.png)

Je fais ensuite clic droit sur le premier paquet, puis Suivre le Flux TCP :

![1](https://user-images.githubusercontent.com/66923124/167313942-8208cb6e-7010-4951-b599-08ffd8d65320.png)

...et tombe sur ce joli paquet :

![1](https://user-images.githubusercontent.com/66923124/167314016-bbff6728-bc3f-4aea-a17b-3767dea2947e.png)

Je suis donc le flux TCP suivant (le 131) et tombe sur ce qui a tout l'air d'être le flag encodé en base64 :

![1](https://user-images.githubusercontent.com/66923124/167314073-d1c5c8b8-b658-49a2-bf44-4b04f9ac2b47.png)

Je copie donc tout le contenu du flux et le colle dans Cyberchef pour décoder tout ça :

![cyberchef_decode_flag](https://user-images.githubusercontent.com/66923124/167314163-d58d23ee-aaa0-4b14-ad52-d2cb86fe1efa.png)

Ainsi, après avoir appliqué le filtre <strong> From Base64</strong>, il suffit simplement de cliquer sur <strong> Show all </strong> et un flag mignon apparaît :

![flag](https://user-images.githubusercontent.com/66923124/167313571-e04ad6a6-a182-481b-8489-c6bbd2cf456b.png)


<strong> FLAG : FCSC{2d47d546d4f919e2d50621829a8bd696d3cd1938} </strong>
