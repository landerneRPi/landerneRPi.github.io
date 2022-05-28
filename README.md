# MPT Landerneau: Atelier Raspberry Pi

## **Saison 2021/2022**



[2022](2022/README.md)



## Mardi 14 décembre

Dernière séance de l'année.

On se retrouvera le mardi 11 janvier 2022, d'ici là, bonnes fêtes de fin d'année.

Animation de 18h à 20h à la MPT.

En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.
Au programme:

   * Jeu en Python avec PyGame (**space\_invaders.py)**


**Gestion du jeu:**

-----------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.20

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    # afficher du texte sur l'ecran

    def afficherEcran(screen, message):

        pygame.font.init()

        font = pygame.font.SysFont('Arial', 60)

        textsurface = font.render(message, False, (44, 0, 62))

        text\_rect = textsurface.get\_rect(center=(640/2, 480/2))

        screen.blit(textsurface, text\_rect)

    # fin de la méthode

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    # game over, figer le jeu

    perdu = False

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # afficherEcran(screen, "Le jeu des aliens")

        # vérifier si il reste encore des aliens

        if len(aliens) == 0:

            # le tableau des aliens est vide

            afficherEcran(screen, "Victoire sur les aliens")

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

            # vérification de collision avec les rockets

            for chaqueRocket in rockets:

                if (chaqueRocket.x < chaqueAlien.x + 30 and

                    chaqueRocket.x > chaqueAlien.x and

                    chaqueRocket.y < chaqueAlien.y + 30 and 

                    chaqueRocket.y > chaqueAlien.y - 30):

                    # enter en collision

                    # enlever l'alien

                    aliens.remove(chaqueAlien)

                    # enlever la rocket

                    rockets.remove(chaqueRocket)

            # vérifier qu'un Alien est arrivé au niveau du vaisseau

            if (chaqueAlien.y + 30) > space\_y:

                afficherEcran(screen, "Game Over!")

                # j'ai perdu

                perdu = True

    

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        if not perdu:

            dessiner\_vaisseau(screen, space\_x, space\_y)

            for chaqueRocket in rockets:

                chaqueRocket.draw()

                if chaqueRocket.y >= 0:

                    nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

----------



