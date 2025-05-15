<!-- Lectura usando punteros
Enunciado: ahora vas a usar un puntero para leer la posición de memoria a la que este apunta, es decir, vas a leer por medio del puntero la variable cuya dirección está almacenada en él.

int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
En este caso:

b = *p;
el código anterior hace que el valor de b cambie de 5 a 10 porque p apunta a a y con *p a la derecha del igual estás leyendo el contenido de la variable apuntada.

Traduce el programa el siguiente programa a ensamblador y no olvides simular
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
Entrega: la traducción a ensamblador.-->

### Mi solución a la actividad 5

``` js
@10
D=A
@16
M=D
@5
D=A
@17
M=D
@16
D=A
@18
M=D
@18
D=M
A=D
D=M
@17
M=D
```
