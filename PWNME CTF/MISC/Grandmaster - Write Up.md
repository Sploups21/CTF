# Grandmaster - Write up

![sc](https://user-images.githubusercontent.com/66923124/178143735-42c7bb09-6fc7-4d7a-b10e-d66f130efe4f.png)

Pour commencer, regardons le fichier que nous possédons :

![sc](https://user-images.githubusercontent.com/66923124/178143797-5cd998f1-76e5-4f97-b832-7483b46e5dde.png)

Il s'agit d'une image JPEG. Je lance <strong>exiftool</strong> afin de voir les potentielles métadonnées de celle-ci :

![sc](https://user-images.githubusercontent.com/66923124/178143822-85080fa3-624b-4c3a-a69b-1dadd48cf801.png)

On peut voir directement une chaîne en Base64 étrange. Décodons là :

![sc](https://user-images.githubusercontent.com/66923124/178143864-1117338c-427c-4e0f-91f1-c14d2412d81d.png)

Ceux qui ont déjà réalisés des challenges de stéganographie en rapport avec les échecs reconnaissent directement ce format : il s'agit du format <em>PGN</em>.

> Ce format permet simplement de retranscrire des parties d'échecs afin de les rejouer automatiquement.

Sans plus attendre, je vais sur <em>https://incoherency.co.uk/chess-steg/</em> afin de décoder le message caché à l'intérieur du PGN :

![sc](https://user-images.githubusercontent.com/66923124/178143999-26cbb874-4c16-412b-aa6b-c698ba461dbc.png)

On obtient une chaîne de caractères étranges. Allons sur <em>https://www.dcode.fr/cipher-identifier</em> afin de voir si on peut en tirer quelque chose :

![sc](https://user-images.githubusercontent.com/66923124/178144099-b047a591-4756-479e-a43b-33bd3ec833f2.png)

Il s'agit apparemment d'un lien Youtube. Cliquons dessus pour voir :

![sc](https://user-images.githubusercontent.com/66923124/178144189-bde4e718-ca27-4193-9c00-863be2a9fc65.png)

Il s'agissait bien d'un id de vidéo Youtube et en regardant la description de la vidéo on trouve le flag !

<strong> FLAG : PWNME{1_L0v3_Ch3sSsss} </strong>



