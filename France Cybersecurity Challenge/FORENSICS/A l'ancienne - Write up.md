# À l'ancienne - Write up

# Enoncé :

![enonce](https://user-images.githubusercontent.com/66923124/167314233-446143ea-58f7-47bd-96f4-e8b35a812a44.PNG)

# Résolution :

En ouvrant la capture sur Wireshark, les premières choses qui sautent aux yeux sont les paquets DNS qui contiennent clairement de la Base64 :

![1](https://user-images.githubusercontent.com/66923124/167314406-5ec3e1a1-94f8-4c9a-b5fa-fe93d23ac1b6.png)

Sans plus attendre j'applique le filtre <em>DNS</em> afin de garder uniquement les paquets DNS, puis exporte la sélection en texte clair. <br>
> pour faire cela j'ai fait : fichier -> export packet analysis -> as plaintext <br>

J'obtiens ainsi le fichier suivant :

![queries](https://user-images.githubusercontent.com/66923124/167314547-ed7c5a7b-120c-4868-b07e-8df4b4a45aa3.PNG)

Après un peu de filtrage, j'obtiens un fichier plus propre, mais ça ne suffit pas. Enlevons les dernières colonnes qui se répétent :

![1](https://user-images.githubusercontent.com/66923124/167314711-47d5985a-0926-4158-a1c4-c79b9a43f331.png)

Et enlevons également les <strong>.</strong> et les <strong>-</strong> ainsi que les <strong>*</strong> pour avoir de la Base64 valide :

![1](https://user-images.githubusercontent.com/66923124/167314802-d73cd4d4-d499-43f8-b7a4-6616bd34ce77.png)

Bon, on a un truc qui ressemble à quelque chose. Prenons la 1ère ligne et tentons de la décoder pour voir à quoi on à affaire :



En revanche, les <strong>*</strong> me perturbent... et si ces dernières correspondaient à des <strong>+</strong>, qui syntaxiquement parlant, en Base64 seraient corrects ?
