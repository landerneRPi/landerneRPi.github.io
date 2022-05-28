# Saison 2022

## Samedi 28 mai

Animation de 10h à 12h à la MPT.

En présentiel à la MPT.

Au programme:

   * Gestion du bluetooth (BT)


### Gestion du Bluetooth

Préparation de l'environnement

* installation entête:

```
sudo apt install libbluetooth-dev
```

* installation bibliothèque Python3

```
pip3 install pybluez
```

Installation d'un terminal bluetooth sur un smartphone ou une tablette Android (via [F-Droid](https://f-droid.org/) ou Google Play): exemple [Bluetooth Terminal](https://f-droid.org/fr/packages/ru.sash0k.bluetooth_terminal/)

Exemple: piloter les leds simulés (tkgpio) en utilisant des commandes venant d'un terminal bluetooth.

Code, fichier pilote_bt_led.py:
```
#!/usr/bin/env python3
"""
Test Bluetooth and Tkgpio
"""

import bluetooth
from tkgpio import TkCircuit

# initialize the circuit inside the GUI

configuration = {
    "width": 300,
    "height": 200,
    "leds": [
        {"x": 50, "y": 40, "name": "LED 1", "pin": 21},
        {"x": 100, "y": 40, "name": "LED 2", "pin": 22}
    ]
}

circuit = TkCircuit(configuration)
@circuit.run
def main ():
    
    # now just write the code you would use in a real Raspberry Pi
    
    from gpiozero import LED, PWMLED
    from time import sleep
    
    
    led1 = LED(21)
    led1.blink()
    led2 = PWMLED(22)
    led2.pulse()
   
    while True:
        server_sock = bluetooth.BluetoothSocket(bluetooth.RFCOMM)
        server_sock.bind(("", bluetooth.PORT_ANY))
        server_sock.listen(1)

        port = server_sock.getsockname()[1]

        uuid = "94f39d29-7d6d-437d-973b-fba39e49d4ee"

        bluetooth.advertise_service(server_sock, "SampleServer", service_id=uuid,
                            service_classes=[uuid, bluetooth.SERIAL_PORT_CLASS],
                            profiles=[bluetooth.SERIAL_PORT_PROFILE],
                            # protocols=[bluetooth.OBEX_UUID]
                            )

        print("Waiting for connection on RFCOMM channel", port)

        client_sock, client_info = server_sock.accept()
        print("Accepted connection from", client_info)

        try:
            while True:
                data = client_sock.recv(1024)
                if not data:
                    break
                print("Received", data)
                message = str(data, 'UTF-8')
                if message == "allumer":
                    print("Allumer la led")
                    led1.blink()
                if message == "stop":
                    print("Eteindre la led")
                    led1.off()
                # client_sock.send(data)
        except OSError:
            pass
    
        print("Disconnected.")

        client_sock.close()
        server_sock.close()
        print("All done.")
    # delay
    sleep(0.1)
```


Références:

