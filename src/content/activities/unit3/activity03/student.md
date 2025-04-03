### Mi solución a la actividad 3

- Imagen de la ejecucion del programa:

![Consola de depuración de Microsoft Visual Studio 11_03_2025 9_19_02 a  m](https://github.com/user-attachments/assets/c78c0bee-e8fa-4851-ada2-01861b3b85ec)

- Mapa de memoria usando el que nos dio el profe:

``` bash
+-------------------------------+
|       Segmento de código      |
|   (instrucciones, funciones)  |  <--- Código ejecutable de las funciones.
| Dirección de la función suma()|
| Dirección de main()            |
| Dirección de funcionConStatic()|
+-------------------------------+
| Variables globales y estáticas |
| Dirección de global_inicializada|
| Dirección de global_no_inicializada|
| Dirección de mensaje_ro (constante global de solo lectura)|
| Dirección de var_estatica (static)|
+-------------------------------+
|           Heap                |  <--- Asignación dinámica (new)
| Dirección de arrayHeap        |  <--- Dirección donde se almacena el array dinámico.
+-------------------------------+
|           Stack               |  <--- Variables locales
| Dirección de variable 'a'     |  <--- Dirección de la variable local 'a'
| Dirección de variable 'b'     |  <--- Dirección de la variable local 'b'
| Dirección de variable 'c'     |  <--- Dirección de la variable local 'c'
+-------------------------------+
```
