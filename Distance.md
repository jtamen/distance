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

## Etape 1 : emetteur/balise
``||basic: Au démarrage||``, il faut régler ``||radio: radio définir groupe||`` dans la même plage pour les deux cartes
(groupe 1 dans notre exemple) Ces plages (groupes) peuvent aller de 1 à 256…
Choisis le numéro correspondant à celui de ton îlot afin d'éviter les interférences entre toutes les cartes.
Il faut également ``||radio: radio définir puissance de transmission||`` à 1.
```blocks
radio.setGroup(1)
radio.setTransmitPower(1)
```

 ## Etape 2 : emetteur/balise
 En continu ``||basic: Toujours||``, on envoie une chaine de caractères (et pas un nombre)
 toutes les 200ms. Ici ce texte est "1" qui correspond à la force du signal transmis.
```blocks
basic.forever(function () {
    radio.sendString("1")
    basic.pause(200)
})
```
## Etape 3 : emetteur/balise
Brancher la carte micro:bit en USB avec le câble fourni.
Téléverser le programme dans la carte micro:bit à l'aide de la commande "Télécharger".
Il est également conseillé d'enregistrer le programme dans un dossier en le renommant afin de le recharger en dehors du tutoriel
En cas de disfonctionnement on pourra  ainsi utiliser le mode débogage : La procédure est la même que pour téléverser dans la carte.
![Afficher bouton](https://edu.tactileo.fr/storage/download?filePath=0750360J%2Fjtamen%2Fpublic%2Fbp_telecharger.jpg)

## @showdialog
Il est vivement conseillé de supprimer tous les blocs créés dans le programme précédent, avant de commencer le nouveau programme !

## Etape 1 : récepteur
``||basic: Au démarrage||``, il faut régler ``||radio: radio définir groupe||`` dans la même plage pour les deux cartes
```blocks
radio.setGroup(1)
```

## Etape 2 : récepteur
Quand le récepteur reçoit un message de la balise, il stocke sa force dans une variable appelée ``||variables: signal||``
et l'affiche sur sa matrice à Dels.
On utilise le bloc ``||math: projeter||`` de la bibliothèque Maths pour convertir les numéros de force du signal radio 
de la plage -95 (faible) à -42 (fort) à une plage de 0 à 9 que nous pouvons utiliser pour tracer un graphe à barres.
```blocks
radio.onReceivedString(function (receivedString) {
    signal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    led.plotBarGraph(
    Math.map(signal, -95, -42, 0, 9),
    0
    )
})
```
## Etape 3 : récepteur
Si le ``||variables: signal||`` est supérieur à -60 (les 2 cartes sont très proches), alors on
montre l'icône ``||basic: Faché||`` et on met la sortie ``||pins: P0||`` à 1 (alerte sonore).
Sinon on met la sortie ``||pins: P0||`` à 0 (son coupé).
```blocks
radio.onReceivedString(function (receivedString) {
    signal = radio.receivedPacket(RadioPacketProperty.SignalStrength)
    led.plotBarGraph(
    Math.map(signal, -95, -42, 0, 9),
    0
    )
    if (signal > -60) {
        basic.showIcon(IconNames.Angry)
        pins.digitalWritePin(DigitalPin.P0, 1)
    } else {
        pins.digitalWritePin(DigitalPin.P0, 0)
    }
})
```

## Etape 4 : récepteur
Brancher la carte micro:bit en USB avec le câble fourni.
Connecter cette carte sur un shield possédant un buzzer en P0.
![Afficher bouton](https://edu.tactileo.fr/storage/download?filePath=0750360J%2Fjtamen%2Fpublic%2FDistance.jpg)
Téléverser le programme dans la carte micro:bit comme vu précédemment.
Il est également conseillé d'enregistrer le programme dans un dossier.

## FIN
Tester vos cartes !