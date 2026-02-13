# como-realizar-un-pol-gono-en-2d-paso-a-paso-en-blender-
paso a paso de como realizar un poligono en 2d en blender 
Instalación de Blender
Primero lo primero, necesitamos el entorno de trabajo.
Descarga: Ve a la página oficial blender.org y baja la versión más reciente (la LTS es la más estable para proyectos escolares).
<img width="921" height="193" alt="image" src="https://github.com/user-attachments/assets/02586cc2-0773-45df-97de-b0039c557d21" />

Instalación: Sigue el asistente típico. En Windows es "Next, Next, Finish". En Linux lo puedes bajar por terminal o Flatpak, pero el ejecutable directo funciona de lujo.

Primer inicio: Al abrirlo, selecciona tu idioma y la configuración de "Select with Left Click" (es el estándar moderno).

Preparando el Entorno de Scripting
Blender tiene un IDE (entorno de desarrollo) integrado que es donde vamos a meter el código de la imagen.
En la barra superior de pestañas (donde dice Layout, Modeling, Sculpting...), busca la que dice Scripting (está casi al final a la derecha).

<img width="1912" height="998" alt="image" src="https://github.com/user-attachments/assets/94cc7c77-49aa-4278-9b1b-1aab1fda42da" />

Verás que la pantalla cambia: a la izquierda tienes la consola, en medio el visor 3D y a la derecha un Editor de Texto vacío.

Haz clic en el botón "+ New" que está en la parte superior central del editor de texto para crear un archivo nuevo.

<img width="1906" height="987" alt="image" src="https://github.com/user-attachments/assets/4c37efc8-7d9b-4b85-9deb-0ab3b0957a59" />

    import bpy
    import math

    def crear_poligono_2d(nombre, lados, radio):
       malla = bpy.data.meshes.new(nombre)
       objeto = bpy.data.objects.new(nombre, malla)

       bpy.context.collection.objects.link(objeto)

       vertices = []
       aristas = []

       for i in range(lados):
          angulo = 2 * math.pi * i / lados 
          x = radio * math.cos (angulo)
          y = radio * math.sin (angulo)
          vertices.append((x, y, 0))
    
       for i in range(lados):
          aristas.append((i, (i+1) % lados))
        
       malla.from_pydata(vertices, aristas, [])
       malla.update()
    
    bpy.ops.object.select_all(action = "SELECT")
    bpy.ops.object.delete()
        
    crear_poligono_2d("poligono 2d", lados = 6, radio =5) 

Ejecución y Resultados
Run Script: Una vez pegado el código, busca el botón que dice "Run Script" (o presiona Alt + P) en la parte superior del editor de texto.

<img width="1040" height="717" alt="image" src="https://github.com/user-attachments/assets/b56c1825-ce56-4020-95f3-10c7a3f82a31" />


Ver el resultado: Si todo salió bien, verás un hexágono perfecto en el visor 3D.

<img width="622" height="491" alt="image" src="https://github.com/user-attachments/assets/22caed84-c42c-4f6d-8278-9ee928c1b4ae" />

Depuración: Si no sale nada, revisa la "System Console" (en Windows: Window > Toggle System Console) para ver si Python arrojó algún error de identación o de escritura.
