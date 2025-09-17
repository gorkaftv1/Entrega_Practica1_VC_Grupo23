# Práctica 1: Procesamiento básico y Configuración del entorno

## Descripción

En esta práctica hemos realizado algunas tareas de procesamiento de imágenes usando las herramientas de opencv y matplotlib.

## Autores

- **Wail Ben El Hassane Boudhar**
- **Gorka Eymard Santana Cabrera**

## Requisitos

Como se nos enseña al inicio del guión de la práctica, debemos configurar un entorno de python aislado con **Conda Prompt** en el que instalemos los siguiente paquetes:
- **opencv-python**
- **numpy**
- **matplotlib**

Para ello usamos la herramienta de instalación **pip**.

A continuación configuramos visualstudio para usar el kernel que hemos configurado.

## Desarollo

### Tarea 1: Crear una imagen con la textura de un tablero de ajedrez
- **Descripción**: Se crea una imagen en color (200x200 píxeles) simulando un patrón similar a un tablero de ajedrez, pero con rectángulos y líneas personalizadas.
- **Implementación**:
- Se recorre la imagen pintando en cada paso las casillas blancas intercaladas, dejando un 2x2 de 
    - [blanco, negro]
    - [negro, blanco]
- Visualización con Matplotlib (`plt.imshow` y `plt.show`).

### Tarea 2: Crear una imagen estilo Mondrian
- **Descripción**: usando las funciones de OpenCV crear una imagen estilo Mondrian.
- **Implementación**:
- Basándonos en la imagen de ejemplo https://www3.gobiernodecanarias.org/medusa/ecoescuela/sa/2017/04/17/descubriendo-a-mondrian/
- Definiendo un fondo negro, añadimos sobre el varios retángulos de distintos colores y tamaños en diversas posiciones y algunas para líneas negras de distintos grosores para delimitarlos.



### Tarea 3: Modificar de forma libre los valores de un plano de la imagen
- **Descripción**: Modificar un canal de color en tiempo real desde la webcam.
- **Implementación**:
- Captura de vídeo con `cv2.VideoCapture`.
-  Se ha modificado uno de los planos invirtiendo sus colores, y el otro aumento el color de dichos planos. 
- **Resultado**: El efecto obtenido es un collage de 3 frames con colores invertidos

### Tarea 4: Pintar círculos en las posiciones del píxel más claro y oscuro de la imagen
- **Descripción**: Detectar y marcar píxeles claros (luminosidad > 200) y oscuros (luminosidad < 50) con círculos. Se propone una variante por bloques de 8x8 (aproximado a 50x50 para simplicidad).
- **Implementación**:
- **Por píxeles** :
- Convierte cada fotograma de la webcam a escala de grises (`cv2.cvtColor`).
- Obtiene el píxel más claro y el más oscuro de toda la imagen usando `cv2.minMaxLoc`, que devuelve los valores mínimo y máximo de intensidad junto con sus posiciones.
- Dibuja un círculo **rojo** sobre el píxel más claro y un círculo **azul** sobre el píxel más oscuro en el fotograma original (`cv2.circle`).
- Muestra el vídeo en tiempo real con las marcas superpuestas y permite salir pulsando **ESC**.

- **Por bloques**: 
- Divide la imagen en bloques de 50x50, calcula la media de luminosidad por bloque, y dibuja círculos en el bloque más claro (verde) y oscuro (negro).
- Uso de `cv2.cvtColor` para gris, `np.where` para posiciones, y `cv2.circle` para dibujar.
- **Resultado**: Vídeo en tiempo real con círculos superpuestos. Detener con ESC.

### Tarea 5: Llevar a cabo tu propuesta de Pop-Art
- **Descripción**: Crear un efecto Pop-Art inspirado en Andy Warhol, dividiendo la imagen de la webcam en un collage de 2x2 con manipulaciones de color y un mosaico de triángulos en una de las secciones.
- **Implementación**:
- Captura de vídeo con `cv2.VideoCapture` y reducción de resolución a la mitad para optimizar la visualización.
- Creación de un collage de 2x2 con cuatro subimágenes (arriba-izquierda, arriba-derecha, abajo-izquierda, abajo-derecha).
- Manipulación de canales RGB:
 - Arriba-izquierda: Imagen original (RGB sin cambios).
 - Arriba-derecha: Inversión del canal rojo (`255 - r`), canal verde modificado (`96 - g`), y canal azul ajustado (`55 + b`).
 - Abajo-izquierda: Imagen original, pero con un mosaico de triángulos de 4x4 píxeles creado con `cv2.fillPoly`, donde cada triángulo usa el color del píxel en la esquina superior izquierda del bloque.
 - Abajo-derecha: Inversión de los canales rojo (`255 - r`) y verde (`96 - g`), manteniendo el canal azul original.
- Visualización en tiempo real del collage.
- **Resultado**: Un collage en tiempo real con efectos de color vibrantes y un mosaico triangular que se asimila al estilo Pop-Art. Detener con ESC.

## Webgrafía:

https://www.geeksforgeeks.org/python/python-opencv-cv2-rectangle-method/
https://pyimagesearch.com/2014/09/29/finding-brightest-spot-image-using-python-opencv/

