# Distance
## @showdialog
Tutoriel créé par :
![Afficher logo](https://edu.tactileo.fr/storage/download?filePath=0750360J%2Fjtamen%2Fpublic%2Flogo-technotam-chappe1.jpg)

## @showdialog
Académie :
![Afficher logo-académie](https://edu.tactileo.fr/storage/download?filePath=0750360J%2Fjtamen%2Fpublic%2Flogo-IAN.png)

## @showdialog
Nous allons créer deux programmes différents, un pour la balise qui envoie constamment
un message radio de faible puissance. L'autre programme est pour le récepteur.
Quand le récepteur reçoit un message de la balise, il stocke sa force dans une variable
appelée signal et l'affiche sur son affichage LED.
Les signaux radio se renforcent lorsque vous vous rapprochez de l'émetteur, donc si le signal
est fort, cela signifie que l'autre micro:bit est probablement proche.
Si le signal radio est faible, l'autre micro:bit est probablement plus éloigné.
Il affiche un graphique en barres qui s'agrandit plus fort le signal et plus près vous
vous trouvez.
Il déclenche une alarme visuelle ou audible quand quelqu'un se rapproche trop.

## Etape 1 : emmeteur
``||basic: Au démarrage||``, il faut régler « radio définir groupe » dans la même plage pour les deux cartes
(groupe 1 dans notre exemple) Ces plages (groupes) peuvent aller de 1 à 256…
Choisis le numéro correspondant à celui de ton îlot afin d'éviter les interférences entre toutes les cartes.
Il faut également définir la puissance de transmission.
 ```blocks
radio.setGroup(1)
radio.setTransmitPower(1)
 ```