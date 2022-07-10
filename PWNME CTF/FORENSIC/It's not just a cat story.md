# It's not just a cat story - Write up

![enonce](https://user-images.githubusercontent.com/66923124/178142073-dce272c8-6b2d-42aa-96ed-d04346d0f748.png)

Pour ce challenge, on possède une image disque en format Encase (.e01)
Je commence par monter le fichier Encase :

![sc](https://user-images.githubusercontent.com/66923124/178142557-52740f94-aeb1-47cc-b828-deeedc9228dd.png)

En regardant ce qui a été monté, on peut voir qu'il s'agit d'une partition DOS/MBR propre aux disques Windows :

![sc](https://user-images.githubusercontent.com/66923124/178142583-e682fc9b-398e-4624-b37f-c4e48c11d4fc.png)

Je transfert donc l'image disque <em>ewf1</em> vers mon Windows, puis lance FTK Imager.

En ouvrant l'image, on peut voir que pas mal de fichiers ont été supprimés :

![sc](https://user-images.githubusercontent.com/66923124/178142646-77119ff4-d358-45ac-aa6f-6d44fad04133.png)

J'exporte donc tous les fichiers de <em>root</em> vers mon propre disque :

![sc](https://user-images.githubusercontent.com/66923124/178142676-d755977c-5bf9-4bb5-b5e0-d2c5cf79de93.png)

Je peux maintenant visualiser les différents fichiers :

![sc](https://user-images.githubusercontent.com/66923124/178142713-c2121b2b-4879-4aaf-9d61-8470ed7da8bd.png)

En regardant le tout dernier, on peut voir qu'il s'agit de celui qui contient le flag :

![sc](https://user-images.githubusercontent.com/66923124/178142732-f908d404-1753-4aa1-badd-4092a5b66399.png)


<strong> FLAG : Flag{K3PT_Y0U_W41T1N6_HUH} </strong>



