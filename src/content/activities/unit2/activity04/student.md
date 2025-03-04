<!-- Escritura usando punteros
Enunciado: un puntero es una variable que almacena la dirección de memoria de otra variable. Observa el siguiente programa escrito en C++:

int a = 10;
int* p;
p = &a;
*p = 20;
El programa anterior modifica el contenido de la variable a por medio de la variable p. p es un puntero porque almacena la dirección de memoria de la variable a. En este caso el valor de la variable a será 20 luego de ejecutar *p = 20;.

Ahora analiza con detenimiento:

¿Cómo se declara un puntero en C++?
int* p;
p es una variable que almacenará la dirección de otra variable. Dicha variable almacenará número enteros.

¿Cómo se define (nota que antes preguntamos cómo se declara) un puntero en C++?
p = &a;. 
Definir el puntero es inicializar el valor del puntero, es decir, guardar la dirección de una variable. En este caso p contendrá la dirección de a o podemos decir que p apunta a a

¿Cómo se almacena en C++ la dirección de memoria de una variable? Con el operador &.
p = &a;
¿Cómo se escribe el contenido de la variable a la que apunta un puntero? Con el operador *.
*p = 20;
En este caso como p contiene la dirección de a. Por tanto, se está modificando el valor de la variable a por medio de p.

Ahora tu misión será convertir este programa a ensamblador:

int a = 10;
int* p;
p = &a;
*p = 20;
Por favor, te ruego que verifiques con el simulador. No olvides que p debe guardar la dirección de a
Entrega: la solución al problema anterior. -->

### Mi solución a la actividad 4

 ``` js
@10  
D=A 
@16 
M=D  
@16  
D=A  
@17  
M=D 
@20 
D=A 
@17 
A=M  
M=D
```
