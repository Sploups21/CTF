# Échec OP 1-3 - Write up

# Enoncé :

![enonce](https://user-images.githubusercontent.com/66923124/167387637-7a432711-169b-4c72-9d4a-ac1b412e512b.PNG)

# Résolution :

Après extraction de l'archive, on obtient un fichier .raw, qui correspond au disque dur de l'admin.

Commençons par regarder les partitions :

![writeup](https://user-images.githubusercontent.com/66923124/167388800-30985def-3b28-4458-9415-5274d9e37256.png)

La dernière partition, <em>fcsc.raw3</em> est la plus conséquente, c'est celle qui nous intéresse. Extrayons la :

![writeup](https://user-images.githubusercontent.com/66923124/167389057-e1e8d328-c2f0-4940-acc3-cd0d40d3d280.png)

On remarque que la partition est chiffrée par LUKS (Linux Unified Key Setup) :

![writeup](https://user-images.githubusercontent.com/66923124/167389258-6629443d-6be5-4576-8b6e-5d1f0eb78b05.png)

Le mot de passe fourni dans l'énoncé est <strong>fcsc2022</strong>. Essayons de déchiffrer la partition avec ce mot de passe en utilisant <strong>cryptsetup</strong>, puis affichons les partitions :

![writeup](https://user-images.githubusercontent.com/66923124/167389551-192c2527-bea0-443a-8685-a26e5b5a6214.png)

Parfait ! Notre partition est bien montée et déchiffrée.

Comme l'on peut le voir, notre partition déchiffrée se nomme <em>ubuntu--vg-ubuntu--lv</em> et correspond à un <strong>LVM</strong> (Logical Volume) :

![writeup](https://user-images.githubusercontent.com/66923124/167390075-f1381b42-83f6-4fbd-bc41-fd9613744a68.png)

Maintenant, il suffit de faire un <strong>lvdisplay</strong> afin d'afficher les informations sur le LVM et on obtient la date de création de ce dernier :

![writeup](https://user-images.githubusercontent.com/66923124/167390538-5341ae7f-9e4f-44af-a2a3-89d35c8552c2.png)

On possède donc comme date le 26 mars 2022 à 23h44 49 secondes ce qui donnerait ceci en respectant le format du flag : FCSC{2022-03-27T05:44:49Z}

Sauf qu'il ne s'agit pas de la date correcte, donc faisons des modifs :

```
Etant donné que ma machine virtuelle a un décalage de -6h, j'en additionne 6 à l'heure obtenue, ce qui donne :

FCSC{2022-03-27T05:44:49Z} (27 mars 2022 à 5h44 du mat')

Maintenant, il faut bien prendre en compte que l'heure est en format UTC. Il faut donc soustraire 2h au résultat obtenu, ce qui donne :

FCSC{2022-03-27T03:44:49Z}
```

Et voila, on a donc le flag : <strong>FCSC{2022-03-27T03:44:49Z}</strong>


> Liens qui m'ont aidé lors de ce challenge : <br>
> https://askubuntu.com/questions/63594/mount-encrypted-volumes-from-command-line <br>
> http://juho.tykkala.fi/Mount-and-decrypt-LVM-luks-encrypted-hard-disk
