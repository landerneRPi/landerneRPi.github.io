# MPT Landerneau: Atelier Raspberry Pi

## Mardi 14 janvier 2020

Séance de 18h à 20h.
Sujets:

   * programmation **Python**, 
   * utilisation du module **turtle** pour apprendre les bases

## Mardi 10 décembre 2019 

Séance de 18h à 20h.
Sujets:

* présentation Fablab Elorn \url{http://fablorn.net/}


## Samedi 23 novembre 2019

Séance de 10h à 12h.
Sujets:

* application labyrinthe avec Scratch,
* installation et découverte Node-red sur la Raspberry Pi.

## Mardi 12 novembre 2019

Séance de 18h à 20h.

Configuration Raspberry Pi

   * installation
Sujets:

   * utilisation de **git** via Github (pour contribuer au projet: documentation, code...)
   * mise en ouvre du pilote de moteur
   * mise en œuvre capteur de température
Programmation:

   * Python
Références:

   * \url{https://github.com/landerneRPi} ## premier projet: \url{https://github.com/landerneRPi/capteurs}
## Samedi 26 octobre 2019

   * Pilote de moteur: \url{https://github.com/Kidde82/raspberry-pi-dc-motor-pwm}, \url{https://github.com/gavinlyonsrepo/RpiMotorLib}\url{https://boutique.semageek.com/fr/1447-driver-de-moteur-continu-pas-a-pas-l9110.html}
Mais vous devrez le faire chaque fois que vous installez OpenCV.

Ajoutez `` / usr / local / lib / python2.7 / site-packages`` au PYTHON\_PATH : Cela ne doit être fait qu'une fois. Il suffit d’ouvrir ~/.bashrcet d’ajouter la ligne suivante, puis de se déconnecter et de revenir.

export  PYTHONPATH = $ PYTHONPATH : /usr/local/lib/python2.7/site-packages
Programmation

   * Scratch                             
   * Python: \url{https://opencv-python-tutroals.readthedocs.io/en/latest/py\_tutorials/py\_gui/py\_video\_display/py\_video\_display.html}
   * 

## Mardi 8 octobre 2019
Programmation

   * Scratch: initiation
   * Python: mise en place de l'environnement
\url{https://www.meetup.com/fr-FR/DIY-Robocars-Brest-FR/}
\url{https://diyrobocars.com/}

Références:
    \url{https://debian-handbook.info/download/fr-FR/stable/debian-handbook.pdf}
    \url{https://guidespratiques.traduc.org/guides/vf/Bash-Beginners-Guide/Bash-Beginners-Guide.pdf}
    

## Samedi 28 septembre 2019
Première séance de la saison 2019/2020

   * Présentation de l'atelier
       * Raspberry Pi
       * Programmation Python
   * Installation des logiciels/outils

## Samedi 21 juin 2019
Attention dernière séance de la saison.

Pour mettre à jour la Raspbian sur la Raspberry Pi: \url{https://www.raspberrypi.org/documentation/raspbian/updating.md}

   * par exemple passage de la Jessie à la Stretch

## Mardi 11 juin 2019

   * participation portes-ouvertes MPT: \url{https://infolocale.ouest-france.fr/landerneau-29103/agenda/portes-ouvertes-a-la-mptcs\_6598055}
   * Raspberry Pi: Bluetooth, application client sur Android
       * avec MIT App Inventor: \url{https://appinventor.mit.edu/explore/} (\url{http://appinventor.mit.edu/appinventor-sources/}
       * Android Studio: \url{https://fr.wikipedia.org/wiki/Android\_Studio}, installation: \url{https://developer.android.com/studio}
   * démonstration ESP32: \url{http://esp32.net/}, Exemple: \url{https://fr.wikipedia.org/wiki/NodeMCU}, \url{https://www.gotronic.fr/art-module-nodemcu-esp32-28407.htm}
##Samedi 25 mai 2019

   * suite de la mise en oeuvre du Bluetooth (server)
   * mise en oeuvre d'un écran e-ink sur la Raspberry Pi en python: \url{https://shop.pimoroni.com/products/inky-phat}*# Menu Préférences / Configuration Raspberry Pi / Interfaces: Activé SPI
*$ sudo apt update
*$ sudo apt upgrade
*$ git clone \url{https://github.com/pimoroni/inky.git}
*$ sudo pip3 install inky
*$ cd inky/examples/phat
*# exemple d'affichage du calendrier du mois courant
*$ python3 calendar-phat.py -c yellow

## Mardi 14 mai 2019

   * mise en oeuvre Bluetooth sur Raspberry Pi
       * installation*$ sudo apt update
*$ sudo apt install python3-pip python3-dev
*$ sudo apt-get install pi-bluetooth bluetooth libbluetooth-dev bluez blueman
*$ sudo pip3 install pybluez
*$ python3
*>>> # test
*>>> import bluetooth


   * application cliente en python
   * application server en python, serveur simple*import bluetooth
*server\_sock=bluetooth.BluetoothSocket( bluetooth.RFCOMM )
*port = 1
*server\_sock.bind(("",port))
*server\_sock.listen(1)
*client\_sock,address = server\_sock.accept()
*print("Accepted connection from ",address)
*data = client\_sock.recv(1024)
*print("received [%s]" % data)
*client\_sock.close()
*server\_sock.close()

## Samedi 27 avril 2019

   * mise en oeuvre sur la Raspberry Pi d'un LEDStrip Neopixel en python: \url{https://www.gotronic.fr/art-ruban-neopixel-rgb-1m-30-leds-ada1376-22878.htm} (alimentation séparée: 5v, 1 mètre, 30 LEDs)*# connexion de la masse commune entre le ruban, et connexion du fil de controle des LEDs
*$ sudo pip3 install rpi\_ws281x adafruit-circuitpython-neopixel
*$ python3
*>> > import board
*>>> import neopixel
*>>> pixels = neopixel.NeoPixel(board.D18, 30)  # broche RPi et nombre de LEDs sur le ruban$ fswebcam --no-banner -r 640x480 image.jpg
*>>> pixels[0] = (255, 0, 0) # première LED en rouge
*>>> pixels.fill((0, 255, 0)) # allume toutes les LEDs du ruban en vert

## Mardi 9 avril 2019

   * revue sur l'installation et le programme du pan tilt et du pilotage de la caméra PiCam: \url{https://github.com/pimoroni/PanTiltFacetracker}*#!/usr/bin/env python
*
*import cv2, sys, time, os
*from pantilthat import *
*
*# Load the BCM V4l2 driver for /dev/video0
*os.system('sudo modprobe bcm2835-v4l2')
*# Set the framerate ( not sure this does anything! )
*os.system('v4l2-ctl -p 8')
*
*# Frame Size. Smaller is faster, but less accurate.
*# Wide and short is better, since moving your head
*# vertically is kinda hard!
*FRAME\_W = 180
*FRAME\_H = 100
*
*# Default Pan/Tilt for the camera in degrees.
*# Camera range is from -90 to 90
*cam\_pan = 90
*cam\_tilt = -90 # montage à l'envers de notre installation
*
*# Set up the CascadeClassifier for face tracking
*#cascPath = 'haarcascade\_frontalface\_default.xml' # sys.argv[1]
*cascPath = '/usr/share/opencv/lbpcascades/lbpcascade\_frontalface.xml'$ fswebcam --no-banner -r 640x480 image.jpg
*faceCascade = cv2.CascadeClassifier(cascPath)
*
*# Set up the capture with our frame size
*video\_capture = cv2.VideoCapture(0)
*video\_capture.set(cv2.cv.CV\_CAP\_PROP\_FRAME\_WIDTH,  FRAME\_W)
*video\_capture.set(cv2.cv.CV\_CAP\_PROP\_FRAME\_HEIGHT, FRAME\_H)
*time.sleep(2)
*
*# Turn the camera to the default position
*pan(cam\_pan-90)
*tilt(cam\_tilt-90)
*
*while True:
*    # Capture frame-by-frame
*    ret, frame = video\_capture.read()
*    # This line lets you mount the camera the "right" way up, with neopixels above
*    frame = cv2.flip(frame, -1)
*    
*    if ret == False:
*      print("Error getting image")
*      continue
*
*    # Convert to greyscale for detection
*    gray = cv2.cvtColor(frame, cv2.COLOR\_BGR2GRAY)
*    gray = cv2.equalizeHist( gray )
*
*    # Do face detection
*    faces = faceCascade.detectMultiScale(frame, 1.1, 3, 0, (10, 10))
*   
*    # Slower method 
*    '''faces = faceCascade.detectMultiScale(
*        gray,
*        scaleFactor=1.1,
*        minNeighbors=4,
*        minSize=(20, 20),
*        flags=cv2.cv.CV\_HAAR\_SCALE\_IMAGE | cv2.cv.CV\_HAAR\_FIND\_BIGGEST\_OBJECT | cv2.cv.CV\_HAAR\_DO\_ROUGH\_SEARCH
*    )'''
*
*    for (x, y, w, h) in faces:
*        # Draw a green rectangle around the face
*        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
*
*        # Track first face
*        
*        # Get the center of the face
*        x = x + (w/2)
*        y = y + (h/2)
*
*        # Correct relative to center of image
*        turn\_x  = float(x - (FRAME\_W/2))
*        turn\_y  = float(y - (FRAME\_H/2))
*
*        # Convert to percentage offset
*        turn\_x  /= float(FRAME\_W/2)
*        turn\_y  /= float(FRAME\_H/2)
*
*        # Scale offset to degrees
*        turn\_x   *= 2.5 # VFOV
*        turn\_y   *= 2.5 # HFOV
*        cam\_pan  += -turn\_x
*        cam\_tilt += turn\_y
*
*        print(cam\_pan-90, cam\_tilt-90)
*
*        # Clamp Pan/Tilt to 0 to 180 degrees
*        cam\_pan = max(0,min(180,cam\_pan))
*        cam\_tilt = max(0,min(180,cam\_tilt))
*
*        # Update the servos
*        pan(int(cam\_pan-90))
*        tilt(int(cam\_tilt-90))
*
*        break
*
*    frame = cv2.resize(frame, (540,300))
*    frame = cv2.flip(frame, 1)
*   
*    # Display the image, with rectangle
*    # on the Pi desktop 
*    cv2.imshow('Video', frame)
*
*    if cv2.waitKey(1) \& 0xFF == ord('q'):
*        break
*
*# When everything is done, release the capture
*video\_capture.release()
*cv2.destroyAllWindows()


## Samedi 30 mars 2019

Séance au Family:

   * installation du pan tilt: \url{https://www.kubii.fr/cartes-extension-cameras-raspberry-pi/1873-pan-tilt-hat-kit-kubii-3272496007277.html}, \url{https://shop.pimoroni.com/products/pan-tilt-hat}, \url{https://github.com/pimoroni/pantilt-hat}
   * mise en oeuvre OpenCV avec la PiCam sur le pan tilt: \url{https://www.kubii.fr/cameras-accessoires/1653-module-camera-v2-8mp-kubii-640522710881.html}
##Mardi 12 mars 2019

Références OpenCV:

   * \url{https://opencv.org/}
   * \url{https://opencv-python-tutroals.readthedocs.io/en/latest/}
   * \url{https://www.pyimagesearch.com/} ## 
   * \url{https://docs.opencv.org/3.0-beta/doc/py\_tutorials/py\_tutorials.html}
   * 

   * \url{https://www.pyimagesearch.com/2018/07/19/opencv-tutorial-a-guide-to-learn-opencv/}
Exemple:
### face\_recognition\_exemple.py
*import cv2
*import sys
*
*# telecharger \url{https://github.com/Itseez/opencv/blob/master/data/haarcascades/haarcascade\_frontalface\_default.xml}
*# comme argument au programme
## lancer le programme $ python3 face\_recognition\_exemple.py haarcascade\_frontalface\_default.xml
*cascPath = sys.argv[1]
*faceCascade = cv2.CascadeClassifier(cascPath)
*
*video\_capture = cv2.VideoCapture(0)
*
*while True:
*    # Capture frame-by-frame
*    ret, frame = video\_capture.read()
*
*    gray = cv2.cvtColor(frame, cv2.COLOR\_BGR2GRAY)
*
*    faces = faceCascade.detectMultiScale(
*        gray,
*        scaleFactor=1.1,
*        minNeighbors=5,
*        minSize=(30, 30),
*        flags=cv2.cv.CV\_HAAR\_SCALE\_IMAGE #(si erreur remplacer par: " flags=cv2.CASCADE\_SCALE\_IMAGE "
*    )

*    # Draw a rectangle around the faces
*    for (x, y, w, h) in faces:
*        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
*
*    # Display the resulting frame
*    cv2.imshow('Video', frame)
*
*    if cv2.waitKey(1) \& 0xFF == ord('q'):
*        break
*
*# When everything is done, release the capture
*video\_capture.release()
*cv2.destroyAllWindows()

## Samedi 23 février 2019
Connexion sur le Raspberry Pi:

   * Relai: \url{https://www.gotronic.fr/art-module-relais-5v-ef03052-23553.htm}
   * DS18b20: \url{https://www.gotronic.fr/art-ds18b20-14094.htm}
##Mardi 12 février 2019
Connexion Raspberry Pi et capteur de température et humidité (DHT 22)

   * Capteur DHT 22: \url{https://www.gotronic.fr/art-capteur-de-t-et-d-humidite-dht22-20719.htm}
##Samedi 26 janvier 2019
Connexion Raspberry Pi et LED, puis servo-moteur

   * Servo Moteur SG 90: \url{https://www.gotronic.fr/art-servomoteur-sg90-19377.htm}

## Mardi 8 janvier 2019
Suite de la présentation vie privée

# Mardi 1er janvier 2019

Actualités

   * MOOC:
       * Apprendre à coder avec Python 3: \url{https://www.fun-mooc.fr/courses/course-v1:ulb+44013+session01/about}
       * Python 3 : des fondamentaux aux concepts avancés du langage \url{https://www.fun-mooc.fr/courses/course-v1:UCA+107001+session02/info}
       * Protection de la vie privée dans le monde numérique: \url{https://www.fun-mooc.fr/courses/course-v1:inria+41015+session02/about}
#Samedi 24 novembre

Base de données avec Python

   * Généralités
   * Base de Données: \url{https://fr.wikipedia.org/wiki/Base\_de\_donn%C3%A9es}
   * Un type de base de données:
       * Base de données **relationnelle**: \url{https://fr.wikipedia.org/wiki/Base\_de\_donn%C3%A9es\_relationnelle}
       * La théorie, l'algèbre **relationnelle**: \url{https://fr.wikipedia.org/wiki/Alg%C3%A8bre\_relationnelle}
   * Méthodes de développement de projet informatique autour du modèle relationnel
       * Merise: \url{https://fr.wikipedia.org/wiki/Merise\_(informatique)}
       * Génie logiciel et UML (en anglais): \url{https://en.wikibooks.org/wiki/Introduction\_to\_Software\_Engineering}
   * Le langage de requêtes pour les bases de données relationnelle: SQL:
       * \url{https://fr.wikipedia.org/wiki/Structured\_Query\_Language}
       *  \url{https://fr.wikibooks.org/wiki/Programmation\_SQL} 
   * Système de gestion de base de données: (SGBD):
       * SGBD / DBMS (en anglais): \url{https://fr.wikipedia.org/wiki/Syst%C3%A8me\_de\_gestion\_de\_base\_de\_donn%C3%A9es}
       * Système pour les bases relationnelle, SGBDR / RDBMS (en anglais): \url{https://en.wikipedia.org/wiki/Relational\_database\_management\_system}
       * Liste et comparaison de SGBDR: \url{https://en.wikipedia.org/wiki/Comparison\_of\_relational\_database\_management\_systems}
   * Python et les bases de données
       * API "standard" en Python (DB-API 2.0), Python Database API Specification v2.0: \url{https://www.python.org/dev/peps/pep-0249/}
           * ce qui veut dire qu'un module Python pour une base de données relationnelle quelconque (MySQL, PostgreSQL...) qui respecte ce "standard" DB-API 2.0, permettra d'avoir un code Python "portable" d'un SDBDR à un autre,
       * Python et base de données: \url{https://fr.wikibooks.org/wiki/Programmation\_Python/Bases\_de\_donn%C3%A9es}
       * Programmation Python: \url{https://fr.wikibooks.org/wiki/Programmation\_Python/Gestion\_d%27une\_base\_de\_donn%C3%A9es}
   * Installation et exemple avec SQLite3:
       * Python 3 et SQLite 3, module intégré à python (facile à utiliser): \url{https://docs.python.org/3/library/sqlite3.html}
       * Utilisation d'un outil de navigation d'une base SQLite: \url{https://sqlitebrowser.org/}
           * permet de créer, visualiser, détruire une base de données, les tables et les données
Installation sur une distribution Debian (et Debian like):
*# installation de DB Browser for SQLite
*$ sudo apt install sqlitebrowser
*# et/ou en ligne de commande
*$ sudo apt install sqlite3
*$ sqlite3
*QLite version 3.22.0 2018-01-22 18:45:57
*Enter ".help" for usage hints.
*Connected to a transient in-memory database.
*Use ".open FILENAME" to reopen on a persistent database.
*sqlite> 
# <control> + D pour sortir ou taper: .quit

Exemple de code Python:
*import sqlite3
*# créer une base de données en mémoire (volatile, disparaît à la fin du programme)
*conn = sqlite3.connect(':memory:')
*curs = conn.cursor()
*# création d'une table dans la base de données
*curs.execute('''CREATE TABLE contacts (nom text, prenom text, age integer)''')
*# ajouter une ligne dans la table 
*curs.execute("INSERT INTO contacts VALUES ('Mon nom', 'Mon prénom', 22)")
*# lire tous les champs et toutes les valeurs de la table
*curs.execute("SELECT * FROM contacts")
*# parcourir et afficher toutes les lignes
*print(curs.fetchall())
*[('Mon nom', 'Mon prénom', 22)]
*# mise à jour d'un champ dans une ligne pour une table
*curs.execute("UPDATE contacts SET age=45 WHERE nom='Mon nom'")
*# lire une ligne de la table suivant une condition sur un champ
*curs.execute("SELECT * FROM contacts WHERE age=45")
*# Afficher tous les résultats
*print(curs.fetchall())
*[('Mon nom', 'Mon prénom', 45)]

## Mardi 13 novembre 2018

Interface Graphique avec Python

   * Généralité sur l'interface graphique
   * Bibliothèques interfaces graphiques sous Linux
       * GTK: \url{https://python-gtk-3-tutorial.readthedocs.io/en/latest/}
           * création des interfaces graphique avec Glade: \url{https://python-gtk-3-tutorial.readthedocs.io/en/latest/builder.html}
       * QT: \url{https://www.qt.io/qt-for-python}
       * TK (TCL/TK): \url{https://docs.python.org/fr/3/library/tk.html}
   * Bibliothèques interfaces en mode texte
       * curses: \url{https://docs.python.org/3/howto/curses.html}
       * Dialog: \url{http://pythondialog.sourceforge.net/doc/}Installation
$ 
Exemples:
    

## Samedi 27 octobre 2018

Session:

   * Environnement Python
       * pip (gestion de paquets: modules python)
           * \url{https://docs.python-guide.org/dev/virtualenvs/}
           * \url{https://pipenv.readthedocs.io/en/latest/}
       * IDE (environnement de développement)
           * pycharm: \url{https://www.jetbrains.com/pycharm/}
           * eclipse: \url{http://www.pydev.org/}Atelier

   * Mise en œuvre avec exemple
#Exemple Python

Mon premier programme en python

Il s'agit de transformer une liste de prets de bibliothèque en un fichier csv, traitable par un tableur ou une base de données.


#!/usr/bin/env python
# -*- coding: utf-8 -*-

nouvline = ""
i = 0

ftxt = open("/home/pi/mediatheque.TXT",'r',encoding ='ISO-8859-1')
fcsv = open("/home/pi/mediacsv.txt", "a")

for line in ftxt:
    
    manque\_info = False
    #print (i, line)
    if ((i == 1) and (line.find ("Auteur") == -1)):
        #print ("ANOMALIE AUTEUR")
        nouvline = nouvline + ';' 
        manque\_info = True
                           
    if ((i == 2)and (line.find ("Année") == -1)):
        #print ("ANOMALIE ANNEE")
        nouvline = nouvline + ';'
        manque\_info = True
    
    nouvline += line.replace('\n',';')
    
    if (manque\_info):
        i += 1
    
    if (i == 3):
        fcsv.write(nouvline + '\n')
        #print(nouvline)
        nouvline = ""
        i = 0
    else:   
        i += 1
     
ftxt.close()
fcsv.write(nouvline)
fcsv.close()#!/usr/bin/env python

#jo

## Mardi 9 octobre 2018

Le deuxième mardi du mois de 18H à 20H:
l'accès aux salles se fait par l'arrière du bâtiment, la porte est ouverte le mardi soir
la salle N° 1 qui se trouve à l'étage est réservée le 2ème mardi pour notre atelier.
Accès par l’ascenseur ou la cage d'escalier.

Je pense qu'il faut lire 9 octobre. Moi j'ai tout faux. J'avais noté le 19 octobre. Pas bien!!
C'est exact :-)

Prévoir une clé USB pour stocker.

## Samedi 29 septembre 2018

Présentation de l'atelier 2018-2019

Quelques liens pour démarrer:

   * \url{https://www.raspberrypi.org/magpi/} (Magazines MagPI en anglais gratuit)
   * Un exemple: \url{https://www.raspberrypi.org/magpi/issues/74/} 
   * Existe aussi en français (payant, édité par Elektor): \url{https://www.magpi.fr/}
   * \url{https://www.humblebundle.com/} (publie parfois des lots de livres pas chers)
Programmation:

   * outil pour créer et manipuler des algorithmes (avec des exemples):  Algobox: \url{http://www.xm1math.net/algobox/}
   * pour s'amuser: \url{https://scratch.mit.edu/} (avec des exemples sur Internet ou sur le Raspberry Pi)
   * pour étudier les programmes des autres: source sur \url{https://github.com/}, exemples: \url{https://github.com/search?q=python}*installer git: $ sudo apt install git
*$ git clone \url{https://github.com/lewischeng-ms/tiny-basic.git}
*$ git clone \url{https://github.com/TheAlgorithms/Python.git}

Programmation Python:

   * installation de PyCharm (community): \url{https://www.jetbrains.com/pycharm/}
Installation de PyCharm (IDE pour Python, ce n'est pas le seul qui existe)

   * IDE (environnement de développement): \url{https://fr.wikipedia.org/wiki/Environnement\_de\_d%C3%A9veloppement}
   * récupération du fichier tar.gz sur \url{https://www.jetbrains.com/pycharm/download/download-thanks.html?platform=linux\&code=PCC}
   * à l'endroit où se trouve le fichier : pycharm-community-2018.2.4.tar.gz, le mien se trouve dans le répertoire **Téléchargement**# installation de java
$ sudo apt install openjdk-8-jdk
$ tar xf pycharm-community-2018.2.4.tar.gz
$ cd pycharm-community-2018.2.4/bin
$ ./pycharm.sh
# répondre aux questions (ou répondre par défaut)


## Samedi 8 septembre 2018

La MPT nous a prévu un stand pour le carrefour des associations le samedi 8 septembre 2018 de 9 H à 17 H.
L'installation sur le stand peut se faire de 8 H à 9 H.
Notre stand sur le carrefour est à côté de la MPT, le plan du carrefour est consultable à l’accueil de la MPT/CS.
On dispose d'une table blanche et de deux chaises. 
Un branchement électrique est disponible sur le stand il faut juste apporter des rallonges électriques.
Je serai disponible sur le stand toute la journée.


## Samedi 30 juin 2018

Session:

   * GPIOAtelier

   * Mise en oeuvre:

## Samedi 26 mai 2018

Session:

   * Utilisation d'OpenCV
   * Découverte de PyGame (SDL) pour créer des jeux
   * Découverte de Glade (GTK) pour créer des interfaces graphiquesAtelier

   * Mise en oeuvre:
       * Reconnaissance faciale de OpenCV avec une WebCam
       * Utilisation de Pygame
       * Utilisation de Glade
###Reconnaissance faciale de OpenCV avec une WebCam
Dans cet atelier, nous n'utiliserons pas la PiCam mais une Webcam (plus facile à trouver et à installer).
Ce qui veut dire aussi que vous pouvez tester cet atelier sur un n'importe quel ordinateur pourvu d'une Webcam.

Installation d'OpenvCV et ses dépendances:
*$ sudo apt install python-opencv
*$ sudo apt install python-numpy
*$ sudo apt install python-scipy

Test de la capture vidéo avec la Webcam, créer le fichier 'capture\_video\_webcam.py' avec le contenu suivant:
*import numpy as np
*import cv2
*
*cap = cv2.VideoCapture(0) # capture la webcam 0, la première webcam /dev/video0
*
*while(True):
*    # Capture frame-by-frame
*    ret, frame = cap.read()
*
*    # Our operations on the frame come here
*    gray = cv2.cvtColor(frame, cv2.COLOR\_BGR2GRAY)
*
*    # Display the resulting frame
*    cv2.imshow('frame',gray)
*    if cv2.waitKey(1) \& 0xFF == ord('q'):
*        break
*
*# When everything done, release the capture
*cap.release()
*cv2.destroyAllWindows()

Lancer l'application:
*$ python capture\_video\_webcam.py
Une fenêtre s'ouvre avec l'image de votre Webcam en noir et blanc. Appuyer sur 'q' pour quitter.

Application avec la détection d'un visage: détecte le visage et l'entoure avec un rectangle vert.
Ccréer le fichier 'face\_recognition\_exemple.py' avec le contenu suivant:
*import cv2
*import sys
*
*# telecharger \url{https://github.com/Itseez/opencv/blob/master/data/haarcascades/haarcascade\_frontalface\_default.xml}
*# comme argument au programme
*cascPath = sys.argv[1]
*faceCascade = cv2.CascadeClassifier(cascPath)
*
*video\_capture = cv2.VideoCapture(0)
*
*while True:
*    # Capture frame-by-frame
*    ret, frame = video\_capture.read()
*
*    gray = cv2.cvtColor(frame, cv2.COLOR\_BGR2GRAY)
*
*    faces = faceCascade.detectMultiScale(
*        gray,
*        scaleFactor=1.1,
*        minNeighbors=5,
*        minSize=(30, 30),
*        flags=cv2.cv.CV\_HAAR\_SCALE\_IMAGE
*    )
*
*    # Draw a rectangle around the faces
*    for (x, y, w, h) in faces:
*        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
*
*    # Display the resulting frame
*    cv2.imshow('Video', frame)
*
*    if cv2.waitKey(1) \& 0xFF == ord('q'):
*        break
*
*# When everything is done, release the capture
*video\_capture.release()
*cv2.destroyAllWindows()

Récupérer le fichier de détection de visage pré-entrainé 'haarcascade\_frontalface\_default.xml' avec la commande ci-dessous:
*$ wget \url{https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade\_frontalface\_default.xml}

Ensuite démarrer le script avec ce fichier:
*$ python face\_recognition\_exemple.py haarcascade\_frontalface\_default.xml

Placer vous face à la Webcam pour que la détection de visage fonctionne, appuyer sur 'q' pour quitter.

On peut détecter d'autres choses voir liste \url{https://github.com/opencv/opencv/tree/master/data/haarcascades}
ou entraîner un classifieur sur un modèle.

Références:

   * \url{https://opencv.org/}
###Utilisation de Pygame

Pygame est une bibliothèque qui facilite le dévelopement de jeux. Cette bibliothèque est basée sur SDL (Simple DirectMedia Layer):
Références:

   * \url{https://www.pygame.org/}
   * \url{https://fr.wikipedia.org/wiki/Simple\_DirectMedia\_Layer}
**Apparemment Pygame est installé par défaut sur la Raspberry Pi avec Raspbian.**

Autrement, installation de Pygame (pour Python 3) et de ses dépendances, compilation à partir des sources:
*$ sudo apt-get install mercurial python3-dev python3-numpy libav-tools \
*    libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsmpeg-dev \
*    libsdl1.2-dev  libportmidi-dev libswscale-dev libavformat-dev libavcodec-dev
*$ hg clone \url{https://bitbucket.org/pygame/pygame}
*$ cd pygame
*$ python3 setup.py build
*$ sudo python3 setup.py install

Test avec les exemples qui se trouvent dans le répertoire 'example' de pygame:
*$ python3 -m pygame.examples.aliens

Références:

   * \url{http://pygametutorials.wikidot.com/tutorials-basic}
   * \url{https://www.pygame.org/docs/}
   * \url{http://kidscancode.org/lessons/}

###Utilisation de Glade

Glade est un environment de création d'interface graphique basé sur la bibliothèque GTK.
Références:

   * \url{https://fr.wikipedia.org/wiki/Glade}
   * \url{https://glade.gnome.org/}
Installation de l'outil de conception Glade sur Raspberry Pi (ou sur n'importe quel ordinateur):
*$ sudo apt install glade

Démarrer l'application (à partir du menu ou en tapant dans une console '**glade**').

Créer un fichier 'test.glade' contenant:
*<?xml version="1.0" encoding="UTF-8"?>
*<interface>
*  <!-- interface-requires gtk+ 3.0 -->
*  <object class="GtkWindow" id="window1">
*    <property name="can\_focus">False</property>
*    <signal name="destroy" handler="onDestroy" swapped="no"/>
*    <child>
*      <object class="GtkButton" id="button1">
*        <property name="label" translatable="yes">button</property>
*        <property name="use\_action\_appearance">False</property>
*        <property name="visible">True</property>
*        <property name="can\_focus">True</property>
*        <property name="receives\_default">True</property>
*        <property name="use\_action\_appearance">False</property>
*        <signal name="pressed" handler="onButtonPressed" swapped="no"/>
*      </object>
*    </child>
*  </object>
*</interface>

Vous pouvez aussi charger ce fichier dans l'environnement de conception Glade.

Ensuite créer un fichier Python 'test.py' qui va lire et afficher le contenu du fichier glade et aussi connecter les signaux
des éléments de l'interface vers les méthodes Python du programme (par exemple: l'appui sur un bouton, affiche un message dans la console):
*import gi
*gi.require\_version('Gtk', '3.0')
*from gi.repository import Gtk
*
*class Handler:
*    def onDestroy(self, *args):
*        Gtk.main\_quit()
*
*# prise en compte de l'appui sur le bouton **button1**
*    def onButtonPressed(self, button):
*        print("Hello World!")
*
*builder = Gtk.Builder()
*builder.add\_from\_file("test.glade")
*# connecte les méthodes qui se trouvent dans la classe Handler avec les mêmes noms qui se trouvent dans le fichier glade
*builder.connect\_signals(Handler())
*
*window = builder.get\_object("window1")
*window.show\_all()
*
*Gtk.main() # lancement de la boucle principale 

Références:

   * \url{https://openclassrooms.com/courses/pygtk/glade}
   * \url{https://zestedesavoir.com/tutoriels/870/des-interfaces-graphiques-en-python-et-gtk/1456\_utilisation-avancee/5778\_prise-en-main-de-glade/}
   * \url{http://python-gtk-3-tutorial.readthedocs.io/en/latest/builder.html}

## Samedi 28 avril 2018

Session:

   * Réseaux sans fil: Wifi
   * Atelier
       * Mise en oeuvre Wifi, en mode Point d'accès
###Mise en oeuvre Wifi, en mode Point d'accès
Références:

   * \url{https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md}
   * \url{https://frillip.com/using-your-raspberry-pi-3-as-a-wifi-access-point-with-hostapd/}
Installer les paquets DNSMasq et HostAPD

   * DNSMasq pour gérer le serveur DHCP (attribution des adresses IP aux clients qui se connecteront)
   * HostAPD pour transformer la carte wifi en point d'accès (serveur à l'écoute de clients wifi)
*$ sudo apt-get install dnsmasq hostapd

Arrêter les services pour les configurer avec nos paramètres:
*$ sudo systemctl stop dnsmasq
*$ sudo systemctl stop hostapd

Configuration du serveur DHCP en supprimant la configuration automatique en tant que client DHCP sur l'interface Wifi:
*$ sudo nano /etc/dhcpcd.conf
*# à la fin du fichier ajouter 
*denyinterfaces wlan0

Modification de l'interface Wifi pour définir une adresse IP fixe (pour être serveur sur l'adresse IP 192.168.4.1):
$ sudo nano /etc/network/interfaces
*# dans le fichier
*allow-hotplug wlan0  
*iface wlan0 inet static  
*    address 192.168.4.1
*    netmask 255.255.255.0
*    network 192.168.4.0
*    broadcast 192.168.4.255

Redémarrer le service DHCP pour qu'il ne s'occupe plus de l'interface Wifi wlan0 qui sera géré par nos soins:
*# redémarrer le service
*$ sudo service dhcpcd restart

Réconfiguration de l'interface Wifi wlan0 à laquelle nous avons maintenant attribué une adresse IP fixe: 198.168.4.1:
*# redémarrer l'interface
*$ sudo ifdown wlan0
*$ sudo ifup wlan0

Configuration de notre serveur DHCP d'attribution d'adresses IP pour nos clients Wifi de notre point d'accès:
*# configurer le serveur d'adresse IP
*$ sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig  
*$ sudo nano /etc/dnsmasq.conf
*# dans le fichier
*interface=wlan0
*listen-address=192.168.4.1
*bind-interfaces
*server=8.8.8.8
*domain-needed
*bogus-priv
*dhcp-range=192.168.4.2,192.168.4.20,255.255.255.0,24h

Configuration de notre carte Wifi en point d'accès:
*# configuration du point d'accès
*$ sudo nano /etc/hostapd/hostapd.conf
*# dans le fichier
*interface=wlan0
*driver=nl80211
*ssid=RaspberryPi1
*hw\_mode=g
*channel=7
*wmm\_enabled=1
*macaddr\_acl=0
*auth\_algs=1
*ignore\_broadcast\_ssid=0
*wpa=2
*wpa\_passphrase=maisondulibre
*wpa\_key\_mgmt=WPA-PSK
*wpa\_pairwise=TKIP
*rsn\_pairwise=CCMP

Vérification de la syntaxe et des paramètres de notre fichier de configuration:
*# Test
*$ sudo /usr/sbin/hostapd /etc/hostapd/hostapd.conf

Prise en compte de notre fichier de configuration par l'application hostapd:
*# indiquer le fichier de configuration
*$ sudo nano /etc/default/hostapd
*# dans le fichier, remplacer:
*DAEMON\_CONF="/etc/hostapd/hostapd.conf"

Rédémarrer les services DNMasq et HostAPD:
*# redémarrer les services
*$ sudo systemctl start hostapd
*$ sudo systemctl start dnsmasq

Normalement vous devez à partir d'un smartphone ou d'un autre ordinateur voir le nouveau point d'accès porté par la Raspberry Pi
et pouvoir vous connecter dessus et obtenir une adresse IP, mais vous ne pouvez pas encore utiliser "Internet" car la porté du réseau se 
limite à la Raspberry Pi, vous pouvez installer un serveur Web sur celle-ci et qui sera vu par votre smartphone (en utilisation l'adresse IP
192.168.4.1 dans votre navigateur).
Pour avec accès à "Internet", il faut router notre réseau 192.68.4.1 vers un autre réseau, par exemple le réseau filaire de la Raspberry Pi 
qui sera lui connecté à une autre box pour aller sur Internet.


#Samedi 31 mars 2018

Session:

   * Préparation animation du samedi 7 avril
       * Réseaux sans fil: Wifi
   * Atelier
       * Mise en oeuvre Wifi, en mode Point d'accès
   * 
Note: Normalement la MPT a fait l'acquisition de deux écrans pour notre atelier du samedi, on va pouvoir brancher les Raspberry Pi. 

Transformer la Raspberry Pi en point d'accès Wifi:
*$ sudo apt-get install dnsmasq hostapd
*
*$ sudo systemctl stop dnsmasq
*$ sudo systemctl stop hostapd
*
*# configuration
*$ sudo nano /etc/dhcpcd.conf


#Samedi 24 février 2018

Session:

   * Présentations
       * Fonctionnement Page Web dynamique (suite): base de données
   * Atelier
       * installation de MySQL
Références sur les bases de données:

   * Principes: \url{https://fr.wikipedia.org/wiki/Base\_de\_donn%C3%A9es}
   * La théorie: \url{https://fr.wikipedia.org/wiki/Alg%C3%A8bre\_relationnelle}
   * Le langage utilisé pour les bases de données relationnelles SQL: \url{https://fr.wikipedia.org/wiki/Structured\_Query\_Language}
Installation du serveur de base de données (mariadb)
*$ sudo apt install mariadb-server
Installation de PhpMyAdmin (page web, visualisation et manipulation des bases et des tables stockées sur le serveur mariadb
*$ sudo apt install phpmyadmin
# choisir le mot de passe de l'utilisateur de PhpMyAdmin (login: phpmyadmin)

Ouvrir votre navigateur web sur l'URL: localhost/phpmyadmin
login : phpmyadmin
mot de passe: <mot de passe choisi précédemment>
Explorer les bases et les tables du système mariadb et de PhpMyAdmin

Il n'y a pas de mot de passe pour MariaDB (par défaut), il faut en ajouter un, car ensuite pour installer notre exemple en PHP:
Les commandes pour ajouter un mot de passe à l'utilisateur root de mariadb sont (remplacer 'password' par votre mot de passe, exemple: 'toto'):
*$  sudo mysql --user=root
*> DROP USER 'root'@'localhost';
*> CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';
*> GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost';
*> exit
*$ sudo mysql -u root -ppassword  # votre mot de passe exemple: sudo mysql -u root -ptoto
*> CREATE DATABASE wordpress;
*> exit

# installation de wordpress à la main:
*$ sudo su
*# cd /var/www/html
*# wget \url{http://wordpress.org/latest.tar.gz} # on récupère la dernière version de wordpress
*# tar xvf latest.tar.gz # on déploye l'archive
*# chown -R www-data:www-data wordpress/ # on change les droits (utilisateur et group apache2) sur l'arborescence wordpress 
*# rm latest.tar.gz # on nettoye derrière
*# exit # on sort

Ouvrir votre navigateur web sur l'URL: localhost/wordpress

   * choisir la langue
   * garder la même base: wordpress
   * changer le login: root
   * donner le mot de passe root de mariadb, celui qui a été configuré précédemment
   * cliquer sur l'installation
   * choisir le titre du blog, un login, un mot de passe et ensuite c'est bon, vous pouvez démarrer le blon
   * ceci est un exemple (wordpress/les blogs ont moins la faveur des jeunes)
Pour développer le même type de site, il faut programmer en PHP, créer des modèles HTML/CSS/Javascript qui seront remplis par du contenu stocké dans la base de données. On peut tout faire soi-même à la main, mais le mieux c'est d'utiliser un logiciel (un framework) qui va nous aider à créer les modèles, à gérer le contenu de la base de données suivant les meilleurs principes en vigueur dans la profession (le design pattern est au développeur, ce que le savoir-faire est à l'artisan-boulanger: l'expérience).

Voici quelques frameworks PHP pour développer des sites web dynamiques:

   * Lavarel: \url{https://laravel.com/},
   * Symfony: \url{https://symfony.com/} (qui est aussi utilisé dans d'autres projets)
   * CodeIgniter:\url{https://codeigniter.com/}, 

#Annonces:

   * La MPT et la médiathèque de Landerneau organisent une animation: projet écrans Landerneau
       * le samedi 7 avril toute la journée au Family
       * nous sommes invités sur les animations:
           * pour une install party
           * présentation des RPi de notre atelier
           * ...

   * Animation sur Brest (au 214 rue Jean Jaurès) pendant les vacances scolaires: semaine du lundi 5 mars au 9 mars 
       * les places seront limitées, inscription nécessaire,
       * participation financière (adhésion à la Maison du Libre à 20 euros).

#Samedi 27 janvier 2018
###
Session:

   * Présentations
       * Navigateur web, protocole HTTP
       * Vue d'ensemble: HTML, CSS, Javascript
       * Fonctionnement Page Web dynamique
   * Atelier
       * suite installation du serveur apache 
       * installation de PHP
Installation PHP sur Raspbian stretch (Raspberry Pi 2/3)

   * ouvrir un terminal (une console)
   * $ sudo apt update
   * $ sudo apt upgrade
   * # installation d'apache2 (si ce n'est pas déjà fait)
   * $ sudo apt install apache2
   * # test de l'installation d'apache
   * # nom de la machine locale: **localhost** => adresse IP locale pour la machine locale: 127.0.0.1
   * $ wget localhost # ok => téléchargement de la page HTML de test dans un fichier index.html
   * $ more index.html # pour lire le fichier par page 
   * # installation de PHP
   * $ sudo apt install php
   * # tester l'installation de PHP
   * $ sudo su # passer en mode administrateur pour créer un fichier PHP dans le répertoire où pointe apache pour servir les fichiers
   * # echo "<?php phpinfo(); ?>" > /var/www/html/index.php
   * # # exit pour quitter le mode administrateur (root)
   * $ wget localhost/index.php # ou navigateur web
   * $ more index.php # résultat HTML de la fonction PHP: phpinfo()
Vous pouvez modifier le fichier index.php pour tester des commandes PHP, exemple sur: \url{http://php.net/manual/fr/tutorial.firstpage.php}
*<html>
* <head>
*  <title>Test PHP</title>
* </head>
* <body>
* <?php echo '<p>Bonjour le monde</p>'; ?>
* </body>
*</html>

Attention: on n'a pas encore installé de base de données (tous les exemples ne fonctionneront pas).

Références:

   * MOOC: Introduction à HTML5 - Animations et jeux \url{https://www.fun-mooc.fr/courses/course-v1:groupeinsa+13001S05+session05/about}
   * Utiliser HTML5 et CSS3: \url{https://openclassrooms.com/courses/apprenez-a-creer-votre-site-web-avec-html5-et-css3}
   * MOOC: Supervision de Réseaux et Services: \url{https://www.fun-mooc.fr/courses/course-v1:lorraine+30008+session01/info} pas adapté (sauf Nagios ...)
   * MOOC: Réseaux Locaux: \url{https://www.fun-mooc.fr/courses/course-v1:univ-toulouse+101008+session01/info}
   * Cours PHP: 
       * \url{https://openclassrooms.com/courses/concevez-votre-site-web-avec-php-et-mysql} ( parties 1, 2 et 3)
       * \url{https://openclassrooms.com/courses/programmez-en-oriente-objet-en-php} (parties 1 et 2)
Jeu HTML 5 (en anglais):

   * Le dernier tuto de la série: \url{https://www.ibm.com/developerworks/library/wa-html5-game10/index.html} qui contient le lien vers le jeu (le plus jouable): \url{http://www.ibm.com/developerworks/apps/download/index.jsp?contentid=938007\&filename=wa-html5-game10-code.zip\&method=http\&locale=}
Liens Divers:

   * La dure vie des bibliothèques/framework Javascript: \url{https://stackoverflow.blog/2018/01/11/brutal-lifecycle-javascript-frameworks/}
   * Jeux d'instructions de CPU (ISA: \url{https://fr.wikipedia.org/wiki/Jeu\_d%27instructions)}:
       * CISC: \url{https://fr.wikipedia.org/wiki/Complex\_instruction\_set\_computing}
           * ce jeux d'instructions est ensuite décomposé en instructions élémentaires (programme de fonctionnement du CPU: \url{http://www.commentcamarche.net/contents/763-processeur}, \url{http://www.ybet.be/hard1ch7/hard1\_ch7.php}, \url{https://www.iro.umontreal.ca/~monnier/1215/notes-cpumem2.pdf)}: 
               * microcode: \url{https://fr.wikipedia.org/wiki/Microprogrammation}
               * video: \url{https://www.youtube.com/watch?v=6-NFcC8yOXo}
               * Slide: \url{https://ecc2017.coreboot.org/uploads/talk/presentation/38/Microcode.pdf}
               * Status du Microcode CPU intel sous linux: \url{https://www.cyberciti.biz/faq/install-update-intel-microcode-firmware-linux/}
       * RISC: \url{https://fr.wikipedia.org/wiki/Reduced\_instruction\_set\_computing}
   * Article sur l'étude des informaticiens (2018 Developer Skills Report): \url{https://research.hackerrank.com/developer-skills/2018/}
   * Hacker un PC (How to Hack a Turned-off Computer, or Running Unsigned Code in Intel ME): \url{http://blog.ptsecurity.com/2018/01/running-unsigned-code-in-intel-me.html}
   * Une mauvaise bibliothèque (I’m harvesting credit card numbers and passwords from your site. Here’s how.): \url{https://hackernoon.com/im-harvesting-credit-card-numbers-and-passwords-from-your-site-here-s-how-9a8cb347c5b5} Note de l'auteur: "The following is a true story. Or maybe it’s just based on a true story. Perhaps it’s not true at all." ça ne rassure pas ...
   * Humour: \url{https://xkcd.com/} et les explications: \url{http://www.explainxkcd.com/wiki/index.php/Main\_Page}

#Lundi 01 janvier 2018

Bonne année à tous !
Et Merci à notre Maître Jedi (ou Maître Rpi plutôt) pour les enseignements de 2017... Vivement ceux de 2018 !


MOOC: cours en ligne en français:

   * Les Réseaux Locaux:  \url{https://www.fun-mooc.fr/courses/course-v1:univ-toulouse+101008+session01/about} démarre le 8 janvier
   * Maîtriser le shell Bash: \url{https://www.fun-mooc.fr/courses/course-v1:univ-reunion+128001+session01/about} démarre le 5 février
   * L'essentiel pour maîtriser Linux: \url{https://www.fun-mooc.fr/courses/ucarthage/115001/session01/about} démarre le 2 mars
Ça  fait un calendrier bien rempli, l'inscription et les cours sont gratuits, même si vous ne suivez pas le cours, l'inscription au cours permet d'avoir accès aux ressources du cours (pour les consulter plus tard quand vous aurez le temps)

**Attention**: un MOOC prend du temps.
**Attention 2**: les notions de commandes Linux et de shell Bash sont différentes (dans le MOOC "Maîtriser le shell Bash", vous apprendrez quelques commandes Linux, mais vous allez surtout apprendre à programmer avec le shell Bash, ce qui est très intéressant aussi).

Pour les commande Linux, vous pouvez consulter par exemple:

   * \url{http://juliend.github.io/linux-cheatsheet/}Note: dans un moteur de recherche Web, taper: "commandes linux" pour trouver des tutoriels, et si vous avez des questions sur certaines commandes, vous pouvez les poster sur ce "pad".


#samedi 30 décembre 2017

###Session (spéciale, dans une salle au rez-de-chaussée, accès: derrière le bâtiment):

   * Atelier
       * Mise en œuvre pratique de la Raspberry Pi
           * prévoir la Raspberry Pi, l'alimentation et la carte SD (installer la raspbian sur la carte SD \url{https://www.raspberrypi.org/downloads/raspbian/}, autrement on le fera sur place)
           * j'apporte l'écran, clavier/souris

#samedi 25 novembre 2017

###Session:

   * Présentations
       * serveur web, protocole HTTP
       * HTML
   * Atelier
       * installation du serveur 
       * pages web#
#
#Note Jo

###Acces distant à SSH sous windows : ça fonctionne bien. Quelques notes de rappel d’après les explications de Christian lors de la dernière session  :

   * Raspbian sur SD : j'ai utilisé un petit utilitaire qui s'appelle Etcher
   * Sur PC dans explorateur sur la carte SD, création d'un fichier ssh
   * SD sur RPB
   * Connection au réseau par câble
   * Démarrer le RPB
   * Adresse IP allouée : aller sur la page de la box (chez Free : \url{http://mafreebox.freebox.fr/} puiis sur Paramétres de la Frrebox/Mode avancé/Réseau local/Dhcp)
   * Installer Putty, Puis ouvrir (Dans progammes dossier Putty programme Puttty)
   * Configurer l'adresse IP, connection type SSH, Open
   * La console s'ouvre. Se connecter en tant que pi mdp par défaut raspberry
   * 
###Se connecter en Wifi

   * Pour Paramétrer la wifi en mode console, se reporter au lien \url{https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md}. Ca marche très bien en utilisant wpa\_passphrase mais c'est en anglais
   * Ne pas oublier de virer le mot de passe en commentaire dans le fichier wpa\_supplicant et de sauvegarder la configuration
   * Débrancher le câble réseau et redémarrer.
   * Redémarrer une session Putty avec nouvelle adresse allouée au RPB (Attention, comme c'est en wifi, ça ne sera pas la même adresse.
###Acceder par VNC

   * Un toto bien fait ,et en plus en français (ça rime!).  \url{http://www.framboise314.fr/prenez-la-main-a-distance-sur-votre-raspberry-pi-avec-vnc/#Installer\_le\_serveur\_VNC\_sur\_le\_Raspberry\_Pi}
   * Il suffit de suivre les instructions du tuto, et vous avez accès a votre RPB en mode X (environnement graphique). Bien pratique pour moi qui n'ai pas de moniteur HDMI.
Bon dimanche à tous




##samedi 28 octobre 2017

###Session:

   * Mise en place du matériel
   * Présentations
       * système d'exploitation (linux)
       * réseau IPv4
   * Atelier
       * configuration Raspberry Pi
       * démarrage
       * accès distant SSH à jula carte (sans écran/clavier)
###Références:

   * OS: \url{https://fr.wikipedia.org/wiki/Syst%C3%A8me\_d%27exploitation}
   * Réseau informatique: \url{https://fr.wikipedia.org/wiki/R%C3%A9seau\_informatique}
   * TCP-IP: \url{https://fr.wikipedia.org/wiki/Suite\_des\_protocoles\_Internet}
##samedi 30 septembre 2017

###Session:

   * tour de table
   * présentation du matériel et des logiciels nécessaires
       * Matériel:
           * carte Raspberry Pi: sur kubii.fr
           * alimentation 5v, >= 2.5 A (peut aussi fonctionner avec moins suivant l'usage: à partir de 500mA (mais recommandé au minimum 2.0 A) 
           * boîtier pour protéger la carte Raspberry Pi: \url{https://www.kubii.fr/fr/21-boitiers-raspberry-pi}
           * carte mémoire, micro SD (avec adaptateur): exemple: \url{http://multimedia.e-leclerc.com/univers+multimedia/catalogue/produit/carte-m%C3%A9moire,24664/}, prévoir une carte mémoire de secours, vérifier la compatibilité de la carte mémoire avec la Raspberry Pi sur: \url{https://elinux.org/RPi\_SD\_cards}
           * clavier USB (ou sans fil), ou un clavier qui fait les deux: \url{https://www.kubii.fr/fr/peripheriques-usb-rapsberry-pi/671-mini-clavier-rii-mini-i8-azerty-6952917708002.html}
           * souris USB (ou sans fil)
       * logiciels
           *  \url{https://www.raspberrypi.org/}, dans "Downloads": \url{https://www.raspberrypi.org/downloads/}, récupérer une image, pour les tests avec VirtualBox pour cette session, récupérer la **Raspberry Pi Desktop**: \url{https://www.raspberrypi.org/downloads/raspberry-pi-desktop/}
           * \url{https://www.virtualbox.org/} logiciel de gestion de machine virtuelle (pour les besoins de cette session)
           * prochaine session, installation de logiciel pour installer la Raspbian sur la carte Micro SD
   * présentation de la carte Raspberry Pi
       * SoC: puce principale de la carte contient le CPU, la carte graphique (GPU), la RAM
       * USB: pour connecter, clavier, souris, disque dur, clé USB, webcam, carte son externe, dongle Wifi et bluetooth
       * GPIO (broches): entrées et sorties numériques (pas d'entrée analogique)
       * emplacement pour la carte micro SD
   * présentation des distributions (GNU/Linux ou autres) disponibles pour RPi
       * NOOBS: distribution permettant d'installer d'autres distributions
       * Raspbian: distribution Debian adaptée pour Raspberry Pi
       * autres distributions: Kali, Ubuntu, LibreElec (pour Kodi)
   * présentation de la raspbian (documentation debian)
       * avec une interface graphique
       * ou sans: utilisation d'un terminal avec un shell (bash)
       * gestion des logiciels de la raspbian (Debian)
           * les logiciels sont disponibles sous forme de paquet (paquet Debian, fichiers avec un suffixe .deb) pour l'ensemble de la distribution
           * un paquet est un ou plusieurs programmes (binaires ou sources) encapsulés avec sa configuration et sa documentation dans un fichier
           * la gestion de ces paquets se fait de préférence avec les commande APT,
               * les commandes principales pour débuter:
                   * $ sudo apt update # permet de mettre à jour mes références locales par rapport à celle d'un serveur distant qui contient la liste des paquets Debian les plus récents
                   * $ sudo apt upgrade # mettre à jour tous mes logiciels installés par rapport au résultat de la commande précédente (noyau linux, firefox, python...)
                   * $ sudo apt install <nom du paquet logiciel> # permet d'installer un logiciel qui existe sur le serveur distant mais pas encore présent et utilisable sur mon ordinateur, exemple: sudo apt install minetest # ersatz de minecraft
               * **voici tous les paquets (logiciels) disponibles pour la Debian (par catégories):** \url{https://packages.debian.org/stable/}
                   * ne pas essayer de tout installer (il n'y aura pas assez de place sur la partition)

   * mise en pratique sur VirtualBox (comportement proche d'un Raspberry Pi)
       * télécharger et installer VirtualBox
       * après avoir télécharger la **Raspberry Pi Desktop**
       * démarrer le logiciel VirtualBox
           * cliquer sur l'icône "nouvelle"
           * Nom: Raspbian
           * Type: Linux
           * Version: debian/64
           * suivant
           * Taille mémoire: 1024 Mo (dans les conditions du réel)
           * suivant
           * "créer un disque dur virtuel maintenant"
           * Créer
           * "VDI"
           * suivant
           * "Dynamiquement alloué"
           * suivant
           * Nom du fichier qui simule le disque: Raspbian
           * Taille: 16 Go (comme la carte Micro SD)
           * Créer
           * Sélectionner la machine "Raspbian"
           * Cliquer sur **Stockage** (au milieu dans la configuration de la machine)
               * Cliquer sur **Vide** et complètement à droite cliquer sur l'icône qui représente un CDROM
               * pour afficher le menu "Choisissez un fichier de disque optique virtuel"
               * dans la liste de fichier, retrouver et sélectionner l'image ISO: **2017-06-22-rpd-x86-jessie.iso**
               * valider (ok)
           * Démarrer la machine virtuelle Raspbian (cliquer sur Démarrer)
           * Pour installer, sélectionner le menu "Install"
           * Sélectionner la langue: French
           * Partitionnement: "Entire Disk"
           * Confirmation (menu suivant: touche "entrée")
           * Choisir "All files in one partition"
           * "Finish"
           * Confirmer, choisir "Yes"
           * "Install Grub on Master Boot" => "Yes"
           * Choisir "/dev/sda"
           * "Installation Finish" => Continue
       * Reboot automatique
       * Démarrage Desktop Pi PC
           * L'interface graphique est la même que celle obtenue sur Raspberry Pi avec le réseau qui marche (en passant pas la machine locale)
           * Le clavier fonctionne en AZERTY, mais le reste n'est pas configuré:
               * Dans le menu (en forme de Framboise), sélectionner "Preferences" puis "Raspberry Pi Configuration"
               * Sélectionner l'onglet "Localisation"
               * Changer "Locale/Language": fr (french)
               * Changer "Locale/Country": FR (France)
               * Changer TimeZone / Area: Europe
               * Changer TimeZone / Location: Paris (laisser la souris sur le bas de la liste pour faire défiler)
               * Changer Keyboard : France / French
               * Change Wifi Country: FR (France)
           * Ok puis un redémarrage est nécessaire pour prendre en compte les modifications

           * Pour arrêter la machine virtuelle: menu "Framboise" / "Shutdown" / "Shutdown"

   * présentation de la séquence de démarrage de la raspberry pi
       * la carte micro SD contient deux partitions pour la Raspbian:
           * une partition FAT 32 qui contient les programmes pour démarrer et configurer la Raspberry Pi (fichier de configuration), le noyau linux et son fichier de configuration
           * une partition EXT4 qui contient le système de fichier de la Raspbian (et tous les logiciels)
       * le GPU va lire les programmes (microcode...) pour se configurer et charger le noyau linux en RAM
       * le GPU donne la main au CPU pour démarrer le noyau linux et sa configuration (paramètres, comme l'endroit où se trouve le système de fichier)
       * les applications en mode terminal ou graphique sont lancés
       * **Important**: pour arrêter la carte (pas de bouton on/off), il faut arrê$ fswebcam --no-banner -r 640x480 image.jpgter correctement le système linux, soit en cliquant sur "éteindre" en mode graphique, soit en tapant "shutdown -h now" ou "halt" en ligne de commande
###Références:

   * site raspberry pi:  \url{https://www.raspberrypi.org/}
   * debian manuel: \url{https://debian-handbook.info/get/now/},
   * commande Debian, APT \url{https://www.debian.org/doc/manuals/refcard/refcard}
   *  carte mémoire: 
       * \url{http://www.framboise314.fr/ne-negligez-pas-la-qualite-de-la-carte-sd-de-votre-raspberry-pi/}
       * \url{http://www.raspberrypi-france.fr/cartes-sd-raspberry-pi/}
   * matériel pour RPi:
       * \url{https://raspbian-france.fr/acheter-raspberry-pi-3-accessoires/}
   * Bash: \url{https://openclassrooms.com/courses/reprenez-le-controle-a-l-aide-de-linux/introduction-aux-scripts-shell}
   * Kodi: \url{https://fr.wikipedia.org/wiki/Kodi\_(logiciel)}
   * Initiations sur internet:
       * \url{https://openclassrooms.com/}
       * \url{https://www.fun-mooc.fr/} (en informatique: \url{https://www.fun-mooc.fr/cours/#filter/subject/informatique?page=1\&rpp=50)}
       * \url{https://fr.coursera.org/} (en anglais)
