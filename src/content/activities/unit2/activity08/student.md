### Mi solución a la actividad 8

- Este es el código cuando es pasado a asm.

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
- Explicación:

 ``` js
@16384 
D=A 
@16 
M=D
```
- Se carga el número 16384 (La dirección base de la memoria de la pantalla) en el registro D y se guarda en la dirección RAM[16]. La dirección 16 se usa como únterp que
indica la posición actual en la pantalla en la que se va a escribir.

``` js
@24576 
D=M 
@19 
D;JNE
```
- Se accede a la dirección 24576, que es donde está mapeado el teclado. Se copia el contenido (El valor leído del teclado) en D. Luego la instrucción D;JNE salta a la instrucción 19
si el valor leído es distinto de 0 (Es decir, se ha presionado alguna tecla).

``` js
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
```
- Se carga el valor del puntero (almacenado en RAM[16]) en D
- Se resta 16384 (La dirección base de la pantalla) de ese valor.
- Con D;JLE se salta a la dirección 4 (que corresponde a volver a leer el teclado) si el resultado es menor o igual que 0, lo cual significa que si el puntero esta en 16384
(o por debajo, aunque este programa no ocurrirá que sea menor), no se borra nada y se vuelve el bucle.
Si el resultado es mayor que 0 (Es decir, hay almenos un pixel dibujado) se procede a decrementar el puntero (AM=M-1) se resta 1 a RAM[16] y se pone el valor en A, escribir 0 en la posicion de la pantalla
apuntada (borrando el último pixel dibujado).
- Finalmente se salta incondicionalmente a la dirección 4 (Donde se vuelve a leer el teclado).

``` js
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

