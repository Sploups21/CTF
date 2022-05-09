# Enoncé :

![flag](https://user-images.githubusercontent.com/66923124/167393875-57305a82-a889-45ad-af7f-329ee6b1cf2a.PNG)

# Résolution :

# Méthode 1 (la méthode bourrin)

Après avoir suivi les instructions fournies pour émuler le téléphone, je lance ADB afin d'investiguer en profondeur dans celui-ci :

![writeup](https://user-images.githubusercontent.com/66923124/167394352-b0e11f93-5c02-4e98-a011-4da868b64959.png)

Après plusieurs recherches dans le filesystem du téléphone, je remarque un dossier étrange dans /data/app :

![writeup](https://user-images.githubusercontent.com/66923124/167394629-67ec2ccb-ddc1-4df2-88ed-9b0c599d159a.png)

L'appli Authenticator ne faisant pas parti du challenge, je me concentre sur l'app <strong>inputmethod.greek</strong>. En regardant le contenu du dossier, on remarque un APK suspect :

![writeup](https://user-images.githubusercontent.com/66923124/167395072-3d93221d-a42c-4d78-93e1-a9593c0300c0.png)

Exportons donc le dossier contenant l'APK avec ADB pour l'analyser en profondeur :

![writeup](https://user-images.githubusercontent.com/66923124/167395276-8deb9a8b-6565-4fac-ac54-e38832eed47a.png)

On commence par unzip base.apk pour obtenir les différents fichiers de celui-ci :

![unzip_apk](https://user-images.githubusercontent.com/66923124/167395478-39ba955f-b014-4355-96c6-a19a3eb47826.PNG)

Analysons maintenant le fichier <em>classes.dex</em> qui contient toutes les classes relatives à l'application grâce à <strong>Bytecode-Viewer</strong> :

![analysons_classdex](https://user-images.githubusercontent.com/66923124/167395594-f4cf4d4a-20c3-4d79-9e18-ff3d7a2051ca.PNG)

Ainsi, en se baladant dans les différentes classes, on trouve rapidement celle qui nous intéresse, c'est à dire <em>KeyBoarder.class</em> :

![writeup](https://user-images.githubusercontent.com/66923124/167396019-edd6d1a6-20c4-46e4-8c2a-5661e486d862.png)

On peut voir dans cette dernière une multitude de chaînes de caractère en base64. <br> Mon premier réflexe est de les décoder sans même m'attarder sur le code et je remarque ainsi une ligne qui se démarque des autres :

![writeup](https://user-images.githubusercontent.com/66923124/167396339-cfda950e-f4e0-44ef-a926-58b83cc7ab37.png)

Regardons en détail cette ligne... elle a l'air d'être chiffrée, donc j'entame une cryptanalyse bas de gamme dessus pour déterminer quelle est la forme de chiffrement :

![cryptanalyse_du_bled](https://user-images.githubusercontent.com/66923124/167396558-76c3c724-d13b-4e09-8b0c-995ff81d4720.png)

Si on fait le guess qu'il s'agit du flag, qui commence par <strong>FCSC</strong>, on peut déduire qu'il s'agit d'un chiffrement par substitution. <br>

Vu la forme de la chaîne, je suppose qu'il s'agit de ROT47. Essayons de décoder celle-ci pour voir :

![writeup](https://user-images.githubusercontent.com/66923124/167396922-bea2d2e8-9f8d-403c-9543-895dd616a026.png)

Il s'avère que le guess était fructueux. <strong> FLAG : FCSC{0773265361c06ee96e83f43609ca93babe38d6edc4c3ddbe53779e0bf6994c89} </strong>
<br>

# Méthode 2 (la méthode "propre")

Cette méthode consiste à analyser proprement le code afin de savoir ce qu'il effectue.

Comme on l'a vu précédemment, 2 URLs sont contactées :
- 172.18.0.1:8080/debug
- 172.18.0.1:8080/you_won

Et la condition suivante est appelée :

![writeup](https://user-images.githubusercontent.com/66923124/167398311-090d0bfe-0625-4d9d-b81a-6a6552961ee3.png)

Mmmmh... encore une chaîne de caractère bizarre. Sûrement du ROT47 encore une fois, décodons là :

![writeup](https://user-images.githubusercontent.com/66923124/167398654-bfadd520-6d84-4542-a5a9-252885f4752b.png)

On a maintenant quelque chose qui ressemble à de la base64. Enlevons le tiret ainsi que le "h" après le "=" et décodons là aussi :

![writeup](https://user-images.githubusercontent.com/66923124/167399009-52edcc4b-1d4a-4fd3-a6e6-e5970c6368db.png)

Encore un truc qui ressemble à du ROT47 (décidemment...), décodons à nouveau la chaîne obtenue :

![writeup](https://user-images.githubusercontent.com/66923124/167399349-ff5f82ef-2c50-4eff-8edf-72ce2cceb1c2.png)

Un mot de passe magique ? Tout s'explique... On a 2 endpoints, une appli qui simule le clavier du téléphone et un mot de passe magique...

Sûrement un keylogger !

A partir de là, j'émule l'IP 172.18.0.1 et écoute en continu sur le port 8080 avec un script Python.
Ensuite, je vais sur l'émulateur et écrit le mot de passe magique sur le clavier et... le flag est obtenu :

![writeup](https://user-images.githubusercontent.com/66923124/167400139-410ea1cd-8d0b-4aa7-9a9c-6e2a8b63a3b2.png)

Toutes les touches tappées par l'utilisateur sont retransmises vers le serveur malveillant 172.18.0.1 via des requêtes POST, il s'agissait donc bien d'un keylogger 😁
