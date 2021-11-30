# PINGPONG
Reto compartido: El juego del Ping Pong

@ESTHERRODRIGUEZGARCIA, @tereesaalvarez, @Barroso03 

En este repositorio se va a resolver el juego de "Ping Pong". La tarea consiste en trabajar de forma conjunta con un repositorio compartido donde al menos se mostrarán 10 commits, 10 miltones y 5 proyects en el repositorio conjunto con varias ramas por persona y realizar la tarea pendiente que se presenta al final del documento.

Historia de Pong

Aunque desde la aparición de los ordenadores programables en los años 40 del siglo XX se han escrito programas que podían considerarse juegos, se suele considerar que el primer videojuego fue Computer Tennis. Este videojuego fue creado en 1958 para la exposición anual del Laboratorio Nacional de Brookhaven (EEUU) y simulaba un pista de tenis vista lateralmente. El juego se visualizaba en la pantalla de un osciloscopio y se convirtió en la mayor atracción de esa exposición. Aunque al año siguiente la exposición contó con una versión mejorada, tras ella el equipo se desmontó para reutilizar los componentes en el Laboratorio.

Bastante años después, en septiembre de 1972, se comercializó la primera videoconsola de la historia dirigida a los hogares, Magnavox Odyssey. Esta videoconsola se conectaba a una pantalla de televisor y uno de los juegos incluidos era Table Tennis. En este juego cada jugador controlaba una paleta que golpeaba una pelota. El mismo año, pero en noviembre, la compañía Atari comercializó Pong, una de las primeras máquinas de arcade, destinadas a lugares públicos.

