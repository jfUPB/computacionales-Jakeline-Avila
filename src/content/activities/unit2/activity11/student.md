<!-- Resumen
Enunciado:

Vas a listar los principales conceptos que aprendiste en esta unidad.
Explica dichos conceptos y muestra un ejemplo usado en la unidad.
Entrega: en tu bitácora la respuesta a las cuestiones anteriores.-->

### Mi solución a la actividad 11

- Aprendí a usar punteros, funciones, un poco más de saltos.

- Un puntero es una variable que almacena la dirección de memoria de otra variable, permitiendo acceder y modificar ese contenido indirectamente.

- Una función es un bloque de código diseñado para realizar una tarea específica; puede recibir parámetros y, en algunos casos, devolver un resultado, facilitando la reutilización y organización del código.

- Un salto es una instrucción que altera el flujo secuencial de ejecución del programa, permitiendo que éste continúe en otra parte del código, ya sea de forma condicional o incondicional.

``` js

@16384 
D=A 
@16 
M=D 
@24576 
D=M 
@19 
D;JNE 
@16 
D=M 
@16384 
D=D-A 
@4 
D;JLE 
@16 
AM=M-1 
M=0 
@4 
0;JMP 
@16 
D=M 
@24576 
D=D-A 
@4 
D;JGE 
@16 
A=M 
M=-1 
@16 
M=M+1 
@4 
0;JMP 
```
