<!--Manejo básico de la memoria
Enunciado: la memoria en el computador Hack se organiza como una secuencia de direcciones, donde cada dirección almacena un valor de 16 bits. 
El documento "Machine Language" menciona diferentes modos de direccionamiento (página 60).

¿Qué es el direccionamiento directo? ¿Cómo se usa en el lenguaje ensamblador Hack?
¿Qué significa M=D en lenguaje ensamblador Hack? ¿Y D=M?
Explica con tus palabras el concepto de "puntero" en el contexto de la memoria y proporciona un ejemplo sencillo en lenguaje ensamblador Hack. (Puedes usar el ejemplo de
la página 61 del documento como inspiración, pero adáptalo a un caso más simple).
Entrega: respuestas a las preguntas y un ejemplo de código en ensamblador que ilustre el concepto de puntero y su uso para acceder a la memoria. -->

### Mi solución a la actividad 6

##### ¿Qué es el direccionamiento directo? ¿Cómo se usa en el lenguaje ensamblador Hack?

- El direccionamiento directo es la forma más habitual de direccionar la memoria es expresar una dirección concreta o utilizar un símbolo que haga referencia a una dirección concreta.
En el lenguaje ensamblador Hack,
esto significa que el programa hace referencia directa a una dirección de memoria específica en lugar de usar un cálculo o registro intermedio.

###### Ejemplo de uso en el lenguaje emsamblador hack:

``` asm
@67
D=M
```
Carga en D el valor almacenado en la dirección 67

##### ¿Qué significa M=D en lenguaje ensamblador Hack? ¿Y D=M?

- M=D: Guarda el valor del registro D en la dirección de memoria apuntada actualmente.

- D=M: Carga el valor almacenado en la dirección de memoria apuntada actualmente en el registro D.

##### Explica con tus palabras el concepto de "puntero" en el contexto de la memoria y proporciona un ejemplo sencillo en lenguaje ensamblador Hack. (Puedes usar el ejemplo de la página 61 del documento como inspiración, pero adáptalo a un caso más simple).

- Un puntero es una variable que almacena una dirección de memoria en lugar de un valor directamente.
 En ensamblador Hack, los punteros permiten acceder y modificar valores en diferentes partes de la memoria sin necesidad de conocer sus direcciones exactas en el código.

###### Ejemplo:

``` asm
@100
D=A    
@5
M=D    
@5
A=M    
M=42  
```
En D=A se carga la dirección @100 en D y en M=D se guarda 100 en la dirección 5 (Aquí 5 sería el puntero), se cambia a la dirección 100 y en M=42 se guarda el valor de 42 en la dirección 100.
