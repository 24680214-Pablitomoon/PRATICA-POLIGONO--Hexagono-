# PRATICA-POLIGONO--Hexagono-
Documentación en blender de como hacer un hexágono con python. 

Polígono en Blender con Python
Introducción

Un polígono en Blender puede generarse mediante código Python utilizando la API bpy. En este caso se crea un polígono 2D, calculando matemáticamente sus vértices mediante coordenadas polares convertidas a coordenadas cartesianas.
La figura se ubica en el plano XY, manteniendo una altura constante en el eje Z = 0, lo que garantiza que sea un objeto bidimensional.
Este programa trabaja directamente con mallas (meshes), que son la base de los objetos geométricos en Blender.
Cada malla está compuesta por:

Vértices → puntos en el espacio

Aristas → líneas que conectan vértices

Caras → superficies cerradas (no se usan en este caso)

En este código únicamente se utilizan vértices y aristas, sin caras, para mantener la figura en dos dimensiones.


## En este caso: Construcción de un Hexágono
Para este ejemplo se generará un hexágono, que es un polígono de 6 lados, utilizando un radio definido para determinar su tamaño.
## Explicación del Código
1️⃣ Importación de módulos
Explicación

Se importan los módulos necesarios:

bpy → Permite interactuar con Blender

math → Permite usar funciones matemáticas como seno, coseno y π

Código comentado
```Python
import bpy      # Módulo principal para interactuar con Blender
import math     # Módulo matemático para usar funciones trigonométricas
```