Pong, el videojuego
![image](https://user-images.githubusercontent.com/91721860/144032828-0a749965-6164-4954-a12b-ebad2d63ef58.png)

Con Pong, un juego trivial para los estándares actuales, empezaba la era moderna de los videojuegos. Pong es un juego de deportes en dos dimensiones que simula un tenis de mesa. El jugador controla en el juego una paleta moviéndola verticalmente en la parte izquierda de la pantalla, y puede competir tanto contra un oponente controlado por computadora, como con otro jugador humano que controla una segunda paleta en la parte opuesta. Los jugadores pueden usar las raquetas para pegarle a la pelota hacia un lado u otro. El objetivo consiste en que uno de los jugadores consiga más puntos que el oponente al finalizar el juego. Estos puntos se obtienen cuando el jugador adversario falla al devolver la pelota.

La palabra Pong es una marca registrada por Atari Interactive (aunque la patente del juego la tuvo la empresa de Magnavox Odyssey), pero la palabra genérica "pong" se usa para describir el género de videojuegos.

Por todo ello, cuando se aprende a programar videojuegos, es habitual comenzar programando un juego como Pong, por su sencillez y también como homenaje al gran clásico.


  Realización del programa
  Vamos a programar un juego de Pong en el que una de las raquetas esté controlada por el jugador humano mediante el teclado y la otra raqueta esté contralada por el propio programa.

  Para la realización del juego Pong, iremos por fases, implementando en cada paso uno de los elementos del programa.
 
# TAREA 0: 
  Instalación de pygame
  
  0.1 Abra una ventana de terminal y escriba los siguientes comandos.
  
  0.2 Actualice pip:
  
      python -m pip install --upgrade pip
      
  0.3 Instale pygame:
  
      pip install pygame
      
# PASO 1: Ventana de juego

El juego se ejecutará en una ventana independiente. Para crear la ventana, necesitamos bastante código específico de pygame, que no es necesario conocer de memoria, ya que lo podemos reutilizar de un proyecto a otro.

El siguiente programa genera una ventana en blanco con el título del juego, similar a la captura siguiente (la ventana está recortada en la captura).

![image](https://user-images.githubusercontent.com/91721860/144035929-2c8b016e-2b0c-4c2c-a693-6a31dd0dacd6.png)
```
# pong_1_1.py: Ventana de juego
import pygame
from pygame.locals import QUIT

# Constantes para la inicialización de la superficie de dibujo
VENTANA_HORI = 800  # Ancho de la ventana
VENTANA_VERT = 600  # Alto de la ventana
FPS = 60  # Fotogramas por segundo
BLANCO = (255, 255, 255)  # Color del fondo de la ventana (RGB)

def main():
    # Inicialización de Pygame
    pygame.init()

    # Inicialización de la superficie de dibujo (display surface)
    ventana = pygame.display.set_mode((VENTANA_HORI, VENTANA_VERT))
    
    pygame.display.set_caption("Pong 1")

    # Bucle principal
    jugando = True
    
    while jugando:
        ventana.fill(BLANCO)

        for event in pygame.event.get():
            if event.type == QUIT:
                jugando = False

        pygame.display.flip()
        pygame.time.Clock().tick(FPS)

    pygame.quit()


if __name__ == "__main__":
    main()
```

Cada una de las instrucciones tiene una función específica, que se comenta a continuación:

-> Importación de módulos
```
  import pygame
  from pygame.locals import *
  ```
  Importamos los módulos pygame. Para que al hacer referencia en el programa a las constantes de pygame no tengamos que incluir el nombre del módulo, las importamos todas del módulo pygame.locals.

 -> Definición de constantes
  ´´´
  #Constantes para la inicialización de la superficie de dibujo
  VENTANA_HORI = 800  # Ancho de la ventana
  VENTANA_VERT = 600  # Alto de la ventana
  FPS = 60  # Fotogramas por segundo
  BLANCO = (255, 255, 255)  # Color del fondo de la ventana (RGB)
  ```
  Python no tiene un tipo de dato "constante" (es decir, un valor que no se pueda modificar). La costumbre, heredada de otros lenguajes, es simplemente escribir el nombre de una variable en mayúsculas para indicar a quien lea nuestro código fuente que esa variable no se va a modificar en ningún momento del programa. Definimos así varias constantes:

  ·El tamaño de la ventana de juego (en este caso, 800 x 600 px, la llamada resolución SVGA original).
  ·Normalmente FPS hace referencia al número de veces por segundo que se actualiza la imagen en la ventana. En principio, cuanto más alto es ese valor, mejor se verán los objetos en movimiento, aunque cada pantalla admite un valor máximo y dependiendo de la complejidad de la creación de la imagen puede que no se puedan alcanzar valores muy altos. En pygame, la ventana se está actualizando constantemente y en cada actualización los objetos se desplazan, por lo que si la ventana se actualiza demasiadas veces, los objetos se desplazarán demasiado rápido. Para evitarlo, en pygame FPS significa el número máximo de veces que queremos que se actualice la ventana, aunque si debido a la complejidad de la imagen el número de veces que se actualiza la imagen es inferior, pygame no podrá alcanzarlo.
  ·En pygame los colores se indican mediante códigos RGB, así que definimos una constante con el nombre del color para facilitar su referencia.
  
  ->Inicialización
     ```
     # Inicialización de Pygame
      pygame.init()

      # Inicialización de la superficie de dibujo (display surface)
      ventana = pygame.display.set_mode((VENTANA_HORI, VENTANA_VERT))
      pygame.display.set_caption("Pong 1")
      ´´´
  Con estas instrucciones:

  ·Inicializamos pygame.
  ·Creamos el objeto ventana que nos permite acceder al contenido de la ventana (al crearlo, le indicamos su tamaño).
  ·Le damos un título a la ventana.
  
  ->Bucle principal
  ```
      # Bucle principal
      jugando = True
      while jugando:
          ventana.fill(BLANCO)

          for event in pygame.event.get():
              if event.type == QUIT:
                  jugando = False

          pygame.display.flip()
          pygame.time.Clock().tick(FPS)

      pygame.quit()
      ´´´
  El bucle principal se ejecuta continuamente:

  ·línea 22: La variable lógica jugando controlará la repetición del bucle. Inicialmente, la variable tiene el valor True.
  ·línea 23: Mientras se mantenga ese valor, el bucle se repetirá.
  ·línea 24: En cada iteración pintamos la pantalla de blanco para borrar los elementos de la imagen anterior (en este programa todavía no ha elementos, pero podemos añadir ya esta instrucción).
  ·líneas 26 a 28: Las pulsaciones de tecla o del ratón se reciben en forma de eventos.
    -línea 26: El bucle for recorre en cada iteración los eventos recibidos
    -línea 27: Si el evento es de tipo QUIT (es decir, que se ha cerrado la ventana del juego) ...
    -línea 28: La variable jugando pasa a False, por lo que el bucle while no se volverá a ejecutar.
  ·línea 30: Todos los elementos de la pantalla se vuelven a dibujar (en este programa todavía no ha elementos, pero podemos añadir ya esta instrucción).
  ·línea 31: Con esta instrucción pygame comprueba que la ejecución se mantiene en el número de FPS y no va demasiado rápida.
  ·línea 33: Si hemos salido del bucle es que se ha cerrado la ventana, así que con esta instrucción le pedimos a pygame que cierre todos sus procesos.


# PASO 2: Clase PelotaPong
El primer elemento del juego que programaremos será la pelota. Para definir la pelota crearemos una clase a la que llamaremos PelotaPong. Las clases son propias de la programación orientada a objetos y permiten ampliar los tipos de datos del lenguaje. Una vez definida la clase, podemos crear tantas variables de esa clase como queramos (por ejemplo, una o varias pelotas, en el caso de que quisiéramos jugar con varias pelotas a la vez).

El siguiente programa dibuja una pelota cuadrada de color rojo en el centro de la ventana y la desplaza en línea recta en una de las cuatro direcciones diagonales. Cuando llega al borde de la ventana, la pelota deja de verse aunque sigue moviéndose indefinidamente en la misma dirección.
![image](https://user-images.githubusercontent.com/91721860/144065171-611d65b9-3a4c-474e-ac7c-d97dcd2215b0.png)

Para situar los objetos en la ventana pygame utiliza un sistema de coordenadas cartesianas en el que el origen se encuentran en la esquina superior izquierda de la ventana y en el que el eje vertical está dirigido hacia abajo. De esta manera, los valores de las coordenadas serán siempre positivos: cuanto mayor sea la coordenada x más a la derecha estará el objeto y cuanto mayor sea la coordenada y más hacia abajo estará el objeto. Si se asignan valores negativos o mayores que el tamaño de la ventana, no se produce ningún error, pero el objeto simplemente no se verá (dependiendo del tamaño que tenga y de los valores utilizados, el objeto puede verse parcialmente).

```
# pong_1_2.py: Clase PelotaPong

import random
import pygame
from pygame.locals import QUIT

# Constantes para la inicialización de la superficie de dibujo
VENTANA_HORI = 800  # Ancho de la ventana
VENTANA_VERT = 600  # Alto de la ventana
FPS = 60  # Fotogramas por segundo
BLANCO = (255, 255, 255)  # Color del fondo de la ventana (RGB)


class PelotaPong:
    def __init__(self, fichero_imagen):
        # --- Atributos de la Clase ---

        # Imagen de la Pelota
        self.imagen = pygame.image.load(fichero_imagen).convert_alpha()

        # Dimensiones de la Pelota
        self.ancho, self.alto = self.imagen.get_size()

        # Posición de la Pelota
        self.x = VENTANA_HORI / 2 - self.ancho / 2
        self.y = VENTANA_VERT / 2 - self.alto / 2

        # Dirección de movimiento de la Pelota
        self.dir_x = random.choice([-5, 5])
        self.dir_y = random.choice([-5, 5])

    def mover(self):
        self.x += self.dir_x
        self.y += self.dir_y


def main():
    # Inicialización de Pygame
    pygame.init()

    # Inicialización de la superficie de dibujo (display surface)
    ventana = pygame.display.set_mode((VENTANA_HORI, VENTANA_VERT))
    pygame.display.set_caption("Pong 2")

    pelota = PelotaPong("bola_roja.png")

    # Bucle principal
    jugando = True
    while jugando:
        pelota.mover()

        ventana.fill(BLANCO)
        ventana.blit(pelota.imagen, (pelota.x, pelota.y))

        for event in pygame.event.get():
            if event.type == QUIT:
                jugando = False

        pygame.display.flip()
        pygame.time.Clock().tick(FPS)

    pygame.quit()


if __name__ == "__main__":
    main()
    ```
Las instrucciones añadidas con respecto al paso 1 son las siguientes:
    
->Importación de módulos
```
import random
```
Importamos el módulo random, que utilizaremos en el programa.

->Clase PelotaPong
class PelotaPong:
    def __init__(self, fichero_imagen):
        # --- Atributos de la Clase ---

        # Imagen de la Pelota
        self.imagen = pygame.image.load(fichero_imagen).convert_alpha()

        # Dimensiones de la Pelota
        self.ancho, self.alto = self.imagen.get_size()

        # Posición de la Pelota
        self.x = VENTANA_HORI / 2 - self.ancho / 2
        self.y = VENTANA_VERT / 2 - self.alto / 2

        # Dirección de movimiento de la Pelota
        self.dir_x = random.choice([-5, 5])
        self.dir_y = random.choice([-5, 5])

    def mover(self):
        self.x += self.dir_x
        self.y += self.dir_y
````
En la definición de una clase se definen los atributos y los métodos de la clase. Los atributos son variables que van asociadas automáticamente a los objetos. Los métodos son funciones que se pueden aplicar a los objetos. En la definición de la clase para hacer referencia a que los atributos son los del propio objeto se indica con self.
    
    
    
