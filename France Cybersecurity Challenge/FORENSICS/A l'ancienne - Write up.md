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

![1](https://user-images.githubusercontent.com/66923124/167315367-1f0403e5-e765-430b-8514-eeddf02151ce.png)

Bon, on a un truc qui ressemble à quelque chose. Prenons un bout de la 1ère ligne et tentons de la décoder pour voir à quoi on à affaire :

![1](https://user-images.githubusercontent.com/66923124/167315340-8ace4107-05ee-4fb9-bb63-c5f8f29cc0aa.png)

Le header est <strong> 1F 8B 08 </strong>... ce qui veut dire qu'on a affaire à du GZIP :

![1](https://user-images.githubusercontent.com/66923124/167315407-85df03cf-003f-456b-a969-83f4a6d7557a.png)

> https://en.wikipedia.org/wiki/List_of_file_signatures (merci wikipédia)
<br>

On peut ainsi déduire que pour chaque header que l'on voit, on a une archive gunzip différente :

![1](https://user-images.githubusercontent.com/66923124/167315522-2f936402-4dcf-4852-8f13-37670e302a4f.png)

A partir de ce moment là, je me dis que tout est plié : il ne me reste plus qu'à décoder chacun des blocs de base64, puis mettre le contenu décodé dans des fichiers pour obtenir les archives, sauf que :

![1](https://user-images.githubusercontent.com/66923124/167315688-f58be2c2-44c7-42c5-842e-13ff381ceabd.png)

Evidemment, ce serait trop facile non ?

Après des heures de galère à réfléchir d'où pouvait provenir l'erreur, j'ai pensé à un truc.
Les <strong>*</strong> me perturbent... et si ces dernières correspondaient à des <strong>+</strong>, qui syntaxiquement parlant, en Base64 seraient corrects ?

Essayons cela avec le 1er bloc.

<strong> Avant : </strong>

![1](https://user-images.githubusercontent.com/66923124/167315918-96c6c523-36ff-4d53-bd65-ed6e28d689ae.png)

<strong> Après : </strong>

![1](https://user-images.githubusercontent.com/66923124/167315951-fada22a0-d855-4f86-98bc-514f0fd00ab9.png)


Je copie donc ce bloc sur Baseguru pour le convertir en fichier :

![1](https://user-images.githubusercontent.com/66923124/167316061-172028e5-d328-473e-aac5-b1b2986133e8.png)

>https://base64.guru/converter/decode/file

Et tente de le décompresser avec gzip :

![1](https://user-images.githubusercontent.com/66923124/167316198-ac86405e-7e14-4bcb-896a-a318a7eccc09.png)

Bingo ! Ca marche parfaitement maintenant 😁


Ainsi, il ne reste plus qu'à réaliser la même manip avec tous les blocs en base64 (5 au total) en les nommant respectivement par leur nom :

![ls_gzip_files](https://user-images.githubusercontent.com/66923124/167316326-dc8f4cf0-93ce-4455-958a-9295a0e2bcbe.PNG)

Après décompression de ces derniers, on obtient bien des fichiers valides :

![gzip_decompressed](https://user-images.githubusercontent.com/66923124/167316400-0eb9f546-fbd4-477a-b4a1-54481083c92a.PNG)

Après inspection individuelle de chaque fichier, il s'avère ainsi que le flag se trouve dans le fichier Word <em>file4</em> :

![flag](https://user-images.githubusercontent.com/66923124/167316433-a8d1bf6c-a685-4d24-a829-963720b6661b.PNG)

<strong> FLAG : FCSC{18e955473d2e12feea922df7e1f578d27ffe977e7fa5b6f066f7f145e2543a92} </strong>
