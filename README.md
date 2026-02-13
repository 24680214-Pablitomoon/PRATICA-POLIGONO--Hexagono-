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
## Explicación del Código por bloques 
1️⃣ Importación de módulos

Se importan los módulos necesarios:

bpy → Permite interactuar con Blender

math → Permite usar funciones matemáticas como seno, coseno y π

Código:
```Python
import bpy      # Módulo principal para interactuar con Blender
import math     # Módulo matemático para usar funciones trigonométricas
```
2️⃣ Definición de la función

Se define una función llamada crear_poligono_2d que recibe tres parámetros:

nombre → Nombre del objeto

lados → Número de lados del polígono

radio → Distancia del centro a cada vértice

Esta función será la encargada de generar el polígono.

Código:
```Python
def crear_poligono_2d(nombre, lados, radio):
```
3️⃣ Creación de la malla y objeto

Se crea una nueva malla vacía y luego un objeto que la contiene.
Después se vincula el objeto a la colección actual para que aparezca en la escena.

Código:
```Python
    # Crear una nueva malla con el nombre indicado
    malla = bpy.data.meshes.new(nombre)
    
    # Crear un nuevo objeto que contenga la malla
    objeto = bpy.data.objects.new(nombre, malla)
    
    # Vincular el objeto a la colección actual para que sea visible
    bpy.context.collection.objects.link(objeto)
```
4️⃣ Creación de listas para vértices y aristas

Se crean dos listas vacías:

vertices → almacenará las coordenadas (x, y, z)

aristas → almacenará las conexiones entre vértices
```Python
    vertices = []
    aristas = []
```
5️⃣ Cálculo de los vértices

Se utiliza una fórmula trigonométrica:

𝑥 = 𝑟 cos(𝜃)
x = r cos(θ)
𝑦 = 𝑟 sin(𝜃)
y = r sin(θ)

Donde:

r es el radio

θ es el ángulo

2π representa 360°

Esto permite distribuir uniformemente los vértices alrededor del centro.

El valor de Z se fija en 0 para mantener el polígono en 2D.

Código:
```Python
    # Calcular los vértices del polígono
    for i in range(lados):
        angulo = 2 * math.pi * i / lados  # Dividir la circunferencia en partes iguales
        x = radio * math.cos(angulo)      # Coordenada X
        y = radio * math.sin(angulo)      # Coordenada Y
        vertices.append((x, y, 0))        # Z = 0 para mantenerlo en el plano XY
```

6️⃣ Creación de aristas

Se conectan los vértices consecutivos.

El operador módulo % permite que el último vértice se conecte con el primero, cerrando la figura.

Código:
```Python
    # Crear las aristas conectando los vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))  # Conectar el último con el primero
```
7️⃣ Cargar datos en la malla

Se envían los vértices y aristas a la malla mediante from_pydata() y luego se actualiza la geometría.
```Python
    # Asignar vértices y aristas a la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()
```
8️⃣ Limpieza de la escena
Se seleccionan todos los objetos y se eliminan para evitar duplicados.
```Python
# Seleccionar todos los objetos
bpy.ops.object.select_all(action='SELECT')

# Eliminar los objetos seleccionados
bpy.ops.object.delete(use_global=False)
```

9️⃣ Llamada a la función (Creación del hexágono)

Se ejecuta la función indicando:

Nombre → "Poligono2D"
Lados → 6 (hexágono)
Radio → 5
```Python
# Crear un hexágono de radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```

 ## Resultado Final

Después de ejecutar el script en la pestaña Scripting y presionar Run Script, se obtendrá un hexágono 2D dibujado en el plano XY.
La figura estará compuesta únicamente por:

6 vértices
6 aristas
Sin caras (estructura 2D)

## 📌 Código Completo Final 
```Python
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    
    # Crear nueva malla
    malla = bpy.data.meshes.new(nombre)
    
    # Crear objeto que contiene la malla
    objeto = bpy.data.objects.new(nombre, malla)
    
    # Vincular objeto a la escena
    bpy.context.collection.objects.link(objeto)
    
    vertices = []
    aristas = []
    
    # Calcular vértices usando trigonometría
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))  # Z=0 mantiene la figura en 2D
    
    # Crear aristas conectando vértices
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))
    
    # Cargar datos en la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

# Crear hexágono
crear_poligono_2d("Poligono2D", lados=6, radio=5)
```
## Captura de pantalla de la vizualización del código y el hexagono en blender.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2f82f738-e529-4a85-94b2-f1cbd936492d" />

## Captura de pantalla del código en blender.
<img width="1008" height="900" alt="image" src="https://github.com/user-attachments/assets/62fcfff7-d168-43a5-b618-bc5be5986fc8" />

## Captura de pantalla del hexagono en blender.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e74365f7-3683-4919-a371-b9ee7422ce80" />


