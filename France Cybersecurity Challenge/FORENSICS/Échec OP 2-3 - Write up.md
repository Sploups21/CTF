# Enoncé :

![writeup](https://user-images.githubusercontent.com/66923124/167392259-01ee0bc0-69ff-42fa-a8ca-245334b8f3da.png)

# Résolution :

Lors du précédent challenge, on a bien réussi à déchiffrer la partition LUKS. Maintenant, tentons de la monter dans un dossier nommé <em>/mnt/echec_op</em> :

![writeup](https://user-images.githubusercontent.com/66923124/167392411-c7ff2502-08ff-411d-bf78-74f9be3de7f9.png)

Allons dans le dossier et regardons ce qu'il contient :

![flag](https://user-images.githubusercontent.com/66923124/167392692-ce565f2f-57bb-49c8-af4f-e964811963cb.PNG)

Il faut retrouver le mot de passe de l'utilisateur principal du serveur. Mon premier réflexe aurait été de bruteforce le hash contenu dans /etc/shadow, mais l'énoncé dit subtilement que ça ne servira à rien (<em>la force ne résout pas tout</em>).

Après plusieurs recherches, je découvre qu'un utilisateur nommé <em>obob</em> existe et je fais des recherches dans son répertoire /home sans succès.

Je décide donc d'aller dans le dossier /root et affiche tous les fichiers de ce dernier :

![flag](https://user-images.githubusercontent.com/66923124/167393267-e68c4444-bb7e-442b-8c07-b96c522881fe.PNG)

Intéressant, le fichier <strong>.bash_history</strong> n'est pas vide... regardons son contenu :

![flag](https://user-images.githubusercontent.com/66923124/167393632-2ef31acd-e51f-46b4-9bc3-85cd36808b9d.PNG)

On obtient ainsi le mot de passe de obob, et donc le flag.

<strong> FLAG : FCSC{CZSITvQm2MBT+n1nxgghCJ} </strong>