Références;

   * [https://www.pygame.org/news](https://www.pygame.org/news)
   * [https://www.pygame.org/wiki/GettingStarted](https://www.pygame.org/wiki/GettingStarted)
   * [https://htmlcolorcodes.com/fr/](https://htmlcolorcodes.com/fr/)




## Samedi 27 novembre

Animation de 10h à 12h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.



Au programme:

   * Jeu en Python avec GuiZero
       * Création du canvas




# Fichier tictactoe.py

# Imports ---------------

from guizero import App, Box, PushButton, Text, MenuBar





# Functions -------------

def clear\_board():

    new\_board = [[None, None, None], [None, None, None], [None, None, None]]

    for x in range(3):

        for y in range(3):

            button = PushButton(board, text="", grid=[x, y], width=3, command=choose\_square, args=[x,y])

            new\_board[x][y] = button

    return new\_board



def choose\_square(x, y):

    board\_squares[x][y].text = turn

    board\_squares[x][y].disable()

    toggle\_player()

    check\_win()



def toggle\_player():

    global turn

    if turn == "X":

        turn = "O"

    else:

        turn = "X"

    message.value = "It is your turn, " + turn



def check\_win():

    winner = None



    # Vertical lines

    if (

        board\_squares[0][0].text == board\_squares[0][1].text == board\_squares[0][2].text

    ) and board\_squares[0][2].text in ["X", "O"]:

        winner = board\_squares[0][0]

    elif (

        board\_squares[1][0].text == board\_squares[1][1].text == board\_squares[1][2].text

    ) and board\_squares[1][2].text in ["X", "O"]:

        winner = board\_squares[1][0]

    elif (

        board\_squares[2][0].text == board\_squares[2][1].text == board\_squares[2][2].text

    ) and board\_squares[2][2].text in ["X", "O"]:

        winner = board\_squares[2][0]



    # Horizontal lines

    elif (

        board\_squares[0][0].text == board\_squares[1][0].text == board\_squares[2][0].text

    ) and board\_squares[2][0].text in ["X", "O"]:

        winner = board\_squares[0][0]

    elif (

        board\_squares[0][1].text == board\_squares[1][1].text == board\_squares[2][1].text

    ) and board\_squares[2][1].text in ["X", "O"]:

        winner = board\_squares[0][1]

    elif (

        board\_squares[0][2].text == board\_squares[1][2].text == board\_squares[2][2].text

    ) and board\_squares[2][2].text in ["X", "O"]:

        winner = board\_squares[0][2]



    # Diagonals

    elif (

        board\_squares[0][0].text == board\_squares[1][1].text == board\_squares[2][2].text

    ) and board\_squares[2][2].text in ["X", "O"]:

        winner = board\_squares[0][0]

    elif (

        board\_squares[2][0].text == board\_squares[1][1].text == board\_squares[0][2].text

    ) and board\_squares[0][2].text in ["X", "O"]:

        winner = board\_squares[0][2]

        

    if winner is not None:

        message.value = winner.text + " wins!"

    elif moves\_taken() == 9:

        message.value = "It's a draw"



def moves\_taken():

    moves = 0

    for row in board\_squares:

        for col in row:

            if col.text == "X" or col.text == "O":

                moves = moves + 1

    return moves



# rejouer

def rejouer():

    global board\_squares, turn, message

    board\_squares = clear\_board()

    turn = "X"

    message.value = "New Game: It is your turn, " + turn



# quitter

def quitter():

    global app

    app.destroy()



# Variables -------------

turn = "X"



# App -------------------

app = App("Tic tac toe")



menu\_bar = MenuBar(app,

                  toplevel=["File"],

                  options=[

                      [ ["File Rejouer", rejouer], ["Quitter", quitter]],

                    ])

board = Box(app, layout="grid")

board\_squares = clear\_board()

message = Text(app, text="It is your turn, " + turn)



app.display()

# fin de Fichier tictactoe.py



######################################

########################################################################################################################################################

##################################################################################################################



##################################################################################################################







    # Fichier tictactoe.py

    # Imports ---------------

    from guizero import App, Box, PushButton, Text

   * 

    # Functions -------------

    def clear\_board():

        new\_board = [[None, None, None], [None, None, None], [None, None, None]]

        for x in range(3):

            for y in range(3):

                button = PushButton(board, text="", grid=[x, y], width=3, command=choose\_square, args=[x,y])

                new\_board[x][y] = button

        return new\_board

    

    def choose\_square(x, y):

        board\_squares[x][y].text = turn

        board\_squares[x][y].disable()

        toggle\_player()

        check\_win()

    

    def toggle\_player():

        global turn

        if turn == "X":

            turn = "O"

        else:

            turn = "X"

        message.value = "It is your turn, " + turn

    

    def check\_win():

        winner = None

    

        # Vertical lines

        if (

            board\_squares[0][0].text == board\_squares[0][1].text == board\_squares[0][2].text

        ) and board\_squares[0][2].text in ["X", "O"]:

            winner = board\_squares[0][0]

        elif (

            board\_squares[1][0].text == board\_squares[1][1].text == board\_squares[1][2].text

        ) and board\_squares[1][2].text in ["X", "O"]:

            winner = board\_squares[1][0]

        elif (

            board\_squares[2][0].text == board\_squares[2][1].text == board\_squares[2][2].text

        ) and board\_squares[2][2].text in ["X", "O"]:

            winner = board\_squares[2][0]

    

        # Horizontal lines

        elif (

            board\_squares[0][0].text == board\_squares[1][0].text == board\_squares[2][0].text

        ) and board\_squares[2][0].text in ["X", "O"]:

            winner = board\_squares[0][0]

        elif (

            board\_squares[0][1].text == board\_squares[1][1].text == board\_squares[2][1].text

        ) and board\_squares[2][1].text in ["X", "O"]:

            winner = board\_squares[0][1]

        elif (

            board\_squares[0][2].text == board\_squares[1][2].text == board\_squares[2][2].text

        ) and board\_squares[2][2].text in ["X", "O"]:

            winner = board\_squares[0][2]

    

        # Diagonals

        elif (

            board\_squares[0][0].text == board\_squares[1][1].text == board\_squares[2][2].text

        ) and board\_squares[2][2].text in ["X", "O"]:

            winner = board\_squares[0][0]

        elif (

            board\_squares[2][0].text == board\_squares[1][1].text == board\_squares[0][2].text

        ) and board\_squares[0][2].text in ["X", "O"]:

            winner = board\_squares[0][2]

            

        if winner is not None:

            message.value = winner.text + " wins!"

        elif moves\_taken() == 9:

            message.value = "It's a draw"

    

    def moves\_taken():

        moves = 0

        for row in board\_squares:

            for col in row:

                if col.text == "X" or col.text == "O":

                    moves = moves + 1

        return moves

    

            

    # Variables -------------

    turn = "X"

    

    # App -------------------

    app = App("Tic tac toe")

    

    board = Box(app, layout="grid")

    board\_squares = clear\_board()

    message = Text(app, text="It is your turn, " + turn)

    

    app.display()

    # fin de Fichier tictactoe.py



Références;

   * [https://lawsie.github.io/guizero/](https://lawsie.github.io/guizero/)




## Mardi 9 novembre

Animation de 18h à 20h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.



Au programme:

   * Outils de configuration de la Raspberry Pi (le réseau)
   * Jeu en Python avec GuiZero
       * Création de la fenêtre et des Widgets de base


Références;

   * [https://lawsie.github.io/guizero/](https://lawsie.github.io/guizero/)
   * [https://thonny.org/](https://thonny.org/)   éditeur Python pour débutant


## Samedi 23 octobre

Animation de 10h à 12h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.



Au programme:

   * Outils de configuration de la Raspberry Pi (le réseau)
   * Algorithme avec AlgoBox (suite)
       * Implémentation en Scratch et Python




## Mardi 12 octobre

Animation de 18h à 20h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour tous.



Annonce: Install Partly le mardi 19 octobre de 18h à 20h au Fablab Elorn (sur inscription) au Lycée de l'Elorn



Au programme:

   * Algorithme avec AlgoBox
   * Implémentation en Scratch et Python


Références:

   * AlgoBox: [https://www.xm1math.net/algobox/](https://www.xm1math.net/algobox/)
   * Scratch: [https://scratch.mit.edu/](https://scratch.mit.edu/)
       * Blender.org: [https://www.blender.org/](https://www.blender.org/)
   * Make Human: [http://www.makehumancommunity.org/content/plugins.html](http://www.makehumancommunity.org/content/plugins.html)
   * Emulateur Android: [http://www.makehumancommunity.org/content/plugins.html](http://www.makehumancommunity.org/content/plugins.html)








## Samedi 25 septembre

Animation de 10h à 12h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.



[https://www.raspberrypi.org/](https://www.raspberrypi.org/)

[https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit](https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit)



[https://www.raspberrypi.org/books-magazines/](https://www.raspberrypi.org/books-magazines/)

[https://magpi.raspberrypi.org/books](https://magpi.raspberrypi.org/books)



Installation RaspberryPi Os sur carte SD:

   * installation de rpi-imager: outil pour écrire l'image RaspberryPi OS sur une carte SD: [https://www.raspberrypi.org/software/](https://www.raspberrypi.org/software/)
   * utilisation de rpi-imager pour écrire l'image: [https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit](https://www.raspberrypi.org/software/operating-systems/#raspberry-pi-os-32-bit)


Algorithme avec Algobox:

   * installation de Algobox:
    $ sudo apt update

    $ sudo apt upgrade

    $ sudo apt install algobox





## Mardi 14 septembre

Animation de 18h à 20h à la MPT.



En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.



   * Tour de table
   * Présentation Raspberry Pi
       * Carte: 3B, 3B+, 4B: [https://fr.wikipedia.org/wiki/Raspberry\_Pi](https://fr.wikipedia.org/wiki/Raspberry\_Pi)
       * Alimentation: [https://www.raspberrypi-france.fr/guide/accessoires-raspberry-pi/](https://www.raspberrypi-france.fr/guide/accessoires-raspberry-pi/)
       * Câble HDMI: [https://fr.wikipedia.org/wiki/High-Definition\_Multimedia\_Interface#Types\_de\_connecteurs](https://fr.wikipedia.org/wiki/High-Definition\_Multimedia\_Interface#Types\_de\_connecteurs)
       * Boîtier: pour protéger
       * Carte SD: 16 Go minimum (en prendre 2 au cas où une des deux tombe en panne)
   * Le système binaire:
       * Base 2
       * Algèbre de Boole: [https://fr.wikipedia.org/wiki/Alg%C3%A8bre\_de\_Boole\_(logique)](https://fr.wikipedia.org/wiki/Alg%C3%A8bre\_de\_Boole\_(logique))
       * Mise en oeuvre en utilisant Logisim (à continuer à la prochaine séance)
       * Fonctions logiques: [https://fr.wikipedia.org/wiki/Fonction\_logique](https://fr.wikipedia.org/wiki/Fonction\_logique)
           * ET
           * OU
           * NON
   * Architecture des ordinateurs
       * [https://fr.wikipedia.org/wiki/Architecture\_mat%C3%A9rielle](https://fr.wikipedia.org/wiki/Architecture\_mat%C3%A9rielle)
       * Von Neumann: [https://fr.wikipedia.org/wiki/Architecture\_de\_von\_Neumann](https://fr.wikipedia.org/wiki/Architecture\_de\_von\_Neumann)
       * Harvard: [https://fr.wikipedia.org/wiki/Architecture\_de\_type\_Harvard](https://fr.wikipedia.org/wiki/Architecture\_de\_type\_Harvard)
   * Installation de Logisim
       * Mise à jour du système: [https://fr.wikipedia.org/wiki/Raspberry\_Pi\_OS](https://fr.wikipedia.org/wiki/Raspberry\_Pi\_OS)
           * dans un terminal:
    $ sudo apt update

    $ sudo apt upgrade

# touche <entrée>

    $ sudo apt install logisim

# touche <entrée>



Référence:

   * Communauté française: [https://raspberry-pi.fr/](https://raspberry-pi.fr/)
   * Site officiel: [https://www.raspberrypi.org/](https://www.raspberrypi.org/)
   * Revendeurs Raspberry Pi en ligne:
       * [https://www.kubii.fr/](https://www.kubii.fr/)
       * [https://www.gotronic.fr/](https://www.gotronic.fr/)
   * [https://fr.wikipedia.org/wiki/Pascaline](https://fr.wikipedia.org/wiki/Pascaline)
   * [https://fr.wikipedia.org/wiki/Syst%C3%A8me\_binaire](https://fr.wikipedia.org/wiki/Syst%C3%A8me\_binaire)
   * Logisim: [http://www.cburch.com/logisim/](http://www.cburch.com/logisim/)




## Fin de saison



## **Saison 2020/2021**



# **Lien de la visio:  mdl29.net/visio**



## Samedi 26 juin: pas de séance (tour de France)

EXcusez moi, j'ai bouffé la consigne pour mardi dernier. J'étais persuadé que c'était le 29...Et aujourd'hui, pas de séance.!!!Je me suis retrouvé comme un c.. sur le site de visio.

A+ tous



Jo



## Mardi 22 juin en présentiel

Animation de 18h à 20h à la MPT.



[https://github.com/landerneRPi](https://github.com/landerneRPi)



Bilan de l'année et perspectives



Dernière séance



## Samedi 19 juin (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero (suite): Logique du jeu




    # programme tictactoe.py

     

    # import guizero

    from guizero import App, Box, PushButton, Text

     

    # variables gestion joueur

    joueur1 = "A"

    couleur\_joueur1="red"

    joueur2 = "B"

    couleur\_joueur2="blue"

    # variable du joueur courant

    tour\_joueur = joueur1

    couleur\_joueur\_courant = couleur\_joueur1

    # nombre de coups

    nombre\_coup = 0

    # nombre\_coup = 9

     

    # tableau des boutons

    # tableau\_boutons = [ [btn00, btn10, btn20],

    #                     [btn01, btn11, btn21],

    #                     [btn02, btn12, btn22]

    #                   ]

    tableau\_boutons = [ [None,None,None],

                        [None,None,None],

                        [None,None,None]]

     

    # dessiner la grille

    def dessiner\_grille():

        # grille de 3x3 PushButton

        # création des boutons

        # boucle de 0 à 2 => 3 élements

        for x in range(3):

            # boucle de 0 à 2 => 3 élements

            for y in range(3):

                monBouton = PushButton(grille\_jeu, text=f"N{x}{y}", grid=[x,y], command=selection, args=[x,y])

                tableau\_boutons[x][y] = monBouton

     

    # methodes de selection des boutons

    def reset():

        global tour\_joueur, couleur\_joueur\_courant, nombre\_coup

        tour\_joueur = joueur1

        couleur\_joueur\_courant = couleur\_joueur1

        nombre\_coup = 0

        dessiner\_grille()

        message\_joueur.value = "Au tour du joueur: " + tour\_joueur

     

    # methodes de selection des boutons

    def selection(x, y):

        global tour\_joueur, couleur\_joueur\_courant, nombre\_coup

        # incrementer le nombre de coups

        # nombre\_coup = nombre\_coup + 1

        nombre\_coup += 1

        # nombre\_coup++ : n'existe pas en python

        # nombre\_coup += 1

        

        # selectionne le bouton et le desactiver

        monBouton = tableau\_boutons[x][y]

        monBouton.text = tour\_joueur

        monBouton.bg = couleur\_joueur\_courant

        monBouton.disable()

        # changement de joueur

        if tour\_joueur == joueur1: 

            tour\_joueur = joueur2

            couleur\_joueur\_courant = couleur\_joueur2

        else:

            tour\_joueur = joueur1

            couleur\_joueur\_courant = couleur\_joueur1

     

        # condition gagnant est fausse: Nulle

        gagnant = None

        # vérifier si on a un gagnant

        # vérifier les lignes

        for ligne in range(3):

            if (tableau\_boutons[ligne][0].text == tableau\_boutons[ligne][1].text == tableau\_boutons[ligne][2].text):

                gagnant = tableau\_boutons[ligne][0].text

                break

            # instructions suivantes

        # fin de boucle

        if not gagnant:

            # vérifier les colonnes

            for col in range(3):

                if (tableau\_boutons[0][col].text == tableau\_boutons[1][col].text == tableau\_boutons[2][col].text):

                    gagnant = tableau\_boutons[0][col].text

                    break

            # fin de boucle

            if not gagnant:

                # vérifier les deux diagonales

                if (tableau\_boutons[0][0].text == tableau\_boutons[1][1].text == tableau\_boutons[2][2].text):

                    gagnant = tableau\_boutons[0][0].text

                elif (tableau\_boutons[2][0].text == tableau\_boutons[1][1].text == tableau\_boutons[0][2].text):

                    gagnant = tableau\_boutons[2][0].text

        

        # si gagnant

        if gagnant:

            message\_joueur.value = "Le gagnant est le joueur: " + gagnant

            # désactiver tous les boutons

            for ligne in range(3):

                for col in range(3):

                    tableau\_boutons[ligne][col].disable()

        # vérifier le nombre de coups: 9 => fin de la partie

        elif nombre\_coup == 9:

            message\_joueur.value = "Fin de la partie, match null"

        else :

            # afficher le message pour le joueur suivant

            message\_joueur.value = "Au tour du joueur: " + tour\_joueur

     

    # Application: fenetre principale

     

    app = App("Tic tac toe")

     

    # premiere boite pour afficher l'entete

    entete = Box(app)

    message\_jeu = Text(entete, text="Bienvenue dans Tic Tac Toe")

    # deuxieme boite pour afficher la grille de bouton

    grille\_jeu = Box(app, layout="grid")

    dessiner\_grille()

     

    # troisieme boite pour afficher le tour du joueur

    message\_box = Box(app)

    message\_joueur = Text(message\_box, text="Au tour du joueur: " + tour\_joueur)

    bouton\_reset\_jeu = PushButton(app, text="Nouvelle partie", command=reset)

     

    # affichage de la fenetre et attend les evenements (graphique: souris, clavier)

    app.display() # boucle principale d'attente sur les evenements

     

    # fin du programme tictactoe.py





## Samedi 12 juin (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero (suite): Layout et Grid: création du jeu




    # programme tictactoe.py

    

    # import guizero

    from guizero import App, Box, PushButton, Text

    

    # tableau des boutons

    # tableau\_boutons = [ [btn00, btn10, btn20],

    #                     [btn01, btn11, btn21],

    #                     [btn02, btn12, btn22]

    #                   ]

    tableau\_boutons = [ [None,None,None],

                        [None,None,None],

                        [None,None,None]]

    

    # methodes de selection des boutons

    def selection(x, y):

        # selectionne le bouton et le desactiver

        monBouton = tableau\_boutons[x][y]

        monBouton.text = "B"

        monBouton.bg = "red" 

        monBouton.disable()

    

    # Application: fenetre principale

    

    app = App("Tic tac toe")

    

    # premiere boite pour afficher l'entete

    entete = Box(app)

    message\_jeu = Text(entete, text="Bienvenue dans Tic Tac Toe")

    # deuxieme boite pour afficher la grille de bouton

    grille\_jeu = Box(app, layout="grid")

    # grille de 3x3 PushButton

    # création des boutons

    # boucle de 0 à 2 => 3 élements

    for x in range(3):

        # boucle de 0 à 2 => 3 élements

        for y in range(3):

            monBouton = PushButton(grille\_jeu, text="N", grid=[x,y], command=selection, args=[x,y])

            tableau\_boutons[x][y] = monBouton

    

    # troisieme boite pour afficher le tour du joueur

    message\_box = Box(app)

    message\_joueur = Text(message\_box, text="Au tour du joueur: ")

    

    # affichage de la fenetre et attend les evenements (graphique: souris, clavier)

    app.display() # boucle principale d'attente sur les evenements

    

    # fin du programme tictactoe.py

    





Références:

   * [https://appinventor.mit.edu/](https://appinventor.mit.edu/)
   * [https://kiwibrowser.com/](https://kiwibrowser.com/)
   * [https://fr.wikipedia.org/wiki/Shell\_Unix](https://fr.wikipedia.org/wiki/Shell\_Unix)
   * [https://www.youtube.com/watch?v=LamjAFnybo0]([]https://www.youtube.com/watch?v=LamjAFnybo0[])




## Samedi 5 juin (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero (suite): Layout
   * Initiation HTML/CSS/Javascript
       * éléments de base d'une page HTML (suite)


Références:

   * [https://www.brest.fr/actus-agenda/agenda/agenda-2563/en-ligne-table-ronde-le-code-se-conjugue-au-feminin-1037397.html](https://www.brest.fr/actus-agenda/agenda/agenda-2563/en-ligne-table-ronde-le-code-se-conjugue-au-feminin-1037397.html)
   * [https://zoom.us/j/96355726041?pwd=QUptRUxBQ0p0SWRHSmN5dGxybldPUT09](https://zoom.us/j/96355726041?pwd=QUptRUxBQ0p0SWRHSmN5dGxybldPUT09)
   * [https://www.a-brest.net/article24769.html](https://www.a-brest.net/article24769.html)
   * [https://lawsie.github.io/guizero/layout/](https://lawsie.github.io/guizero/layout/)




Code Jeu du pendu



"""

Created on Tue Mar 24 07:36:15 2020

@author: @Xalava

"""



import random

choix = ["casserole", "cuillere", "patate", "souris"]

solution = random.choice(choix)



solution = "casserole"

tentatives = 7

affichage = ""

lettres\_trouvees = ""



for l in solution:

  affichage = affichage + "\_ "



print(">> Bienvenue dans le pendu <<")



while tentatives > 0:

  print("\nMot à deviner : ", affichage)

  proposition = input("proposez une lettre : ")[0:1].lower()



  if proposition in solution:

      lettres\_trouvees = lettres\_trouvees + proposition

      print("-> Bien vu!")

  else:

    tentatives = tentatives - 1

    print("-> Nope\n")

    if tentatives==0:

        print(" ==========Y= ")

    if tentatives<=1:

        print(" ||/       |  ")

    if tentatives<=2:

        print(" ||        0  ")

    if tentatives<=3:

        print(" ||       /|\ ")

    if tentatives<=4:

        print(" ||       /|  ")

    if tentatives<=5:                    

        print("/||           ")

    if tentatives<=6:

        print("==============\n")



  affichage = ""

  for x in solution:

      if x in lettres\_trouvees:

          affichage += x + " "

      else:

          affichage += "\_ "



  if "\_" not in affichage:

      print(">>> Gagné! <<<")

      break

     

print("\n    * Fin de la partie *    ")





**Supprimer la valeur dans le champ texte**

    # exercice: exo7\_1\_guizero.py

    

    from guizero import App, Text, Picture, TextBox, PushButton

    

    # fonctions pour le push button

    def afficher\_name():

        print("le nom est ", entree.value)

    

    def cliquer\_pelle(tarte, gateau):

        message\_pelle.value = "J'ai cliqué sur la pelle " + tarte

        # désactive le bouton

        button\_image.disable()

    

    # events pour le TextBox

    def effacer\_valeur():

        entree.value = ""

    

    

    # la fenêtre de l'application

    app = App("Mon Application")

    app.bg = "yellow"

    app.width = 800

    app.height = 800

    

    # les widgets

    message = Text(app, text="Bonjour le monde !", color="blue")

    message.text\_size=50

    message.bg = "red"

    

    entree = TextBox(app, text="entrer votre nom",  width=20)

    entree.when\_clicked = effacer\_valeur

    

    # bouton avec méthode callback quand le bouton est appuyé

    button\_nom = PushButton(app, text="afficher le nom", command=afficher\_name)

    button\_nom.bg = "green"

    

    # [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)

    button\_image = PushButton(app, image="pelle.png", width=40, height=40, command=cliquer\_pelle, args=["à tarte", "à gâteau"])

    message\_pelle = Text(app, text="Message de la pelle", width=60)

    

    logo = Picture(app, image="logo\_landerneau.png")

    

    # affichage de la fenêtre

    app.display()

    

    # fin exercice: exo7\_1\_guizero.py







**Gérer la disposition (layout) des widgets dans la fenêtre avec une grille (grid):**

    # exercice: exo8\_guizero.py

    

    from guizero import App, Box, Text, Picture, TextBox, PushButton

    

    # fonctions pour le push button

    def afficher\_name():

        print("le nom est ", entree.value)

    

    def cliquer\_pelle(tarte, gateau):

        message\_pelle.value = "J'ai cliqué sur la pelle " + tarte

        # désactive le bouton

        button\_image.disable()

    

    

    # la fenêtre de l'application

    app = App("Mon Application", height=800, width=1200, layout="grid") # layout: 'grid' ou 'auto'

    app.bg = "yellow"

    

    # les widgets

    message = Text(app, text="Bonjour le monde !", color="blue", grid=[0,0])

    message.text\_size=50

    message.bg = "red"

    

    entree = TextBox(app, text="entrer votre nom",  width=20, grid=[0,1])

    

    # bouton avec méthode callback quand le bouton est appuyé

    button\_nom = PushButton(app, text="afficher le nom", command=afficher\_name, grid=[1,1])

    button\_nom.bg = "green"

    

    # [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)

    button\_image = PushButton(app, image="pelle.png", width=40, height=40,

            command=cliquer\_pelle, args=["à tarte", "à gâteau"],grid=[0,2])

    message\_pelle = Text(app, text="Message de la pelle", width=60, grid=[1,2])

    

    logo = Picture(app, image="logo\_landerneau.png", grid=[0,3])

    

    # affichage de la fenêtre

    app.display()

    

    # fin exercice: exo8\_guizero.py





**Gérer la disposition (layout) des widgets dans la fenêtre avec une grille (fusion de cellules):**

    # exercice: exo8\_1\_guizero.py

    

    from guizero import App, Box, Text, Picture, TextBox, PushButton

    

    # fonctions pour le push button

    def afficher\_name():

        print("le nom est ", entree.value)

    

    def cliquer\_pelle(tarte, gateau):

        message\_pelle.value = "J'ai cliqué sur la pelle " + tarte

        # désactive le bouton

        button\_image.disable()

    

    

    # la fenêtre de l'application

    app = App("Mon Application", height=800, width=1200, layout="grid") # layout: 'grid' ou 'auto'

    app.bg = "yellow"

    

    # les widgets

    message = Text(app, text="Bonjour le monde !", color="blue", grid=[0,0])

    message.text\_size=50

    message.bg = "red"

    

    entree = TextBox(app, text="entrer votre nom",  width=20, grid=[0,1], align="left")

    

    # bouton avec méthode callback quand le bouton est appuyé

    button\_nom = PushButton(app, text="afficher le nom", command=afficher\_name, grid=[1,1], align="right")

    button\_nom.bg = "green"

    

    # [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)

    button\_image = PushButton(app, image="pelle.png", width=40, height=40,

            command=cliquer\_pelle, args=["à tarte", "à gâteau"],grid=[0,2])

    message\_pelle = Text(app, text="Message de la pelle", width=60, grid=[1,2])

    

    logo = Picture(app, image="logo\_landerneau.png", grid=[0,3,2,1])

    

    # affichage de la fenêtre

    app.display()

    

    # fin exercice: exo8\_1\_guizero.py





**Gérer la disposition (layout) des widgets dans la fenêtre avec une grille et une boîte (grid + box):**

    # exercice: exo9\_guizero.py

    

    from guizero import App, Box, Text, Picture, TextBox, PushButton

    

    # fonctions pour le push button

    def afficher\_name():

        print("le nom est ", entree.value)

    

    def cliquer\_pelle(tarte, gateau):

        message\_pelle.value = "J'ai cliqué sur la pelle " + tarte

        # désactive le bouton

        button\_image.disable()

    

    

    # la fenêtre de l'application

    app = App("Mon Application", height=800, width=1000, layout="auto") # layout: 'grid' ou 'auto'

    app.bg = "yellow"

    

    box = Box(app, layout="grid", border=True)

    

    # les widgets

    message = Text(box, text="Bonjour le monde !", color="blue", grid=[0,0])

    message.text\_size=50

    message.bg = "red"

    

    entree = TextBox(box, text="entrer votre nom",  width=20, grid=[0,1])

    

    # bouton avec méthode callback quand le bouton est appuyé

    button\_nom = PushButton(box, text="afficher le nom", command=afficher\_name, grid=[1,1])

    button\_nom.bg = "green"

    

    # [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)

    button\_image = PushButton(box, image="pelle.png", width=40, height=40,

            command=cliquer\_pelle, args=["à tarte", "à gâteau"],grid=[0,2])

    message\_pelle = Text(box, text="Message de la pelle", width=60, grid=[1,2])

    

    logo = Picture(app, image="logo\_landerneau.png")

    

    # affichage de la fenêtre

    app.display()

    

    # fin exercice: exo9\_guizero.py







## Samedi 29 mai (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero (suite): Bouton
   * Initiation HTML/CSS/Javascript
       * éléments de base d'une page HTML (suite)




Ajouter une TextBox:

# exercice: exo6\_guizero.py



from guizero import App, Text, Picture, TextBox



app = App("Mon Application")

app.bg = "yellow"

app.width = 800

app.height = 800



message = Text(app, text="Bonjour le monde !", color="blue")

message.text\_size=50

message.bg = "red"



entree = TextBox(app, text="entrer votre nom",  width=20)



logo = Picture(app, image="logo\_landerneau.png")



app.display()



# fin exercice: exo6\_guizero.py





Ajouter un bouton PushButton

# exercice: exo7\_guizero.py



from guizero import App, Text, Picture, TextBox, PushButton



# fonctions pour le push button

def afficher\_name():

    print("le nom est ", entree.value)



def cliquer\_pelle(tarte, gateau):

    message\_pelle.value = "J'ai cliqué sur la pelle " + tarte

    # désactive le bouton

    button\_image.disable()



# la fenêtre de l'application

app = App("Mon Application")

app.bg = "yellow"

app.width = 800

app.height = 800



# les widgets

message = Text(app, text="Bonjour le monde !", color="blue")

message.text\_size=50

message.bg = "red"



entree = TextBox(app, text="entrer votre nom",  width=20)



# bouton avec méthode callback quand le bouton est appuyé

button\_nom = PushButton(app, text="afficher le nom", command=afficher\_name)

button\_nom.bg = "green"



# [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)

button\_image = PushButton(app, image="pelle.png", width=40, height=40, command=cliquer\_pelle, args=["à tarte", "à gâteau"])

message\_pelle = Text(app, text="Message de la pelle", width=60)





logo = Picture(app, image="logo\_landerneau.png")



# affichage de la fenêtre

app.display()



# fin exercice: exo7\_guizero.py





Il manque le paquet Python pillow pour retailler l'image:

$ pip3 install pillow







Références:

   * [https://libre-en-fete.net/2021/](https://libre-en-fete.net/2021/)
   * [https://icones8.fr/icon/23867/open-source](https://icones8.fr/icon/23867/open-source)
   * [https://papy-tux.legtux.org/doc1237/index.html](https://papy-tux.legtux.org/doc1237/index.html)




## Samedi 22 mai (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero (suite):
   * Initiation HTML/CSS/Javascript
       * éléments de base d'une page HTML (suite)


éditeur de texte: Geany 

Installation de geany (version 1.36 sur Ubuntu 20.04) et ses plugins (installation de tous les plugins)

$ sudo apt install geany geany-plugins



Utilisation de geany pour développer en Python3:

   * Aller dans Menu **Construire / Définir les commandes de construction**
   * Changer dans **Commandes pour Python / Compile**: python3 au lieu de python
   * Changer dans **Commande d'exécution / Execute**: python3 au lieu de python
   * Valider


Utilisation des widgets graphiques avec guizero:

   * Application
   * Text
   * Picture
   * TextBox
   * PushButton (et commande de rappel)


Pour convertir les images dans le format approprié (PNG/GIF), utilisation de imagemagick ([https://imagemagick.org/script/index.php)](https://imagemagick.org/script/index.php)):

$ sudo apt install imagemagick



Convertir une image JPG vers PNG:

$ convert <image>.jpg <image>.png



Afficher l'image:

$ display <image>.png



Pour afficher et rétrécir une image directement avec le widget PushButton, il faut installer PIL (pillow):

$ pip install pillow



# exercice: exo\_guizero.py

from guizero import App, Text



app = App(title="Mon application")

app.bg = "yellow"

app.width = 800

app.height = 800



message = Text(app, text="Bonjour le monde !", color="blue")

message.text\_size=50

message.bg = "red"



app.display()

# fin exercice: exo\_guizero.py







# exercice: exo5\_guizero.py



from guizero import App, Text, Picture



app = App("Mon Application")

app.bg = "yellow"

app.width = 800

app.height = 800



message = Text(app, text="Bonjour le monde !", color="blue")

message.text\_size=50

message.bg = "red"



logo = Picture(app, image="logo\_landerneau.png")

app.display()



# fin exercice: exo5\_guizero.py



Les tags HTML:

   * quelques exemples de balises




Références:

   * Geany: [https://www.geany.org/](https://www.geany.org/)
   * Guizero: [https://lawsie.github.io/guizero/](https://lawsie.github.io/guizero/)
   * ImageMagick: [https://imagemagick.org/script/index.php](https://imagemagick.org/script/index.php)
   * ffmpeg: [https://ffmpeg.org/](https://ffmpeg.org/)
   * [https://en.wikipedia.org/wiki/Comparison\_of\_video\_container\_formats](https://en.wikipedia.org/wiki/Comparison\_of\_video\_container\_formats)
   * [https://en.wikipedia.org/wiki/List\_of\_codecs](https://en.wikipedia.org/wiki/List\_of\_codecs)
   * [https://en.wikipedia.org/wiki/Comparison\_of\_video\_codecs](https://en.wikipedia.org/wiki/Comparison\_of\_video\_codecs)
   * [https://en.wikipedia.org/wiki/Raspberry\_Pi](https://en.wikipedia.org/wiki/Raspberry\_Pi)


chercher comment faire une Image en fond transparent .





## Samedi 15 mai (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
       * guizero
   * Initiation HTML/CSS/Javascript
       * serveur de page HTML avec Python
       * éléments de base d'une page HTML


Guizero: interface graphique



$ cd travail/sources

:~/travail/sources $ mkdir guizero\_exemple

$ cd guizero\_exemple



Création de l'environnement virtuel:

$ python3 -m venv .venv



Activation de l'environnement virtuel:

$ source .venv/bin/activate



Installation de la bibliothèque graphique guizero:

$ source .venv/bin/activate





Vérification de l'installation de guizero:

$ python

>>> import guizero



Exemple: fichier gz\_exemple.py:

----------

    from guizero import App

    

    app = App(title="Mon application")

    

    app.display()

----------



Démarrer l'exemple:

$ python gz\_exemple.py





Ajouter un widget de Text:

----------

    from guizero import App, Text

    

    app = App(title="Mon application")

    

    message = Text(app, text="Bonjour le monde !")

    app.display()

----------



Page HTML de base:

---------

    <!DOCTYPE html>

    <html>

        <head>

            <title>Ma page HTML</title>

            <meta charset="utf-8">

        </head>

        <body>

            Message dans la page Web.

        </body>

    </html>

----------------





 $ ls -l

-rw-r--r-- 1 pi pi 177 mai   15 11:48 index.html

$ python3 -m http.server 

Serving HTTP on 0.0.0.0 port 8000 ([http://0.0.0.0:8000/)](http://0.0.0.0:8000/)) ...



Ouvrir un navigateur Web pour afficher la page.

[http://raspberrypi.local:8000/](http://raspberrypi.local:8000/) ou

[http://localhost:8000/](http://localhost:8000/)





Références:

   * [https://www.raspberrypi.org/books-magazines/](https://www.raspberrypi.org/books-magazines/) ## livres et magzines
   * [https://www.wxpython.org/](https://www.wxpython.org/)
   * [http://wxglade.sourceforge.net/docs/intro.html#program-windows](http://wxglade.sourceforge.net/docs/intro.html#program-windows)
$ sudo apt install wxglade



à vérifier avec Geany.





**Deux semaines de pause et reprise le 15 mai**



## Samedi 24 avril (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * Exemples module: Emulateur d'ecran WS2812 (ruban de LED)
   * Initiation HTML/CSS/Javascript


Simulation de ruban de LED neopixel:

**Installation du simulateur vrtneopixel**:

$ pip3 install vrtneopixel

$ python3

>>> from vrtneopixel import *



**Installation de l'exemple**:

$ cd travail/sources/

$ git clone [https://github.com/Hackable-magazine/vrtneopixel](https://github.com/Hackable-magazine/vrtneopixel)

$ cd vrtneopixel/

$ cd vrtneopixel/sample/

$ python3 strandtest.py 



Exemple fichier:  exemple\_neopixel.py:

----------------------

from vrtneopixel import *

import time

# from neopixel import *



# variables pour configurer le ruban de LED

LED\_COUNT   = (1,30)

LED\_PIN     = 18 # Broche ou GPIO

LED\_FREQ\_HZ = 800000 # 800KHz

LED\_DMA     = 5

LED\_BRIGHTNESS = 255

LED\_INVERT  = False



# créer l'objet ruban,

# une instance de la classe neopixel

ruban = Adafruit\_NeoPixel(

            LED\_COUNT,

            LED\_PIN,

            LED\_FREQ\_HZ,

            LED\_DMA,

            LED\_INVERT,

            LED\_BRIGHTNESS

            )



# initialiser le ruban de LED

ruban.begin()



# préparer une LED, choisir la couleur

ruban.setPixelColor(0, Color(255, 0, 0))

# allumer la LED sur le ruban

ruban.show()



# ajouter un délai pour voir le ruban s'afficher

time.sleep(10) # attendre 10 secondes

# avant la fin de l'application

----------------------



Exemple de **matrice**: exemple\_matrice.py

---------------

from vrtneopixel import *

import time

# from neopixel import *



# variables pour configurer le ruban de LED

LED\_COUNT   = **(8,8)**

LED\_PIN     = 18 # Broche ou GPIO

LED\_FREQ\_HZ = 800000 # 800KHz

LED\_DMA     = 5

LED\_BRIGHTNESS = 255

LED\_INVERT  = False



# créer l'objet ruban,

# une instance de la classe neopixel

ruban = Adafruit\_NeoPixel(

            LED\_COUNT,

            LED\_PIN,

            LED\_FREQ\_HZ,

            LED\_DMA,

            LED\_INVERT,

            LED\_BRIGHTNESS

            )



# initialiser le ruban de LED

ruban.begin()



# préparer une LED, choisir la couleur

ruban.setPixelColor(0, Color(255, 0, 0))

ruban.setPixelColor(8, Color(255, 0, 0))

ruban.setPixelColor(16, Color(255, 0, 0))

ruban.setPixelColor(24, Color(255, 0, 0))

ruban.setPixelColor(32, Color(255, 0, 0))

ruban.setPixelColor(40, Color(255, 0, 0))

ruban.setPixelColor(48, Color(255, 0, 0))

ruban.setPixelColor(56, Color(255, 0, 0))

# allumer la LED sur le ruban

ruban.show()



# ajouter un délai pour voir le ruban s'afficher

time.sleep(10) # attendre 10 secondes

# avant la fin de l'application

--------------------



Exemple, fichier: rainbow.py

----------------------

from vrtneopixel import *

import time

# from neopixel import *



# variables pour configurer le ruban de LED

LED\_COUNT   = (20,20)

LED\_PIN     = 18 # Broche ou GPIO

LED\_FREQ\_HZ = 800000 # 800KHz

LED\_DMA     = 5

LED\_BRIGHTNESS = 255

LED\_INVERT  = False



# créer l'objet ruban,

# une instance de la classe neopixel

ruban = Adafruit\_NeoPixel(

            LED\_COUNT,

            LED\_PIN,

            LED\_FREQ\_HZ,

            LED\_DMA,

            LED\_INVERT,

            LED\_BRIGHTNESS

            )



# initialiser le ruban de LED

ruban.begin()



def wheel(pos):

    """Generate rainbow colors across 0-255 positions."""

    if pos < 85:

        return Color(pos * 3, 255 - pos * 3, 0)

    elif pos < 170:

        pos -= 85

        return Color(255 - pos * 3, 0, pos * 3)

    else:

        pos -= 170

        return Color(0, pos * 3, 255 - pos * 3)



# préparer une LED, choisir la couleur

iterations = 5

wait\_ms = 20

for j in range(256*iterations):

    for i in range(ruban.numPixels()):

        ruban.setPixelColor(i, wheel((int(i * 256 / ruban.numPixels()) + j) \& 255))

    ruban.show()

    time.sleep(wait\_ms/1000.0)



# ajouter un délai pour voir le ruban s'afficher

time.sleep(10) # attendre 10 secondes

# avant la fin de l'application

---------------------



Références:

   * [https://github.com/Hackable-magazine/vrtneopixel](https://github.com/Hackable-magazine/vrtneopixel)
   * [https://learn.adafruit.com/neopixels-on-raspberry-pi/python-usage](https://learn.adafruit.com/neopixels-on-raspberry-pi/python-usage)
   * [https://github.com/Aircoookie/WLED](https://github.com/Aircoookie/WLED) ## piloter les rubans de LED




## Samedi 17 avril (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * Exemples tkgpio
   * Initiation HTML/CSS/Javascript


Gestion de boutons er de LEDs:

fichier **boutonled.py**



--------------------------

    from tkgpio import TkCircuit

    

    # configuration du bouton led

    

    configuration = {

        "width": 640,

        "height": 480,

        "leds": [

            {"x": 50, "y": 40, "name": "LED 1", "pin": 21},

            {"x": 100, "y": 40, "name": "LED 2", "pin": 22},

            {"x": 150, "y": 40, "name": "LED 3", "pin": 23}

        ],

        "buttons": [

            {"x": 50, "y": 130, "name": "Press to toggle LED 1", "pin": 11},

            {"x": 50, "y": 180, "name": "Press to toggle LED 2", "pin": 12},

            {"x": 50, "y": 230, "name": "Press to toggle LED 3", "pin": 13},

        ]

    }

    

    # boucle principale

    circuit = TkCircuit(configuration)

    @circuit.run

    def main():

        from gpiozero import LED,Button

        from time import sleep

        # déclaration des LEDs

        led1 = LED(21)

        led2 = LED(22)

        led3 = LED(23)

    

        led1.off()

        led2.off()

        led3.off()

     

        button1 = Button(11)

        button2 = Button(12)

        button3 = Button(13)



       # on va attendre jusqu'à ce que le bouton numéro 1 soit appuyé

        print("appuyer sur le bouton numéro 1")

        button1.wait\_for\_press()

        print("j'ai appuyé sur le bouton numéro 1")

    

        button2.when\_pressed = led2.toggle



        # trouver un cas d'utilisation

        button3.when\_released = led3.toggle



    #    button1.when\_pressed = led1.toggle

    #    button2.when\_pressed = buzzer.on

    #    button2.when\_released = buzzer.off

    #    button3.when\_pressed = show\_sensor\_values

    

        while True:

   *      led1.on()
            sleep(1)

            led1.off()

            sleep(1)

--------------------------



Page Web:

   * [https://fr.wikipedia.org/wiki/Document\_Object\_Model](https://fr.wikipedia.org/wiki/Document\_Object\_Model)
   * [https://www.w3.org/TR/DOM-Level-3-Core/introduction.html](https://www.w3.org/TR/DOM-Level-3-Core/introduction.html)




## Samedi 10 avril (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * Exemples tkgpio


Exemple avec le capteur de mouvement



Fichier **mouvement.py**

--------------------------------

from tkgpio import TkCircuit



# configuration du capteur de mouvement et de l'écran



configuration = {

    "width": 640,

    "height": 480,

    "motion\_sensors": [

        {"x": 150, "y": 170, "name": "Motion Sensor", "pin": 27, "detection\_radius": 50, "delay\_duration": 5, "block\_duration": 3 }

    ],

    "lcds": [

        {"x": 30, "y": 40, "name": "LCD", "pins":[2, 3, 4, 5, 6, 7], "columns": 16, "lines": 2}

    ],

}



# boucle principale

circuit = TkCircuit(configuration)

@circuit.run

def main():

    from Adafruit\_CharLCD import Adafruit\_CharLCD

    from gpiozero import MotionSensor

    from time import sleep



    lcd = Adafruit\_CharLCD(2, 3, 4, 5, 6, 7, 16, 2)



    def affiche\_mouvement():

        lcd.clear()

        lcd.message(

            "Mouvement\ndetecte"

        )



    motion\_sensor = MotionSensor(27)

    motion\_sensor.when\_motion = affiche\_mouvement

    motion\_sensor.when\_no\_motion = lcd.clear



    while True:

        sleep(0.2)



--------------------------------





## Samedi 3 avril (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * tkgpio


Mise à jour de la Raspberry Pi OS:

$ sudo apt update

$ sudo apt upgrade



Création d'un nouveau circuit avec tkgpio



**Fichier vumetre.py**

------------------------------

from tkgpio import TkCircuit



# configuration du vu-mètre



configuration = {

    "width": 640,

    "height": 480,

    "leds": [

        {"x": 50, "y": 40, "name": "LED 1", "pin": 21},

        {"x": 100, "y": 40, "name": "LED 2", "pin": 22},

        {"x": 150, "y": 40, "name": "LED 3", "pin": 23},

        {"x": 200, "y": 40, "name": "LED 4", "pin": 24},

        {"x": 250, "y": 40, "name": "LED 5", "pin": 25},

        {"x": 300, "y": 40, "name": "LED 6", "pin": 26}

    ],

    "distance\_sensors": [

        {"x": 30, "y": 430, "name": "Distance Sensor (cm)", "trigger\_pin": 17, "echo\_pin": 18, "min\_distance": 0, "max\_distance": 30}

    ],

    "buttons": [

        {"x": 50, "y": 130, "name": "Press to toggle LED 2", "pin": 11},

    ]

}



# boucle principale

circuit = TkCircuit(configuration)

@circuit.run

def main():

    from gpiozero import LED, PWMLED, Button, DistanceSensor

    from time import sleep

    # déclaration des LEDs

    led1 = LED(21)

    led2 = LED(22)

    led3 = LED(23)

    led4 = LED(24)

    led5 = LED(25)

    led6 = LED(26)



    led1.off()

    led2.off()

    led3.off()

    led4.off()

    led5.off()

    led6.off()

 

    # création de l'instance du capteur ultrason

    sensor = DistanceSensor(echo=18, trigger=17) 

    while True:

        # distance entre 0, 30 (valeur de retour entre 0.01 et 0.31)

        ## print('Distance: ', sensor.distance * 100)

        vuled = sensor.distance * 100

        ## reset LED, toutes les LEDs off

        # resetLEDs()

        # affichage du vu-mètre

        if vuled < 5:

            led1.on()

            led2.off()

            led3.off()

            led4.off()

            led5.off()

            led6.off()            

        elif vuled < 10:

            led1.on()

            led2.on()

            led3.off()

            led4.off()

            led5.off()

            led6.off()

        elif vuled < 15:

            led1.on()

            led2.on()

            led3.on()

            led4.off()

            led5.off()

            led6.off()

        elif vuled < 20:

            led1.on()

            led2.on()

            led3.on()

            led4.on()

            led5.off()

            led6.off()

        elif vuled < 25:

            led1.on()

            led2.on()

            led3.on()

            led4.on()

            led5.on()

            led6.off()

        elif vuled < 30:

            led1.on()

            led2.on()

            led3.on()

            led4.on()

            led5.on()

            led6.on()



        sleep(0.2)



------------------------------



**Charger une page locale HTML dans le navigateur Web:**

$ **chromium-browser** exemple.html



Et on peut charger une page locale HTML dans le navigateur en appuyant **Control + O.**

Ouvre un explorateur du système de fichier et on choisit son fichier HTML à ouvrir.





## Samedi 27 mars (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * tkgpio


Exemples de callback



exemple\_rappel.py



-----------------------

# led1.toggle

def bonjour():

    print("bonjour")



# bouton when\_pressed

def methode\_callback(methode\_a\_appeler):

    methode\_a\_appeler()



# button.when\_pressed = led1.toggle

methode\_callback(bonjour)

-----------------------



$ python3 exemple\_rappel.py





Exemple méthode de callback avec Tk:

exemple\_rappel\_tk.py

---------------------------

from tkinter import *



root = Tk()



def bonjour(): # notre callback

    print("Bonjour !")



b = Button(root, text="Bonjour", command=bonjour)

b.pack()



root.mainloop() ## boucle d'interaction avec l'utilisateur

---------------------------



$ python3 exemple\_rappel\_tk.py



Exemple de Tk, position dans la fenêtre et utilisation de pack

---------------------

from tkinter import *



root = Tk()

frame = Frame(root)

frame.pack()



bottomframe = Frame(root)

bottomframe.pack( side = BOTTOM )



redbutton = Button(frame, text="Red", fg="red")

redbutton.pack( side = LEFT)



greenbutton = Button(frame, text="green", fg="green")

greenbutton.pack( side = LEFT )



bluebutton = Button(frame, text="Blue", fg="blue")

bluebutton.pack( side = LEFT )



blackbutton = Button(bottomframe, text="Black", fg="black")

blackbutton.pack( side = BOTTOM)



root.mainloop()

---------------------





Page HTML et CSS



-------------------------

<?xml version="1.0" encoding="UTF-8" ?>

<!DOCTYPE html>

<html>

    <head>

        <title>Ma Page Web</title>

        <!-- CSS dans un ficher extérieur -->

        <!-- link rel="stylesheet" href="style.css" / -->

        <!-- CSS dans l'entête -->

        <style>

            h1

            {

                color: blue;

            }

            p 

            {

                color:blueviolet;

            }

            .important

            {

                color: red;

                font-size: 40;

            }

            p.important

            {

                color: rgb(0, 255, 34);

                font-size: 40;

                background-color: salmon;

            }



            #monparagraphe

            {

                color: yellow;

                background-color: black;

                left: 30px;

            }

        </style>        

    </head>

    <body>

        <!-- CSS dans la balise -->

        <h1 style="border: 5cm;">Gros titre</h1>

        <h6>petit titre</h6>

        <h1 style="color: red;">Gros deuxième titre</h1>

        <h1 class="important">Gros deuxième titre</h1>



        <p>Bonjour ! une Phrase avec un retour à la ligne</p>

        <p class="important">Bonjour ! une Phrase avec un retour à la ligne</p>

        <p id="monparagraphe">Bonjour ! une Phrase avec un retour à la ligne</p>

        

        ééàçè$€

        ☺️ 😊 😇 🙂 🙃 😉 😌 😍 🥰 😘 😗 😙 😚 😋 😛 😝 😜 🤪 🤨 🧐 🤓 😎

    </body>

</html>

---------------------------------



Références:

   * [https://fr.wikipedia.org/wiki/Fonction\_de\_rappel](https://fr.wikipedia.org/wiki/Fonction\_de\_rappel)
   * [https://developer.mozilla.org/fr/docs/Web/CSS](https://developer.mozilla.org/fr/docs/Web/CSS)






## Samedi 20 mars (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * tkgpio


Fin de l'installation:



Mise à jour de Pillow:

$ pip3 install Pillow --upgrade



**Installation de lib audio et blas (numpy):**

    sudo apt install libportaudio2 libasound-dev libatlas-base-dev 

    

Démarrage de l'exemple:

$ python3 test\_exemple.py



Installation de **tree** pour afficher la liste des fichiers d'une arborescence:

$ sudo apt install tree



**Test de big circuit:**

Le fichier big\_circuit se trouve dans les exemples:

$ cd travail/sources/**tkgpio**



$ cd docs/examples/big\_circuit

$ python3 big\_circuit.py



Expression 'paInvalidSampleRate' failed in 'src/hostapi/alsa/pa\_linux\_alsa.c', line: 2048

Expression 'PaAlsaStreamComponent\_InitialConfigure( \&self->playback, outParams, self->primeBuffers, hwParamsPlayback, \&realSr )' failed in 'src/hostapi/alsa/pa\_linux\_alsa.c', line: 2722

Expression 'PaAlsaStream\_Configure( stream, inputParameters, outputParameters, sampleRate, framesPerBuffer, \&inputLatency, \&outputLatency, \&hostBufferSizeMode )' failed in 'src/hostapi/alsa/pa\_linux\_alsa.c', line: 2843

Exception in Tkinter callback

Traceback (most recent call last):

  File "/usr/lib/python3.7/tkinter/\_\_init\_\_.py", line 1705, in \_\_call\_\_

    return self.func(*args)

  File "/usr/lib/python3.7/tkinter/\_\_init\_\_.py", line 749, in callit

    func(*args)

  File "/home/pi/.local/lib/python3.7/site-packages/tkgpio/tkgpio.py", line 83, in \_update\_outputs

    output.update()

  File "/home/pi/.local/lib/python3.7/site-packages/tkgpio/tkgpio.py", line 193, in update

    play(self.\_sample\_wave, self.SAMPLE\_RATE, loop=True)

  File "/home/pi/.local/lib/python3.7/site-packages/sounddevice.py", line 177, in play

    **kwargs)

  File "/home/pi/.local/lib/python3.7/site-packages/sounddevice.py", line 2578, in start\_stream

    **kwargs)

  File "/home/pi/.local/lib/python3.7/site-packages/sounddevice.py", line 1489, in \_\_init\_\_

    **\_remove\_self(locals()))

  File "/home/pi/.local/lib/python3.7/site-packages/sounddevice.py", line 895, in \_\_init\_\_

    'Error opening {}'.format(self.\_\_class\_\_.\_\_name\_\_))

  File "/home/pi/.local/lib/python3.7/site-packages/sounddevice.py", line 2738, in \_check

    raise PortAudioError(errormsg, err)

sounddevice.PortAudioError: Error opening OutputStream: Invalid sample rate [PaErrorCode -9997]

pi@raspberrypi:~/travail/sources/tkgpio/docs/examples/big\_circuit $ python3 big\_circuit.py



Configuration du son:

[https://www.raspberrypi.org/documentation/configuration/audio-config.md](https://www.raspberrypi.org/documentation/configuration/audio-config.md)



Clé USB pour récupérer la domotique (statio météo, 433, 866...)







## Samedi 13 mars (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python
   * tkgpio




Installation de tkgpio:

Cloner le dépôt:

$ git clone [https://github.com/wallysalami/tkgpio.git](https://github.com/wallysalami/tkgpio.git)

$ cd tkgpio



Installation 

$ pip3 install .



Mise à jour de numpy:

$  pip3 install numpy --upgrade



Code pour tester (fichier **test\_exemple.py**):

-----------------------------

    from tkgpio import TkCircuit

    # initialize the circuit inside the 

    configuration = {

        "width": 300,

        "height": 200,

        "leds": [

            {"x": 50, "y": 40, "name": "LED 1", "pin": 21},

            {"x": 100, "y": 40, "name": "LED 2", "pin": 22}

        ],

        "buttons": [

            {"x": 50, "y": 130, "name": "Press to toggle LED 2", "pin": 11},

        ]

    }

    circuit = TkCircuit(configuration)@circuit.rundef main ():

        

        # now just write the code you would use on a real Raspberry Pi

        

        from gpiozero import LED, Button

        from time import sleep

        

        led1 = LED(21)

        led1.blink()

        

        def button\_pressed():

            print("button pressed!")

            led2.toggle()

        

        led2 = LED(22)

        button = Button(11)

        button.when\_pressed = button\_pressed

        

        while True:

            sleep(0.1)

-----------------------------



Mise à jour de Pillow:

$ pip3 install Pillow --upgrade



Installation de lib audio et blas (numpy):

    sudo apt install libportaudio2 libasound-dev libatlas-base-dev 

    

Démarrage de l'exemple:

$ python3 test\_exemple.py







## Samedi 20 février (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python/Pygame (suite et fin)


Victoire sur les aliens

------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    # afficher du texte sur l'ecran

    def afficherEcran(screen, message):

        pygame.font.init()

        font = pygame.font.SysFont('Arial', 50)

        textsurface = font.render(message, False, (44, 0, 62))

        screen.blit(textsurface, (110, 160))

    # fin de la méthode

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # vérifier si il reste encore des aliens

        if len(aliens) == 0:

            # le tableau des aliens est vide

            afficherEcran(screen, "Victoire sur les aliens")

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

            # vérification de collision avec les rockets

            for chaqueRocket in rockets:

                if (chaqueRocket.x < chaqueAlien.x + 30 and

                    chaqueRocket.x > chaqueAlien.x and

                    chaqueRocket.y < chaqueAlien.y + 30 and 

                    chaqueRocket.y > chaqueAlien.y - 30):

                    # enter en collision

                    # enlever l'alien

                    aliens.remove(chaqueAlien)

                    # enlever la rocket

                    rockets.remove(chaqueRocket)

            # vérifier qu'un Alien est arrivé au niveau du vaisseau

            if chaqueAlien.y > space\_y:

                afficherEcran(screen, "Game Over!")

    

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

        for chaqueRocket in rockets:

            chaqueRocket.draw()

            if chaqueRocket.y >= 0:

                nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

------





**Méthode d'affichage centrée:**

----------

    # afficher du texte sur l'ecran

    def afficherEcran(screen, message):

        pygame.font.init()

        font = pygame.font.SysFont('Arial', 60)

        textsurface = font.render(message, False, (44, 0, 62))

        text\_rect = textsurface.get\_rect(center=(640/2, 480/2))

        screen.blit(textsurface, text\_rect)

    # fin de la méthode

---------------------

 

 

**Gestion de la fin du jeu:**

-----------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.20

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    # afficher du texte sur l'ecran

    def afficherEcran(screen, message):

        pygame.font.init()

        font = pygame.font.SysFont('Arial', 60)

        textsurface = font.render(message, False, (44, 0, 62))

        text\_rect = textsurface.get\_rect(center=(640/2, 480/2))

        screen.blit(textsurface, text\_rect)

    # fin de la méthode

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    # game over, figer le jeu

    perdu = False

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # afficherEcran(screen, "Le jeu des aliens")

        # vérifier si il reste encore des aliens

        if len(aliens) == 0:

            # le tableau des aliens est vide

            afficherEcran(screen, "Victoire sur les aliens")

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

            # vérification de collision avec les rockets

            for chaqueRocket in rockets:

                if (chaqueRocket.x < chaqueAlien.x + 30 and

                    chaqueRocket.x > chaqueAlien.x and

                    chaqueRocket.y < chaqueAlien.y + 30 and 

                    chaqueRocket.y > chaqueAlien.y - 30):

                    # enter en collision

                    # enlever l'alien

                    aliens.remove(chaqueAlien)

                    # enlever la rocket

                    rockets.remove(chaqueRocket)

            # vérifier qu'un Alien est arrivé au niveau du vaisseau

            if (chaqueAlien.y + 30) > space\_y:

                afficherEcran(screen, "Game Over!")

                # j'ai perdu

                perdu = True

    

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        if not perdu:

            dessiner\_vaisseau(screen, space\_x, space\_y)

            for chaqueRocket in rockets:

                chaqueRocket.draw()

                if chaqueRocket.y >= 0:

                    nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

----------



Références:

   * [https://nasa.github.io/fprime/](https://nasa.github.io/fprime/)
   * [https://opensourcerover.jpl.nasa.gov/](https://opensourcerover.jpl.nasa.gov/)
   * [https://joshdata.me/iceberger.html](https://joshdata.me/iceberger.html)
   * Jeux Excel: [https://www.excelstars.com/fr/juegos-excel/](https://www.excelstars.com/fr/juegos-excel/)
   * VBA: [https://www.excel-pratique.com/fr/vba](https://www.excel-pratique.com/fr/vba)
   * Gambas Basic: [http://gambas.sourceforge.net/en/main.html#](http://gambas.sourceforge.net/en/main.html#)
   * FreeBasic: [https://www.freebasic.net/](https://www.freebasic.net/)




## Samedi 13 février (visio)



[https://books.google.fr/books?id=-zCtDwAAQBAJ\&pg=PR4\&lpg=PR4\&dq=Apprendre+%C3%A0+coder+des+jeux+vid%C3%A9o+en+Python+/+Al+Sweigart+;+traduction+fran%C3%A7aise,+Paul+Durand+Degranges\&source=bl\&ots=CJPlbSUalt\&sig=ACfU3U1Kzs4EZFQxGLNGJMJEPCBqqRrmwQ\&hl=fr\&sa=X\&ved=2ahUKEwjYntL0yMnuAhWtxIUKHUYODeg4ChDoATAIegQIDBAC#v=onepage\&q=Apprendre%20%C3%A0%20coder%20des%20jeux%20vid%C3%A9o%20en%20Python%20%2F%20Al%20Sweigart%20%3B%20traduction%20fran%C3%A7aise%2C%20Paul%20Durand%20Degranges\&f=false](https://books.google.fr/books?id=-zCtDwAAQBAJ\&pg=PR4\&lpg=PR4\&dq=Apprendre+%C3%A0+coder+des+jeux+vid%C3%A9o+en+Python+/+Al+Sweigart+;+traduction+fran%C3%A7aise,+Paul+Durand+Degranges\&source=bl\&ots=CJPlbSUalt\&sig=ACfU3U1Kzs4EZFQxGLNGJMJEPCBqqRrmwQ\&hl=fr\&sa=X\&ved=2ahUKEwjYntL0yMnuAhWtxIUKHUYODeg4ChDoATAIegQIDBAC#v=onepage\&q=Apprendre%20%C3%A0%20coder%20des%20jeux%20vid%C3%A9o%20en%20Python%20%2F%20Al%20Sweigart%20%3B%20traduction%20fran%C3%A7aise%2C%20Paul%20Durand%20Degranges\&f=false)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python/Pygame (suite)


Mise en oeuvre du Débuggeur Python dans Visual Studio Code.



Gestion des collisions

------------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

            for chaqueRocket in rockets:

                if (chaqueRocket.x < chaqueAlien.x + 30 and

                    chaqueRocket.x > chaqueAlien.x and

                    chaqueRocket.y < chaqueAlien.y + 30 and 

                    chaqueRocket.y > chaqueAlien.y - 30):

                    # enter en collision

                    # enlever l'alien

                    aliens.remove(chaqueAlien)

                    # enlever la rocket

                    rockets.remove(chaqueRocket)

    

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

        for chaqueRocket in rockets:

            chaqueRocket.draw()

            if chaqueRocket.y >= 0:

                nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

------------



Liste des fontes installés sur la RPi:

    fc-list



--------------------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    # afficher du texte sur l'ecran

    def afficherEcran(screen, message):

        pygame.font.init()

        font = pygame.font.SysFont('Arial', 50)

        textsurface = font.render(message, False, (44, 0, 62))

        screen.blit(textsurface, (110, 160))

    # fin de la méthode

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

            # vérification de collision avec les rockets

            for chaqueRocket in rockets:

                if (chaqueRocket.x < chaqueAlien.x + 30 and

                    chaqueRocket.x > chaqueAlien.x and

                    chaqueRocket.y < chaqueAlien.y + 30 and 

                    chaqueRocket.y > chaqueAlien.y - 30):

                    # enter en collision

                    # enlever l'alien

                    aliens.remove(chaqueAlien)

                    # enlever la rocket

                    rockets.remove(chaqueRocket)

            # vérifier qu'un Alien est arrivé au niveau du vaisseau

            if chaqueAlien.y > space\_y:

                afficherEcran(screen, "Game Over!")

    

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

        for chaqueRocket in rockets:

            chaqueRocket.draw()

            if chaqueRocket.y >= 0:

                nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

--------------------

Installation de la libSDL2 pour gérer les polices TTF:

    $ sudo apt install libsdl2-ttf-2.0-0



Références:

   * [https://codes-sources.commentcamarche.net/source/list/python-19/340-jeux/last](https://codes-sources.commentcamarche.net/source/list/python-19/340-jeux/last)
   * [https://python.doctor/page-syntaxe-differente-python2-python3-python-differences](https://python.doctor/page-syntaxe-differente-python2-python3-python-differences)
   * [https://docs.python.org/fr/3/howto/pyporting.html](https://docs.python.org/fr/3/howto/pyporting.html)
   * [http://doc.ubuntu-fr.org/testdisk](http://doc.ubuntu-fr.org/testdisk)
   * [https://gparted.org/](https://gparted.org/)
   * [https://www.tecmint.com/check-linux-hard-disk-bad-sectors-bad-blocks/](https://www.tecmint.com/check-linux-hard-disk-bad-sectors-bad-blocks/) ## SMART ctl
   * [https://fr.flossmanuals.net/creer-des-jeux-en-python-avec-pygame/des-jeux-en-python/](https://fr.flossmanuals.net/creer-des-jeux-en-python-avec-pygame/des-jeux-en-python/)
   * 



## Samedi 6 février (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python/Pygame (suite)


Lancer des rockets

   * tirer les rockets
   * ~~effacer~~ les rockets


-------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # class de rocket

    class Rocket:

    

        #  initialisation de l'instance

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        # dessiner sur l'écran

        def draw(self):

            pygame.draw.rect(self.screen, 

                    (254, 52, 110),

                    pygame.Rect(self.x, self.y, 2, 4))

            self.y = self.y - 2

        # fin de la fonction

    # fin de la classe Rocket

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    rockets = []

    nouveau\_rockets = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    espace\_x\_entre\_alien = 10

    # générer les aliens

    for colonne in range(15): # for i = 0 , i < 15 , i++

        for ligne in range(4):

            #  x, y

            aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))

        # fin de ligne

    # fin de colonne

    # monAlien1 = Alien(screen, 30, 30)

    # monAlien3 = Alien(screen, 30+30+10, 30)

    # monAlien4 = Alien(screen, 110, 30)

    # monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # copie de tableau

        rockets = nouveau\_rockets

        nouveau\_rockets = []

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

                

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

            # quand la touche ESPACE est appuyée, tir de rocket

            if event.type == pygame.KEYDOWN and event.key == pygame.K\_SPACE:

                rockets.append(Rocket(screen, space\_x, space\_y))

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner les aliens

        for chaqueAlien in aliens:

            # re-dessiner un alien

            chaqueAlien.draw()

        # monAlien1.draw() # Alien.draw(monAlien1)

        # monAlien2.draw()

        # monAlien3.draw()

        # monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

        for chaqueRocket in rockets:

            chaqueRocket.draw()

            if chaqueRocket.y >= 0:

                nouveau\_rockets.append(chaqueRocket)

            # rocket est en dehors de l'écran

            # enlever la rocket du tableau

    

    # fin de la boucle

    # sortie

------





## Samedi 30 janvier (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Initiation Python/Pygame (suite)


Dessiner le vaisseau spécial:

------------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # base de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    monAlien1 = Alien(screen, 30, 30)

    monAlien2 = Alien(screen, 100, 100)

    monAlien3 = Alien(screen, 30+30+10, 30)

    monAlien4 = Alien(screen, 110, 30)

    

    # boucle principale

    while not done:

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner

        monAlien1.draw() # Alien.draw(monAlien1)

        monAlien2.draw()

        monAlien3.draw()

        monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

    

    # fin de la boucle

    # sortie

-----------



Bouger le vaisseau vers la droite et vers la gauche:

-------------

    import pygame

    

    class Alien:

    

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    # dessiner vaisseau

    def dessiner\_vaisseau(screen\_vaisseau, vaisseau\_x,vaisseau\_y):

        pygame.draw.rect(screen\_vaisseau,

            (210, 250, 251),

            pygame.Rect(vaisseau\_x, vaisseau\_y, 8,5))

    ## fin de la méthode dessiner vaisseau

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    space\_x = width / 2 # milieu de l'écran

    space\_y = height - 20 # bas de l'écran

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    monAlien1 = Alien(screen, 30, 30)

    monAlien2 = Alien(screen, 100, 100)

    monAlien3 = Alien(screen, 30+30+10, 30)

    monAlien4 = Alien(screen, 110, 30)

    

    # boucle principale

    while not done:

    

        # action sur une touche

        pressed = pygame.key.get\_pressed()

        if pressed[pygame.K\_LEFT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x >= 20:

                # diminuer space\_x de 2 pour aller vers la gauche

                space\_x = space\_x - 2

            ## fin de if

        ## fin de if pressed

        if pressed[pygame.K\_RIGHT]:

            # colonne Alien la plus à gauche 30, vaisseau >= 20

            if space\_x <= (width - 20):

                # augmenter space\_x de 2 pour aller vers la droite

                space\_x = space\_x + 2

            ## fin de if

        ## fin de if pressed

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner

        monAlien1.draw() # Alien.draw(monAlien1)

        monAlien2.draw()

        monAlien3.draw()

        monAlien4.draw()

        ## dessiner le vaisseau

        dessiner\_vaisseau(screen, space\_x, space\_y)

    

    # fin de la boucle

    # sortie

------------



Références:

   * [https://code.visualstudio.com/](https://code.visualstudio.com/)
   * [https://code.visualstudio.com/#alt-downloads](https://code.visualstudio.com/#alt-downloads)


sudo apt install ./code\_1.52.1-1608136275\_armhf.deb 





## Samedi 23 janvier (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Mise en oeuvre de mDNS: [https://en.wikipedia.org/wiki/Multicast\_DNS](https://en.wikipedia.org/wiki/Multicast\_DNS)
   * Initiation Python (suite)


Initiation Python:

$ cd travail/sources

$ mkdir jeu

$ cd jeu

$ python3 -m venv .venv

$ source .venv/bin/activate

(.venv) $ **pip install pygame**



(.venv)  $ **python**

Python 3.7.3 (default, Jul 25 2020, 13:03:44) 

[GCC 8.3.0] on linux

Type "help", "copyright", "credits" or "license" for more information.

>>> import pygame

pygame 2.0.1 (SDL 2.0.9, Python 3.7.3)

Hello from the pygame community. [https://www.pygame.org/contribute.html](https://www.pygame.org/contribute.html)

>>> 

$ code



fichier space\_invaders.py:

-------------------------

    import pygame

    

    screen = None

    aliens = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    # boucle principale

    while not done:

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

    # fin de la boucle

    # sortie

-------------------------





Avec la classe Alien:



-------------------    

    import pygame

    

    class Alien:

        def \_\_init\_\_(self, screen, x, y):

            self.x = x

            self.y = y

            self.screen = screen

    

        def draw(self):

            pygame.draw.rect(self.screen,

                (80, 40, 90),

                pygame.Rect(self.x, self.y, 30, 30))

            self.y = self.y + 0.05

    

    # fin de classe Alien

    

    screen = None

    # tableau d'aliens, à partir de la classe Alien

    aliens = []

    

    pygame.init()

    width = 640

    height = 480

    BLACK = (0,0,0)

    

    screen = pygame.display.set\_mode((width, height))

    # un objet Clock: horloge pour compter les FPS

    clock = pygame.time.Clock()

    

    done = False # True=1, False=0

    

    monAlien1 = Alien(screen, 30, 30)

    monAlien2 = Alien(screen, 100, 100)

    

    # boucle principale

    while not done:

        # boucle pour traiter tous les événements

        for event in pygame.event.get():

            if event.type == pygame.QUIT:

                done = True

        # gestion de mon animation

        pygame.display.flip()

        clock.tick(60)

        # couleur (R:0-255 => 2^8, G:0-255, B:0-255)

        screen.fill(BLACK)

        # dessiner

        monAlien1.draw() # Alien.draw(monAlien1)

        monAlien2.draw()

    

    # fin de la boucle

    # sortie

-------------------





Références:

   * PyGame: [https://www.pygame.org/news](https://www.pygame.org/news)
   * SDL: [https://www.libsdl.org/](https://www.libsdl.org/)
   * FIFO: [https://fr.wikipedia.org/wiki/File\_(structure\_de\_donn%C3%A9es)](https://fr.wikipedia.org/wiki/File\_(structure\_de\_donn%C3%A9es))
   * Palette de couleur: [https://htmlcolorcodes.com/fr/](https://htmlcolorcodes.com/fr/)
   * 





## Samedi16 janvier (visio)



Visio-conférence de 10h à 12h.



Programme:

   * Mise en oeuvre de RaspAP (RPi): [https://github.com/billz/raspap-webgui](https://github.com/billz/raspap-webgui)
   * Initiation Python (suite)


### RaspAP

Installation:

$ curl -sL [https://install.raspap.com](https://install.raspap.com) | bash



Utilisation de RaspAP:

Page Web d'Admin: localhost (defaut: **admin**/**secret**)



**Initiation Python (suite)**

Installation d'un IDE Python Thonny ou Code (ou d'un éditeur de texte) 

Installation de Code:

Téléchargement sur [https://code.visualstudio.com/docs/?dv=linuxarmhf\_deb](https://code.visualstudio.com/docs/?dv=linuxarmhf\_deb)

Installation:

$ sudo apt install ./code\_1.52.1-1608136275\_armhf.deb 



Démarrage de l'environnement virtuel Python:

$ mkdir -p travail/jeu

$ cd travail/jeu

$ python3 -m venv .venv

$ ../travail/jeu $ source .venv/bin/activate



Pour désactiver l'environnement virtuel:

(.venv) ~/travail/jeu $ deactivate 



Recherche des paquets Python sur Pypi: [https://pypi.org/](https://pypi.org/)

Installation du paquet pygame:

(.venv)  ../travail/jeu $ pi install pygame

(.venv)  ../travail/jeu $ python

>>> import pygame



Dansle fichier **jeu.py** :



    import pygame

    

    if \_\_name\_\_ == '\_\_main\_\_':

        print("coucou")







## Samedi 9 janvier (visio)



Visio-conférence de 10h à 12h.



Mise en oeuvre de Pi-hole: [https://github.cpython3m/pi-hole/pi-hole](https://github.cpython3m/pi-hole/pi-hole)



### Pi-hole

Installation:

$ wget -O basic-install.sh [https://install.pi-hole.net](https://install.pi-hole.net)

$ sudo bash basic-install.sh





Python

Python => 2

$ python



Python => 3

$ python3



Module création d'un environnement virtuel:

$ sudo apt install python3-venv



Création de répertoire de travail

$ mkdir -p travail/py\_opencv

$ cd travail/py\_opencv



Créer l'environnement virtuel:

$ python3 -m venv .venv



Activer l'environnement virtuel:

$ source .venv/bin/activate



Rerchercher une bibliothèque sous PIP:

$ pip search opencv



IDE:

   * Thonny IDE (livré avec la RaspberryPi OS)
   * Visual Studio Code
       * Télécharger le paquet Debian ARM 
sudo dpkg -i code\_1.52.1-1608136275\_armhf.deb





Pour **désactiver** l'environnement virtuel:

$ deactivate





Références:

   * [https://realpython.com/python-virtual-environments-a-primer/](https://realpython.com/python-virtual-environments-a-primer/)
   * [https://docs.python.org/3/tutorial/venv.html]([]https://docs.python.org/3/tutorial/venv.html[])
   * [https://code.visualstudio.com/](https://code.visualstudio.com/)
   * [https://github.com/VSCodium/vscodium](https://github.com/VSCodium/vscodium)
   * [https://fr.wikipedia.org/wiki/Raspberry\_Pi#Mod%C3%A8le\_3\_B\_(Raspberry\_Pi\_3)](https://fr.wikipedia.org/wiki/Raspberry\_Pi#Mod%C3%A8le\_3\_B\_(Raspberry\_Pi\_3))






## Samedi 19 décembre (visio)



Visio-conférence de 10h à 12h.



Suite atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)

   * Démarrage automatique de l'application
       * Systemd
   * Cron: exécuter des scripts à une date et une heure spécifiée à l’avance. 
   * Awk: traitement et manipulation de fichiers textuels ligne par ligne pour des opérations de recherches, de remplacement et de transformations complexes.


Références:

   * Cron: [https://fr.wikipedia.org/wiki/Cron](https://fr.wikipedia.org/wiki/Cron)
   * Awk: [https://fr.wikipedia.org/wiki/Awk](https://fr.wikipedia.org/wiki/Awk)
   * Liste des commandes: [https://fr.wikipedia.org/wiki/Commandes\_Unix](https://fr.wikipedia.org/wiki/Commandes\_Unix)
   * [https://developer.ibm.com/tutorials/l-lpic1-map/](https://developer.ibm.com/tutorials/l-lpic1-map/)
   * [https://www.lpi.org/our-certifications/exam-101-objectives](https://www.lpi.org/our-certifications/exam-101-objectives)
   * [http://www.mindsensors.com/stem-with-robotics/141-pistorms-v2-express-kit-raspberry-pi-brain-for-lego-robot](http://www.mindsensors.com/stem-with-robotics/141-pistorms-v2-express-kit-raspberry-pi-brain-for-lego-robot)


Crontab:

éditer:

pi$ crontab -e



# m h  dom mon dow   command

0 * * * * df >> /home/pi/df.log





AWK

awk -F: '{print $0}' /etc/passwd

awk -F: '{print $1}' /etc/passwd

awk -F: '{print $1 ":" $7}' /etc/passwd

awk -F: '/bash/ {print $1}' /etc/passwd





Liens:

   * [https://github.com/billz/raspap-webgui](https://github.com/billz/raspap-webgui)  ## Point d'accès Wifi
   * [https://pi-hole.net/](https://pi-hole.net/)  ## 
   * [https://en.wikipedia.org/wiki/Raspberry\_Pi#Model\_B](https://en.wikipedia.org/wiki/Raspberry\_Pi#Model\_B)  ## ARMv8






## Samedi 12 décembre (visio)



Visio-conférence de 10h à 12h.



Suite atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)

   * Démarrage automatique de l'application
       * Systemd
   * Sauvegarde et restauration d'une carte SD
   * mot de passe perdu




Sauvegarde et restauration de la carte SD



* Windows avec **Win32 Disk Imager** disponible sur: [https://sourceforge.net/projects/win32diskimager/](https://sourceforge.net/projects/win32diskimager/)



commande **read** => toute la carte SD (toutes les partitions) vers image (img)

commande **write** => image (img) vers toute la carte SD (**écrase le contenu**)





* RaspberryPi OS avec l'utilitaire: SD Card Copier avec un lecteur de carte SD externe (supplémentaire sur port USB)

=> Menu Accessoires / SD Card Copier



ou installation



$ sudo apt update

$ sudo apt install piclone



=> copier la carte SD vers une autre carte SD



* Sur Linux avec la commande **dd**



# trouver le **device** sur lequel se trouve la carte SD

$ df -h

/dev/**mmcblk0**p1 57288 14752 42536 26% /boot

ou

/dev/sda5 57288 9920 47368 18% /media/boot



# copier la carte SD dans une image

$ sudo dd if=/dev/sdb of=/home/<user>/backup/SDCardBackup.img



# restaurer l'image sur la carte SD



## démonter les partitions si elles sont déjà montées

Par exemple:

$ sudo umount /dev/sdb1

$ sudo umount /dev/sdb2



## copier l'image sur la carte SD

$ sudo dd bs=4M if=/home/<user>/backup/SDCardBackup.img of=/dev/sdb



**Mot de passe Raspberry Pi perdu**



# éteindre la Raspberry Pi



# extraire la carte SD



# avec un autre PC, changer la commande de démarrage (fichier cmdline.txt dans répertoire boot) en ajoutant à la fin:



init=/bin/sh



# redémarrer la RPi avec la carte SD



# démarrage en mode root



# remonter le système de fichier en lecture/écriture



**mount -o remount,rw /**



# changer le mot de passe



password pi

sync



# éteindre la RPi de nouveau

exec /sbin/init  # 0-6



# ne pas oublier le nouveau mot de passe



# extraire la carte SD pour enlever init=/bin/sh du fichier cmdline.txt dans répertoire boot.



# redémarrer la RPi avec la carte SD



# Systemd



Systemd contrôle l'initialisation du système et des services sur la plupart des distribution GNU/Linux.



Pour démarrer le Magic Mirror avec Systemd, il va falloir placer Magic Mirror dans un répertoire utilisateur dédié "**magic**"



## création d'un répertoire d'utilisateur "magic"



$ sudo adduser magic

=> mot de passe vide



## copier le projet dans /home/magic à la racine



$ sudo cp -r /home/pi/MagicMirror /home/magic



**Script pour démarrer le Magic Mirror en mode "server only":**

Fichier /etc/systemd/system/magicmirror.service

$ sudo vi /etc/systemd/system/magicmirror.service



$ sudo nano /etc/systemd/system/magicmirror.service

****************************

[Unit]

Description=Magic Mirror

After=network.target

StartLimitIntervalSec=0



[Service]

Type=simple

Restart=always

RestartSec=1

User=magic

WorkingDirectory=/home/magic/MagicMirror/

ExecStart=/usr/bin/node serveronly



[Install]

WantedBy=multi-user.target

****************************



# démarrage le service de Magic Mirror 

$ **sudo systemctl start magicmirror.service**

 

# arrêter le service Magic Mirror

$ sudo systemctl stop magicmirror.service



# vérifier l'état du sevice Magic Mirror

$ **sudo systemctl status magicmirror.service**





# activer le démarrage automatique de Magic Mirror lors du démarrage de la RaspberryPi

$ sudo systemctl enable magicmirror.service



# désactiver le démarrage automatique de Magic Mirror lors du boot de la RaspberryPi

$ sudo systemctl disable magicmirror.service





## Samedi 5 décembre (visio)



Visio-conférence de 10h à 12h.



Suite atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)

   * Démarrage automatique de l'application


Etudes de deux systèmes:

   * PM2
   * Systemd
   * autre: [https://www.npmjs.com/package/forever](https://www.npmjs.com/package/forever)


[https://semver.npmjs.com/](https://semver.npmjs.com/)



### PM2

Installation de PM2

$ sudo npm install -g pm2



Faire en sorte que PM2 soit lancé au démarrage de la RPi:

$ pm2 startup



Créer un script pour lancer l'application (mm.sh) dans le répertoire home

$ cd ~

$ vi mm.sh

cd ./MagicMirror

DISPLAY=:0 npm start



Rendre le fichier exécutable:

$ chmod +x mm.sh



Démarrer le miroir magique avec la commande:

$ pm2 start mm.sh



Rendre la configuration persistente au reboot:

$ pm2 save





# Autres commande pour gérer l'application



Redémarer l'application:

$ pm2 restart mm



**Stopper l'application**:

$ pm2 stop mm



Voir les messages (logs) de l'application:

$ pm2 logs mm



Affichier les informations sur le process de l'application:

$ pm2 show mm



**Enlever Miroir Magique au démarrage:**

$ pm2 delete mm

$ pm2 save --force



Désactiver pm2 au démarrage:

$ pm2 unstartup



Valider/activer le SSH sur la Raspberry Pi:

Menu Fichier / Préférences / Configuration du Raspberry Pi / Interfaces / Activer SSH et redémarrer la Raspberry Pi



Putty (application graphique): pour Windows ou Linux:

    [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)



Pour trouver l'addresse IP de la machine (sur laquelle on va se connecter):

$ ifconfig

wlp3s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500

        inet 1**92.168.1.105**  netmask 255.255.255.0  broadcast 192.168.1.255



 $ sudo apt install putty



Démarrage l'application:

$ putty 

=> addresse IP de la machine distante

ensuite **Accept**

login: **pi**

password**: raspberry**





## Samedi 28 novembre (visio)



Visio-conférence de 10h à 12h.



Suite atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)

   * création d'un module externe: en utilisant YesNo API:  [https://yesno.wtf/api](https://yesno.wtf/api)
   * Démarrage automatique de l'application


### Création d'un module



Création d'un module pour MagicMirror

Utilisation de l'API YesNo: [https://yesno.wtf](https://yesno.wtf)



# Installation de nodejs et de npm

$ sudo apt update

$ sudo apt install nodejs npm



Installation de curl et de JQ:

$ sudo apt install curl   jq



# Vérification

$ node -v

v10.19.0



$ npm -v

6.14.4



# Création d'un répertoire de travail

$ mkdir -p travail/sources

$ cd travail/sources



# Récupérer les sources de MagicMirror

$ git clone [https://github.com/MichMich/MagicMirror.git](https://github.com/MichMich/MagicMirror.git)

$ cd MagicMirror



# Installation des dépendances de MagicMirror

$ npm install

...



# Copier le template de configuration pour le modifier et pourvoir démarre MagicMirror

$ cp config/config.js.sample config/config.js



# Bonne pratique: Vérifier la syntaxe du fichier de configuration avant de démarrer l'application

$ npm run config:check



# Démarrer MagicMirror avec la configuration par défaut (en mode client Electron)

$ npm run start



Pour quitter: 

* cliquer sur la touche Alt, puis en haut, menu File / Quit

ou

* appuyer sur les touches Crtl + Q





# Créer son module



Références:

* [https://docs.magicmirror.builders/development/introduction.html](https://docs.magicmirror.builders/development/introduction.html)

* [https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules](https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules)

* Exemple à partir de : [https://github.com/Kreshnik/MMM-JokeAPI](https://github.com/Kreshnik/MMM-JokeAPI)



# Y

Appel de l'API en mode programmation: [https://yesno.wtf/api](https://yesno.wtf/api)

Réponse au format JSON:

{

  "answer": "yes",

  "forced": false,

  "image": "[https://yesno.wtf/assets/yes/11-a23cbde4ae018bbda812d2d8b2b8fc6c.gif](https://yesno.wtf/assets/yes/11-a23cbde4ae018bbda812d2d8b2b8fc6c.gif)"

}



Test:

$ curl [https://yesno.wtf/api](https://yesno.wtf/api) | jq 



jq formate correctement le json



# Nom du module

=> MMM-YesNoAPI



# Créer un répertoire avec le nom du module dans le répertoire module de MagicMirror



MagicMirror$ cd modules

MagicMirror/modules$ **mkdir MMM-YesNoAPI**

MagicMirror/modules$ **cd MMM-YesNoAPI**

MagicMirror/modules/MMM-YesNoAPI$ 



# Créer un fichier Javascript, point d'entrée du module qui a le même nom que le module

$** touch MMM-YesNoAPI.js**



# éditer le fichier pour ajouter les éléments suivants:



## enregistrement du module et définition des options par défaut:



    // Exemple de retour JSON de l'appel à l'API: [http://yesnot.wtf/api](http://yesnot.wtf/api)

    // {

    //  "answer": "yes",

    //  "forced": false,

    //  "image": "[https://yesno.wtf/assets/yes/13-c3082a998e7758be8e582276f35d1336.gif](https://yesno.wtf/assets/yes/13-c3082a998e7758be8e582276f35d1336.gif)"

    // }

    

    Module.register("MMM-YesNoAPI", {

        defaults: {

            // intervalle par défaut de rafraîchissement

            fetchInterval: 30 * 1000

        },

        getStyles() {

            return [

                this.file('style.css')

            ]

        },

        yesnoResponse: null,

        notificationReceived(notification, payload, sender) {

            if (notification === 'MODULE\_DOM\_CREATED') {

                this.getYesNoAnswer();

                setInterval(() => {

                    this.getYesNoAnswer()

                }, this.config.fetchInterval);

            }

        },

        getDom() {

            const wrapper = document.createElement("div");

    

            if(this.yesnoResponse === null) return wrapper;

    

            this.setupHTMLStructure(wrapper);

    

            return wrapper;

        },

        setupHTMLStructure(wrapper) {

            if (this.yesnoResponse.answer === 'yes') {

    

                const yesRender = document.createElement("img");

                yesRender.className = "yes no-wrap";

                yesRender.src = this.yesnoResponse.image;

                wrapper.appendChild(yesRender);

    

            } else if (this.yesnoResponse.answer === 'no') {

    

                const noRender = document.createElement("img");

                noRender.className = "no bright medium light no-wrap";

                noRender.src = this.yesnoResponse.image;

                wrapper.appendChild(noRender);

    

            }

            // il existe une troisième réponse 'maybe' que je vous laisse coder

        },

        getYesNoAnswer() {

                // requête HTTP sur l'URL de l'API

            fetch('[https://yesno.wtf/api](https://yesno.wtf/api)').then((response) => {

                // récupération de la réponse et transformation en JSON

                response.json().then((yesnoJSONresponse) => {

                         // la structure JSON est stockée dans notre variable locale au module

                    this.yesnoResponse = yesnoJSONresponse;

                    // demande de rafraîchissement de la page (du div)

                    this.updateDom();

                });

            });

        }

    });



## Appliquer un style CSS à notre image dans le div



# création d'un fichier style.css



.yes {

    animation-name: fadeIn;

    animation-duration: 1s;

    animation-fill-mode: both;

}

.no {

    animation-name: fadeIn;

    animation-duration: 7s;

    animation-fill-mode: both;

}

@keyframes fadeIn {

    0% {opacity: 0;}

    100% {opacity: 1;}

}

DOM = Document Object Model



 {

                        module: "MMM-YesNoAPI",

                        position: "top\_right",

                        config: {

                                fetchInterval: 20 * 1000 

                        }

                }, },

              





# Revenir dans le répertoire de MagicMirror pour déclarer et configurer le module dans la configuration (fichier config/config.js)



ajouter le module MMM-YesNoAPI:

... // module précédent

                

// fin du tableau des modules

        ]



# vérifier la syntaxe

$ npm run config:check

...

[2020-11-27 16:37:28.325] [INFO]   Your configuration file doesn't contain syntax errors :)



# tester MagicMirror avec ce module

$ npm run start

...

[2020-11-27 16:37:48.332] [LOG]    Initializing new module helper ...

[2020-11-27 16:37:48.333] [LOG]    Module helper loaded: newsfeed

[2020-11-27 16:37:48.333] [LOG]    No helper found for module: MMM-YesNoAPI.

[2020-11-27 16:37:48.333] [LOG]    All module helpers loaded.

[2020-11-27 16:37:48.369] [LOG]    Starting server on port 8080 ... 

[2020-11-27 16:37:48.373] [LOG]    Server started ...

...

[2020-11-27 16:37:49.009] [INFO]   Checking git for module: MMM-YesNoAPI

...





sudo apt install linssid





## Samedi 21 novembre (visio)



Visio-conférence de 10h à 12h.



Suite atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)

   * Ajout d'une module externe (Third Party)
   * Démarrage automatique de l'application


Choix d'un module externe (qui marche) !

[https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules](https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules)



Autre 3rd party modules avec gestion de la bourse

<MM2>$ cd modules

$  git clone [https://github.com/hakanmhmd/MMM-Stock.git](https://github.com/hakanmhmd/MMM-Stock.git)



odifier la configuration:

$ **cd ..**

Editer la configuration (**geany**)

$ vi config/config.js

...

modules: [

...

        },

        {

                    module: "MMM-Stock",

                    position: "top\_left",

                    config: {

                            companies: ["MSFT", "GOOG", "ORCL", "FB", "AAPL"]

                    }

        },

]



$ npm run config:check



$ npm run start





Autre module avec installation des dépendances

<MM2>$ cd modules

$ git clone [https://github.com/normyx/MMM-Nantes-TAN.git](https://github.com/normyx/MMM-Nantes-TAN.git)

$ cd MMM-Nantes-TAN

$ npm install



# modifier la configuration:

$** cd ../..**

$ vi config/config.js

...

modules: [

...

        },

        {

            module: 'MMM-Nantes-TAN',

            position: 'top\_right',

            header: 'Metro/Bus Nantes',

            classes: "default everyone",

            config: {

                debug: false,

                showSecondsToNextUpdate:false,

                busStations: [

                    {arret: 'COMM', ligne:'C3', sens:'1', color:'blue'},

                    {arret: 'COMM', ligne:'1', sens:'1', color:'yellow', symbol:'subway'},

                    {arret: 'CDCO', ligne:'4', sens:'1', color:'purple', symbol:'bus'},

                    {arret: 'GMAR', ligne:'NL', sens:'1', color:'green', symbol:'ship'},

                    {arret: 'COMM', ligne:'1', sens:'1', color:'orange'},

                ],

            }

        },

]



Vérification du fichier de config.js:

$ npm run config:check



Démarrer le miroir:

$ npm run start



Il nous restera l'installation au démarrage de la RPi

   * PM2
   * Systemd


Programmation d'un module avec l'API: [https://yesno.wtf/api](https://yesno.wtf/api)



[https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules](https://github.com/MichMich/MagicMirror/wiki/3rd-Party-Modules)



[https://github.com/Kreshnik/MMM-JokeAPI](https://github.com/Kreshnik/MMM-JokeAPI)



//Flux rss Ouest France  (Jo)

title: "Ouest France",

url: "[https://www.ouest-france.fr/rss.xml?insee=FRA](https://www.ouest-france.fr/rss.xml?insee=FRA)"



A mettre dans le fichier config





## Samedi 14 novembre (visio)



Visio-conférence de 10h à 12h.



Atelier autour de la mise en oeuvre d'un miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)



$ mkdir travail

$ cd travail



Site du MagicMirror: [https://github.com/MichMich/MagicMirror](https://github.com/MichMich/MagicMirror)



Récupérer les sources de MagicMirror (MM2)

$ git clone [https://github.com/MichMich/MagicMirror.git](https://github.com/MichMich/MagicMirror.git)



Vérifier les outils (nodejs et npm):

$ node -v                        # version > 10

$ npm -v                         # version > 6



Installation de NodeJS et de NPM

$ sudo apt install nodejs npm



npm, trop vieux:

$ sudo npm i npm@latest -g 



Pour aller dans le répertoire de MagicMirror:

$ cd travail/MagicMirror



dans le répertoire MagicMirror :

$ more package.json



à partir des informations de package.json, le npm va installer les dépendences:

$ npm install



# préparer la configuration

$ cp config/config.js.sample config/config.js



# démarrage de l'application en mode "normal":





$ npm run start



# modifier la config

[https://docs.magicmirror.builders/modules/introduction.html](https://docs.magicmirror.builders/modules/introduction.html)



## ajouter un "hello world" module



$ vi config/config.js

...

modules: [

...

        },

        {

                module: "helloworld",

                position: "top\_right",

                config: {

                        // See 'Configuration options' for more information.

                        text: "Coucou le monde!"

                }

        },

]



Pour vérifier la configuration:

$ npm run config:check

    > magicmirror@2.13.0 config:check /home/pi/travail/MagicMirror

    > node js/check\_config.js

    [2020-11-14 11:40:40.012] [INFO]   Checking file...  /home/pi/travail/MagicMirror/config/config.js

    [2020-11-14 11:40:40.322] [INFO]   Your configuration file doesn't contain syntax errors :)





# démarrage de l'application avec la nouvelle configuration:

$ npm run start

# appuyer sur la touche [Alt] pour afficher la barre de menu pour quitter Electron



Autres modules disponibles et fournis par des tiers:

[https://github.com/MichMich/MagicMirror/wiki/3rd-party-modules](https://github.com/MichMich/MagicMirror/wiki/3rd-party-modules)





Gestion des écrans à la main:

[https://doc.ubuntu-fr.org/mu](h[]ttps://doc.ubuntu-fr.org/mu[])[] --right oflti-ecran[]

[https://troumad.developpez.com/linux/serveurx/xrandr/]([]https://troumad.developpez.com/linux/serveurx/xrandr/[])

[https://incenp.org/notes/2012/dualscreen-dynamic-configuration.html](https://incenp.org/notes/2012/dualscreen-dynamic-configuration.html)



$ xrandr



$ xrandr \

  --output LVDS1 --mode 800x600 \

  --output VGA1  --mode 800x600 --right-of LVDS1

  

  

 

## Samedi 7 novembre (visio)



Visio-conférence de 10h à 12h.



Présentation du matériel et des logiciels (suite)

   * connexion à distance
       * SSH
       * VNC (licence RPi)
       * SSH -X: ssh -X pi@192.168.2.101 (lancer une application graphique sur RPi, affichage à distance)


Protocole RDP (Windows)



Mise  jour distribution RaspberryPi OS (Raspbian):

   * sudo apt update
   * sudo apt upgrade
   * sudo apt autoremove
   * sudo apt autoclean


Vérification des process (applications qui tournent)

   *  top
   * htop
   * bpytop - sudo apt install bpytop


Taille du disque et place disponible sur une partition et/ou disque:

   * df -h .
   * pydf - sudo  apt-ge install pydf


Taille d'un répertoire:

   * du -sh .
   * duf - [https://github.com/muesli/duf](https://github.com/muesli/duf)


Application pour découverte automatique:

    DNS (Domain Name Server)

    RFC => standard

    mDNS (multicast DNS): [https://en.wikipedia.org/wiki/Multicast\_DNS](https://en.wikipedia.org/wiki/Multicast\_DNS)

    [https://www.journaldulapin.com/2015/08/31/acceder-au-raspberry-pi-via-bonjour/](https://www.journaldulapin.com/2015/08/31/acceder-au-raspberry-pi-via-bonjour/)



Rechercher un paquet:

   * dpkg -l | grep mdns
   * apt list --installed | grep paquet


Programmation Python:

python3



[https://fr.wikipedia.org/wiki/Erreur\_d%27arrondi](https://fr.wikipedia.org/wiki/Erreur\_d%27arrondi)

[https://fr.wikipedia.org/wiki/D%C3%A9cimal\_cod%C3%A9\_binaire](https://fr.wikipedia.org/wiki/D%C3%A9cimal\_cod%C3%A9\_binaire)

[https://fr.wikipedia.org/wiki/IEEE\_754](https://fr.wikipedia.org/wiki/IEEE\_754)

[https://fr.wikipedia.org/wiki/Virgule\_flottante](https://fr.wikipedia.org/wiki/Virgule\_flottante)



sudo apt install algobox

[https://trinket.io/]([]https://trinket.io/[])

[https://books.trinket.io/pfe/](https://books.trinket.io/pfe/) ## tuto python

[https://www.py4e.com/book.php](https://www.py4e.com/book.php)  ## PDF (anglais)



[https://pi-hole.net/](https://pi-hole.net/)



Simuler le miroir magique: mise en place des application: logiciels

Exemple: [https://www.framboise314.fr/magic-mirror/](https://www.framboise314.fr/magic-mirror/)



Serveur auto hébergé:

[https://yunohost.org/#/](https://yunohost.org/#/)



Références:

   * Présentation outils scientifiques: [https://cloud.lph.bzh/index.php/s/7FKbIcuIO3kYAKP](https://cloud.lph.bzh/index.php/s/7FKbIcuIO3kYAKP)
   * 



## Samedi 24 octobre



Présentation du matériel et des logiciels (suite)

Préparation de la carte SD pour le démarrage de la Raspberry Pi

   * Télécharger une distribution sur [https://www.raspberrypi.org/downloads/](https://www.raspberrypi.org/downloads/)
   * Prendre par exemple: **l'image Raspberry Pi OS: **[https://www.raspberrypi.org/downloads/raspberry-pi-os/](https://www.raspberrypi.org/downloads/raspberry-pi-os/)
   * Installer un utilitaire pour préparer la carte SD avec l'image téléchargée ci-dessus
       * Utilitaires: (**voir les références plus bas**)
           * Etcher: [https://www.balena.io/etcher/](https://www.balena.io/etcher/) (AppImage pour Linux 32 ou 64)
               * unzip balena-etcher-electron-1.5.109-linux-x64.zip
               * chmod +x balenaEtcher-1.5.109-x64.AppImage
               * Pour démarrer l'application:
                   * ./balenaEtcher-1.5.109-x64.AppImage
           * **Raspberry Pi Imager: **[https://www.raspberrypi.org/downloads/](https://www.raspberrypi.org/downloads/)  (ne marche pas chez moi sous Ubuntu 20.04)
               * Télécharger le paquet  **imager\_1.4\_amd64.deb** pour Ubuntu 20.04:
               * updsudo dpkg -i imager\_1.4\_amd64.deb
   * Démarrer l'utilitaire
       * Insérer la carte SD (tout ce qu'elle contient sera effacée (!) )
       * Sélectionner l'image qui a été téléchargée
       * Choisir le périphérique de destination (Carte SD)
       * Lancer la préparation
   * Une fois que l'opération est terminée, la carte SD est prête et contient deux partitions:
       * une partition de **boot** avec la config (config.txt), le noyau Linux, et les descriptions des composants matériels des cartes Raspberry Pi (fichiers suffixes DTB)
       * une partition **rootfs** avec le système de fichier ext4 qui contient la distribution **Raspberry Pi OS**, par exemple, si on a choisi cette image (cette partition contient le système d'exploitation (l'environnement et les applications) pour la Raspberry Pi)
   * Sauvegarde, il est intéressant de sauvegarder certains éléments des deux partitions, qui en cas de problème avec la carte, seront toujours en sécurité ailleurs:
       * la config (fichier **config.txt, commandline.txt** et tout ce qui a été ajouté d'utile sur cette partition: par exemple: fichier ssh (pour se rappeler de faire la config SSH)) de la partition **boot**
       * et sur la partition **rootfs**, tout ce qui a été utile au développement et à la configuration d'applications, par exemple: les fichiers dans le répertoire **/home/pi**, et quelques fichiers de config du répertoire **/etc**, et parfois des données du répertoire **/var.**


Démarrage de la Raspberry Pi:

   * Insérer la carte SD dans la Raspberry Pi
   * brancher, écran, clavier, mulot, alimentation
       * Framboises
       * Messages du noyau
       * Splash Screen
           * et au premier démarrage (pas de messages (!))
           * agrandissement de la partition **rootfs** pour prendre le reste de la place de la carte SD
           * et redimmensionnement du système de fichier ext4 sous jacent pour occuper le nouvel espace de la partition **rootfs.**
       * Démarrage de la console ou de l'environnement graphique suivant la distribution et l'image choisie.


Configuration au premier démarrage:

   * Donner un mot de passe
   * Choisir la localisation (France, Time Zone, type de clavier)
   * Choisir le réseau Wifi, si pas de connection filaire
   * Mise à jour du système 
       * mise à jour faite automatiquement sur le principe de: 
           * sudo apt update
           * sudo apt upgrade
       * et en option pour nettoyer si besoin:
           * sudo apt autoremove
           * 

   * C'est prêt
       * la Rapsberry Pi n'est pas à l'heure: elle ne contient pas par défaut de dispositif de gestion d'horloge avec alimentation secourue, elle se mettra à l'heure toute seule si elle est connectée à Internet en utilisant une application cliente NTP qui ira chercher l'heure sur un serveur: [https://fr.wikipedia.org/wiki/Network\_Time\_Protocol](https://fr.wikipedia.org/wiki/Network\_Time\_Protocol)
   * Pour changer cette configuration, il faut utiliser l'application **Configuration Raspberry Pi** (ou raspi-config en  console/ligne de commande)
       * Dans le menu de l'environnement graphique: selectionner 
       * ou en ligne de commande:
           * sudo **raspi-config**


Eteindre la Raspberry Pi:

   * Menu principal, choisir **déconnexion** et ensuite bouton **shutdown**
   * ou en utilisant un terminal shell
       * sudo shutdown -h now
           * -h: halt
           * now: maintenant


Connexion à distance en mode console (en utilisant SSH: secure shell):

   * Activation du serveur SSH côté Raspberry Pi
       * par le menu **Configuration Raspberry Pi** 
       * ou par l'application en ligne de commande **raspi-config** 
       * ou par configuration au démarrage (configuration sur la partition **boot**)
   * **Activation au démarrage**
       * insérer la carte SD sur votre PC Linux (ou Windows)
       * ajouter sur la partition **boot**, un fichier **ssh** (vide) pour signaler l'activation du serveur SSH
       * démonter les partitions boot et rootfs
       * récupérer la carte SD pour l'insérer dans la Raspberry Pi
       * démarrer la Rapsberry Pi
   * Connection **SSH**
       * sans écran et sans configuration spécifique du réseau (filaire ou sans fil), il n'est pas facile de savoir sur quelle adresse IP se trouve la Raspberry Pi pour pouvoir s'y connecter en SSH.
       * il est possible de scanner le réseau **local** (j'insiste: **réseau local**) pour essayer de trouver l'adresse IP de la Raspberry Pi
       * utilisation de l'utilitaire nmap (sous linux et apparemment existe aussi sous Windows) pour scanner le réseau local à la recherche de la Raspberry Pi
       * recherche du préfixe du réseau local:
           * sous linux, commande **ip** avec les paramètre **a **(addresse) et **s **(show)
               * ip a s
    1: lo:   inet 127.0.0.1/8 scope host lo ## adresse locale

    2: eno1: ## interface réseau filaire non connecté 

    3: wlp3s0: inet 192.168.1.105/24  ## interface réseau Wifi, adresse IP de la machine sur le réseau local

           * sous Windows, commande **ipconfig**


       * Mon adresse IP est **192.168.1.105/24**, et mon préfixe réseau local est **192.168.1.0/24**
       * scanner le réseau local en utilisant **nmap**:
           * sudo nmap **192.168.1.0/24**
    Nmap scan report for \_gateway (192.168.1.1)

    Host is up (0.042s latency).

    Not shown: 998 closed ports

    PORT     STATE SERVICE

    443/tcp  open  https

    5431/tcp open  park-agent

    MAC Address: xxxx (Cisco-Linksys)

    

    Nmap scan report for nas (192.168.1.42)

    Host is up (0.0057s latency).

    Not shown: 992 closed ports

    PORT     STATE SERVICE

    22/tcp   open  ssh

    

    Nmap scan report for pc portable (192.168.1.105)

    Host is up (0.0000030s latency).

    Not shown: 998 closed ports

    PORT    STATE SERVICE

    139/tcp open  netbios-ssn

    445/tcp open  microsoft-ds

           * avec le résultat de la requête précédente (fictif), on peut estimer que l'adresse IP de la Rapsberry Pi est **192.168.1.42** car c'est la seule adresse IP a avoir un **port 22** (**port logiciel** d'écoute par défaut du serveur SSH)
       * Connecion au compte **pi **de la Raspberry Pi à partir d'un PC distant sur le même réseau local en utilisant l'application **ssh**:
           * ssh pi@**192.168.1.42**
               * répondre yes à la première question (une seule fois)
               * donner le mot de passe
               * résultat: un shell ouvert sur la Raspbery Pi sur le compte pi
               * ensuite utilisation des commande pour lancer les applications non-graphiques sur la RaspBerry Pi
                   * exemple pour configurer la Raspberry Pi
                   * sudo raspi-config
               * éteindre la Rapsberry Pi à distance:
                   * sudo shutdown -h now
                   * fermeture de la session, la Rapsberry Pi s'éteint
       * Sous Windows connexion à la Raspberry Pi en utilisant le logiciel **Putty**: [https://www.putty.org/](https://www.putty.org/)


**Références**:

   * Qu'est ce qu'une partition: [https://fr.wikipedia.org/wiki/Partition\_(informatique)](https://fr.wikipedia.org/wiki/Partition\_(informatique))
   * Outil de gestion des partitions sous Linux, Gparted: [https://fr.wikipedia.org/wiki/GParted](https://fr.wikipedia.org/wiki/GParted)
       * installation: sudo apt install gparted
   * Qu'est ce qu'un système de fichier: [https://fr.wikipedia.org/wiki/Syst%C3%A8me\_de\_fichiers](https://fr.wikipedia.org/wiki/Syst%C3%A8me\_de\_fichiers)
   * Qu'est ce qu'un terminal: [https://fr.wikipedia.org/wiki/Terminal\_(informatique)](https://fr.wikipedia.org/wiki/Terminal\_(informatique))
       * Terminal virtuel: [https://fr.wikipedia.org/wiki/%C3%89mulateur\_de\_terminal](https://fr.wikipedia.org/wiki/%C3%89mulateur\_de\_terminal)
   * Qu'est ce qu'un Shell: [https://fr.wikipedia.org/wiki/Interface\_syst%C3%A8me](https://fr.wikipedia.org/wiki/Interface\_syst%C3%A8me)
       * Shell Unix: [https://fr.wikipedia.org/wiki/Shell\_Unix](https://fr.wikipedia.org/wiki/Shell\_Unix)
       * [https://fr.wikipedia.org/wiki/Shell\_Unix#Shells](https://fr.wikipedia.org/wiki/Shell\_Unix#Shells)
   * Qu'est ce qu'un réseau local: [https://fr.wikipedia.org/wiki/R%C3%A9seau\_local](https://fr.wikipedia.org/wiki/R%C3%A9seau\_local)
   * Qu'est ce qu'une adresse IP: [https://fr.wikipedia.org/wiki/Adresse\_IP](https://fr.wikipedia.org/wiki/Adresse\_IP)
   * Qu'est ce qu'un port logiciel: [https://fr.wikipedia.org/wiki/Port\_(logiciel)](https://fr.wikipedia.org/wiki/Port\_(logiciel))
   * SSH:  [https://fr.wikipedia.org/wiki/Secure\_Shell](https://fr.wikipedia.org/wiki/Secure\_Shell)
   * Putty: [https://fr.wikipedia.org/wiki/PuTTY](https://fr.wikipedia.org/wiki/PuTTY)
   * nmap: [https://fr.wikipedia.org/wiki/Nmap](https://fr.wikipedia.org/wiki/Nmap)




## Mardi 13 octobre



Introduction

Tour de table

Présentation du matériel et des logiciels



Références:

   * [https://www.raspberrypi.org/](https://www.raspberrypi.org/)
   * [https://www.framboise314.fr/](https://www.framboise314.fr/)
   * [https://inforef.be/swi/download/apprendre\_python3.pdf](https://inforef.be/swi/download/apprendre\_python3.pdf)
Achats:

   * [https://www.kubii.fr/](https://www.kubii.fr/)
   * [https://www.gotronic.fr/cat-cartes-raspberry-1413.htm](https://www.gotronic.fr/cat-cartes-raspberry-1413.htm)
   * [https://fr.rs-online.com/web/c/raspberry-pi-arduino-outils-de-developpement/boutique-raspberry-pi/](https://fr.rs-online.com/web/c/raspberry-pi-arduino-outils-de-developpement/boutique-raspberry-pi/)




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