* [Bluetooth](https://fr.wikipedia.org/wiki/Bluetooth)
* [Profiles Bluetooth](https://en.wikipedia.org/wiki/List_of_Bluetooth_profiles)
* [Un profile, une fonction](https://www.cnetfrance.fr/produits/bluetooth-un-profil-pour-une-fonction-1001647.htm)
* [Serial Port Profile](https://learn.sparkfun.com/tutorials/bluetooth-basics/bluetooth-profiles)


## Mardi 10 mai

Animation de 18h à 20h à la MPT.

En présentiel à la MPT.

Au programme:

   * GPIO Raspberry Pi
   * Gestion du PWM
       * Circuit réel avec la Raspberry Pi
   * Gestion du bluetooth (BT)

Commandes pour appairer deux appareils en utilisant le bluetooth:

```
# connaître les périphériques locaux
$ hciconfig

# contrôler l'appairage d'un appareil sur celui sur lequel on est:
$ bluetoothctl
> agent on
> scan on
> pair <device MAC address>
```

Références:

   * [Commandes Bluetooth pour Linux](https://doc.ubuntu-fr.org/bluetooth) 


## Samedi 23 avril

Animation de 10h à 12h à la MPT.

En présentiel à la MPT.

Au programme:

   * GPIO Raspberry Pi
   * Gestion du PWM (suite et fin)
       * Simulation
       * Circuit réel avec la Raspberry Pi

Exemple de code

```
from tkgpio import TkCircuit

# initialize the circuit inside the GUI

configuration = {
    "width": 300,
    "height": 200,
    "leds": [
        {"x": 50, "y": 40, "name": "LED 1", "pin": 21},
        {"x": 100, "y": 40, "name": "LED 2", "pin": 22}
    ]
}

circuit = TkCircuit(configuration)

@circuit.run
def main ():
    # le code est identique à une utilisation sur une vrai Raspberry Pi

    from gpiozero import LED, PWMLED
    from time import sleep

    led1 = LED(21)
    led1.blink()
    led2 = PWMLED(22)
    led2.pulse()

    while True:
        sleep(0.1)
```


Références:

   * [https://fritzing.org/](https://fritzing.org/)
   * [https://www.apprendre-en-ligne.net/crypto/passecret/ohm.html](https://www.apprendre-en-ligne.net/crypto/passecret/ohm.html)
   * [https://www.lenovo.com/fr/fr/laptops/legion-laptops/legion-5-series/Legion-5-Pro-16ACH6H/p/WMD00000468](https://www.lenovo.com/fr/fr/laptops/legion-laptops/legion-5-series/Legion-5-Pro-16ACH6H/p/WMD00000468)


## Mardi 12 avril

Animation de 18h à 20h à la MPT.

En présentiel à la MPT.

Au programme:

   * GPIO Raspberry Pi
   * Gestion du PWM
       * Simulation
       * Circuit réel avec la Raspberry Pi

Références:

   * Rétro Gaming: [https://magpi.raspberrypi.com/books/retro-gaming-raspberry-pi-2nd-edition](https://magpi.raspberrypi.com/books/retro-gaming-raspberry-pi-2nd-edition)
   * git clone [https://github.com/themagpimag/retro-gaming.git](https://github.com/themagpimag/retro-gaming.git)
   * pip3 install pgzero

## Samedi 26 mars

Animation de 10h à 12h à la MPT.

En présentiel à la MPT, avec Pass Vaccinal pour les adultes.

Au programme:

   * GPIO Raspberry Pi
   * Gestion du PWM

Installation TkGPIO:

```
$ pip3 install tkgpio
```

Code de test:

```
    from tkgpio import TkCircuit

    # initialize the circuit inside the GUI

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

    circuit = TkCircuit(configuration)

    @circuit.run
    def main ():
        # now just write the code you would use in a real Raspberry Pi

        from gpiozero import LED, Button
        from time import sleep

        led1 = LED(21)
        led1.blink()

        def button_pressed():

            print("button pressed!")
            led2.toggle()

        led2 = LED(22)
        button = Button(11)
        button.when_pressed = button_pressed

        while True:
            sleep(0.1)
```

Exemple code pour LED PWM:

```
    from tkgpio import TkCircuit

    # initialize the circuit inside the GUI

    configuration = {
        "width": 300,
        "height": 200,
        "leds": [
            {"x": 50, "y": 40, "name": "LED 1", "pin": 21},
            {"x": 100, "y": 40, "name": "LED 2", "pin": 22}
        ]
    }

    circuit = TkCircuit(configuration)

    @circuit.run
    def main ():

        # now just write the code you would use in a real Raspberry Pi

        from gpiozero import LED, PWMLED
        from time import sleep

        led1 = LED(21)
        led1.blink()
        led2 = PWMLED(22)
        led2.pulse()

        while True:
            sleep(0.1)
```

Création d'un environnement virtuel Python pour installer tkgpio.

```
$ sudo apt install python3-venv
$ python3 -m venv .
$ source .venv/bin/activate
$ pip install tkgpio
```

Références:

   * [https://www.gotronic.fr/art-kit-d-experimentation-vmp502-27002.htm](https://www.gotronic.fr/art-kit-d-experimentation-vmp502-27002.htm)
   * [https://www.dealabs.com/](https://www.dealabs.com/)
   * [https://github.com/wallysalami/tkgpio](https://github.com/wallysalami/tkgpio)
   * [https://github.com/commaai/openpilot](https://github.com/commaai/openpilot)


## Mardi 8 mars

Animation de 18h à 20h à la MPT.

En présentiel à la MPT, avec Pass Vaccinal pour les adultes.

Au programme:

   * GPIO Raspberry Pi


Installation de tkgpio:

```
$ pip3  install tkgpio
```

Tester si la bibliothèque tkgpio est bien installée:

```
$ python3
>>> import tkgpio
```

Utilisation d'un éditeur de texte pour Python:

* Thonny ou
* VS-Code.

Ajouter les dépendences pour l'exemple tkgpio:

```
$ pip install lirc
$ pip install Adafruit_CharLCD
$ pip install py_irsend
```

Références:

   * [https://github.com/wallysalami/tkgpio](https://github.com/wallysalami/tkgpio)


## Samedi 26 février

Animation de 10h à 12h à la MPT.

En présentiel à la MPT, avec Pass Vaccinal pour les adultes.

Au programme:

   * Jeu en Python avec Pygame
       * Sprites


Pour récupérer les sources avec git:

   * installation de git:

```
$ sudo apt install git
```

   * utilisation de git pour récupérer les sources

```
$ git clone https://github.com/landerneRPi/initiation-python.git
```

## Mardi 8 février

Animation de 18h à 20h à la MPT.

En présentiel à la MPT, avec Pass Vaccinal pour les adultes.

Au programme:

   * Jeu en Python avec Pygame
       * Sprites (en cours)
   * Raytracing
       * Exemple en Python
       * Explications

Exemple de code en Python pour faire du Raytracing simple:

```
import numpy as np
import matplotlib.pyplot as plt

def normalize(vector):
    return vector / np.linalg.norm(vector)

def reflected(vector, axis):
    return vector - 2 * np.dot(vector, axis) * axis

def sphere_intersect(center, radius, ray_origin, ray_direction):
    b = 2 * np.dot(ray_direction, ray_origin - center)
    c = np.linalg.norm(ray_origin - center) ** 2 - radius ** 2
    delta = b ** 2 - 4 * c
    if delta > 0:
        t1 = (-b + np.sqrt(delta)) / 2
        t2 = (-b - np.sqrt(delta)) / 2
        if t1 > 0 and t2 > 0:
            return min(t1, t2)
    return None

def nearest_intersected_object(objects, ray_origin, ray_direction):

    distances = [sphere_intersect(obj['center'], obj['radius'], ray_origin, ray_direction) for obj in objects]

    nearest_object = None

    min_distance = np.inf

    for index, distance in enumerate(distances):

        if distance and distance < min_distance:

            min_distance = distance

            nearest_object = objects[index]

    return nearest_object, min_distance

width = 300
height = 200

max_depth = 3

camera = np.array([0, 0, 1])

ratio = float(width) / height

screen = (-1, 1 / ratio, 1, -1 / ratio) # left, top, right, bottom

light = { 'position': np.array([5, 5, 5]), 'ambient': np.array([1, 1, 1]), 'diffuse': np.array([1, 1, 1]), 'specular': np.array([1, 1, 1]) }

objects = [
    { 'center': np.array([-0.2, 0, -1]), 'radius': 0.7, 'ambient': np.array([0.1, 0, 0]), 'diffuse': np.array([0.7, 0, 0]), 'specular': np.array([1, 1, 1]), 'shininess': 100, 'reflection': 0.5 },

    { 'center': np.array([0.1, -0.3, 0]), 'radius': 0.1, 'ambient': np.array([0.1, 0, 0.1]), 'diffuse': np.array([0.7, 0, 0.7]), 'specular': np.array([1, 1, 1]), 'shininess': 100, 'reflection': 0.5 },

    { 'center': np.array([-0.3, 0, 0]), 'radius': 0.15, 'ambient': np.array([0, 0.1, 0]), 'diffuse': np.array([0, 0.6, 0]), 'specular': np.array([1, 1, 1]), 'shininess': 100, 'reflection': 0.5 },

    { 'center': np.array([0, -9000, 0]), 'radius': 9000 - 0.7, 'ambient': np.array([0.1, 0.1, 0.1]), 'diffuse': np.array([0.6, 0.6, 0.6]), 'specular': np.array([1, 1, 1]), 'shininess': 100, 'reflection': 0.5 }
]

image = np.zeros((height, width, 3))

for i, y in enumerate(np.linspace(screen[1], screen[3], height)):

    for j, x in enumerate(np.linspace(screen[0], screen[2], width)):

        # screen is on origin
        pixel = np.array([x, y, 0])
        origin = camera
        direction = normalize(pixel - origin)
        color = np.zeros((3))
        reflection = 1

        for k in range(max_depth):

            # check for intersections
            nearest_object, min_distance = nearest_intersected_object(objects, origin, direction)

            if nearest_object is None:
                break

            intersection = origin + min_distance * direction

            normal_to_surface = normalize(intersection - nearest_object['center'])

            shifted_point = intersection + 1e-5 * normal_to_surface

            intersection_to_light = normalize(light['position'] - shifted_point)

            _, min_distance = nearest_intersected_object(objects, shifted_point, intersection_to_light)

            intersection_to_light_distance = np.linalg.norm(light['position'] - intersection)

            is_shadowed = min_distance < intersectio_to_light_distance

            if is_shadowed:
                break

            illumination = np.zeros((3))

            # ambiant
            illumination += nearest_object['ambient'] * light['ambient']

            # diffuse
            illumination += nearest_object['diffuse'] * light['diffuse'] * np.dot(intersection_to_light, normal_to_surface)

            # specular
            intersection_to_camera = normalize(camera - intersection)

            H = normalize(intersection_to_light + intersection_to_camera)

            illumination += nearest_object['specular'] * light['specular'] * np.dot(normal_to_surface, H) ** (nearest_object['shininess'] / 4)

            # reflection
            color += reflection * illumination

            reflection *= nearest_object['reflection']

            origin = shifted_point

            direction = reflected(direction, normal_to_surface)

        image[i, j] = np.clip(color, 0, 1)

    print("%d/%d" % (i + 1, height))

plt.imsave('image.png', image)
```

Autre exemple de Raytracing en Python:

```
from PIL import Image
from functools import reduce
import numpy as np
import time
import numbers

def extract(cond, x):
    if isinstance(x, numbers.Number):
        return x
    else:
        return np.extract(cond, x)

class vec3():
    def __init__(self, x, y, z):
        (self.x, self.y, self.z) = (x, y, z)

    def __mul__(self, other):
        return vec3(self.x * other, self.y * other, self.z * other)

    def __add__(self, other):
        return vec3(self.x + other.x, self.y + other.y, self.z + other.z)

    def __sub__(self, other):
        return vec3(self.x - other.x, self.y - other.y, self.z - other.z)

    def dot(self, other):
        return (self.x * other.x) + (self.y * other.y) + (self.z * other.z)

    def __abs__(self):
        return self.dot(self)

    def norm(self):
        mag = np.sqrt(abs(self))
        return self * (1.0 / np.where(mag == 0, 1, mag))

    def components(self):
        return (self.x, self.y, self.z)

    def extract(self, cond):
        return vec3(extract(cond, self.x),

                 extract(cond, self.y),

                    extract(cond, self.z))

    def place(self, cond):
        r = vec3(np.zeros(cond.shape), np.zeros(cond.shape), np.zeros(cond.shape))

        np.place(r.x, cond, self.x)

        np.place(r.y, cond, self.y)

        np.place(r.z, cond, self.z)
        return r

rgb = vec3

(w, h) = (400, 300)         # Screen size
L = vec3(5, 5, -10)        # Point light position
E = vec3(0, 0.35, -1)     # Eye position

FARAWAY = 1.0e39            # an implausibly huge distance

def raytrace(O, D, scene, bounce = 0):

    # O is the ray origin, D is the normalized ray direction

    # scene is a list of Sphere objects (see below)

    # bounce is the number of the bounce, starting at zero for camera rays

    distances = [s.intersect(O, D) for s in scene]

    nearest = reduce(np.minimum, distances)
    color = rgb(0, 0, 0)

    for (s, d) in zip(scene, distances):
        hit = (nearest != FARAWAY) & (d == nearest)

        if np.any(hit):
            dc = extract(hit, d)
            Oc = O.extract(hit)
            Dc = D.extract(hit)
            cc = s.light(Oc, Dc, dc, scene, bounce)
            color += cc.place(hit)
    return color

class Sphere:

    def __init__(self, center, r, diffuse, mirror = 0.5):
        self.c = center
        self.r = r
        self.diffuse = diffuse
        self.mirror = mirror

    def intersect(self, O, D):
        b = 2 * D.dot(O - self.c)
        c = abs(self.c) + abs(O) - 2 * self.c.dot(O) - (self.r * self.r)
        disc = (b ** 2) - (4 * c)
        sq = np.sqrt(np.maximum(0, disc))
        h0 = (-b - sq) / 2
        h1 = (-b + sq) / 2
        h = np.where((h0 > 0) & (h0 < h1), h0, h1)
        pred = (disc > 0) & (h > 0)
        return np.where(pred, h, FARAWAY)

    def diffusecolor(self, M):
        return self.diffuse

    def light(self, O, D, d, scene, bounce):
        M = (O + D * d)                         # intersection point
        N = (M - self.c) * (1. / self.r)        # normal
        toL = (L - M).norm()                    # direction to light

        toO = (E - M).norm()                    # direction to ray origin

        nudged = M + N * .0001                  # M nudged to avoid itself
        # Shadow: find if the point is shadowed or not.

        # This amounts to finding out if M can see the light

        light_distances = [s.intersect(nudged, toL) for s in scene]

        light_nearest = reduce(np.minimum, light_distances)

        seelight = light_distances[scene.index(self)] == light_nearest

        # Ambient
        color = rgb(0.05, 0.05, 0.05)
        # Lambert shading (diffuse)
        lv = np.maximum(N.dot(toL), 0)
        color += self.diffusecolor(M) * lv * seelight
        # Reflection
        if bounce < 2:
            rayD = (D - N * 2 * D.dot(N)).norm()
            color += raytrace(nudged, rayD, scene, bounce + 1) * self.mirror

        # Blinn-Phong shading (specular)
        phong = N.dot((toL + toO).norm())
        color += rgb(1, 1, 1) * np.power(np.clip(phong, 0, 1), 50) * seelight
        return color

class CheckeredSphere(Sphere):

    def diffusecolor(self, M):
        checker = ((M.x * 2).astype(int) % 2) == ((M.z * 2).astype(int) % 2)
        return self.diffuse * checker

scene = [
    Sphere(vec3(.75, .1, 1), .6, rgb(0, 0, 1)),
    Sphere(vec3(-.75, .1, 2.25), .6, rgb(.5, .223, .5)),
    Sphere(vec3(-2.75, .1, 3.5), .6, rgb(1, .572, .184)),
    CheckeredSphere(vec3(0,-99999.5, 0), 99999, rgb(.75, .75, .75), 0.25),
]

r = float(w) / h

# Screen coordinates: x0, y0, x1, y1.

S = (-1, 1 / r + .25, 1, -1 / r + .25)

x = np.tile(np.linspace(S[0], S[2], w), h)

y = np.repeat(np.linspace(S[1], S[3], h), w)

t0 = time.time()
Q = vec3(x, y, 0)
color = raytrace(E, (Q - E).norm(), scene)
print ("Took", time.time() - t0)

rgb = [Image.fromarray((255 * np.clip(c, 0, 1).reshape((h, w))).astype(np.uint8), "L") for c in color.components()]

Image.merge("RGB", rgb).save("rt3.png")
```

Références:

   * [https://www.frandroid.com/dossiers/660693\_dossier-ray-tracing-explication](https://www.frandroid.com/dossiers/660693\_dossier-ray-tracing-explication)
   * [https://fr.wikipedia.org/wiki/Optique](https://fr.wikipedia.org/wiki/Optique)
   * [https://fr.wikipedia.org/wiki/Ray\_tracing](https://fr.wikipedia.org/wiki/Ray\_tracing)
   * [https://fr.wikipedia.org/wiki/Infographie](https://fr.wikipedia.org/wiki/Infographie)
   * [https://www.blender.org/](https://www.blender.org/)

## Samedi 22 janvier

Animation de 10h à 12h à la MPT.

En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.

Au programme:

   * Jeu en Python avec Pygame
       * Sprites


Site Github de l'atelier:

    [https://github.com/landerneRPi](https://github.com/landerneRPi)

Références:

   * [https://fr.wikipedia.org/wiki/OpenGL](https://fr.wikipedia.org/wiki/OpenGL)
   * [https://fr.wikipedia.org/wiki/Vulkan\_(API)](https://fr.wikipedia.org/wiki/Vulkan\_(API))
   * [https://medium.com/swlh/ray-tracing-from-scratch-in-python-41670e6a96f9](https://medium.com/swlh/ray-tracing-from-scratch-in-python-41670e6a96f9)
   * [https://learnopengl.com/book/book\_pdf.pdf](https://learnopengl.com/book/book\_pdf.pdf)
   * [https://github.com/openglbook](https://github.com/openglbook)
   * [https://www.cs.utexas.edu/users/fussell/courses/cs354/handouts/Addison.Wesley.OpenGL.Programming.Guide.8th.Edition.Mar.2013.ISBN.0321773039.pdf](https://www.cs.utexas.edu/users/fussell/courses/cs354/handouts/Addison.Wesley.OpenGL.Programming.Guide.8th.Edition.Mar.2013.ISBN.0321773039.pdf)
   * [https://fr.wikipedia.org/wiki/Preuve\_de\_travail](https://fr.wikipedia.org/wiki/Preuve\_de\_travail)
   * [https://fr.wikipedia.org/wiki/Preuve\_d%27enjeu](https://fr.wikipedia.org/wiki/Preuve\_d%27enjeu)
   * [https://cardano.org/](https://cardano.org/)

## Mardi 11 janvier

Animation de 18h à 20h à la MPT.

En présentiel à la MPT, avec Pass Sanitaire ou test négatif pour les adultes.

Au programme:

   * Jeu en Python avec PyGame (suite), déplacement du vaisseau

[https://www.wallpaperflare.com/search?wallpaper=ubuntu](https://www.wallpaperflare.com/search?wallpaper=ubuntu)

Suite de l'exemple:

```
        if event.type == pygame.KEYDOWN and event.key == pygame.K_c:
            ligne = 1
            for colonne in range(15):
                #  x, y
                aliens.append(Alien(screen, (colonne*40) + 30, (ligne *40) + 30))
```

Références:

   * [https://www.pygame.org/news](https://www.pygame.org/news)
   * [https://www.pygame.org/wiki/GettingStarted](https://www.pygame.org/wiki/GettingStarted)
   * [https://htmlcolorcodes.com/fr/](https://htmlcolorcodes.com/fr/)
