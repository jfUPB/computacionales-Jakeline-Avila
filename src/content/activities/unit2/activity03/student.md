<!-- Convierte un ciclo while en un ciclo for
Enunciado: considera el siguiente programa:

//Adds 1+...+100.
 int i=1;
 int sum=0;
 
 while(i <=100){
    sum+= i;
    i++;
 }
Vamos a transformar este programa a su equivalente usando un ciclo for:

//Adds 1+...+100.
int sum=0;
for(int 1 = 1; i <=100; i++){
   sum+= i;
}
Analiza los programas anteriores y asegúrate de entender por qué son equivalentes.
Convierte la versión del for a ensamblador.
No olvides comprobar el funcionamiento de los programas en ensamblador en el simulador.
Compara las versiones en ensamblador del while y del for. ¿Qué puedes concluir?
Entrega: la solución a las cuestiones planteadas en el enunciado. -->

### Mi solución a la actividad 3

Traducción del ciclo for a ensamblador

- El equivalente en ensamblador del código con for es:

``` js
// Adds 1+...+100.
@sum
M=0 // sum = 0
@i
M=1 // i = 1

(LOOP)
@i
D=M // D = i
@100
D=D-A // D = i - 100
@END
D;JGT // If(i - 100) > 0 goto END

@i
D=M // D = i
@sum
M=D+M // sum = sum + i

@i
M=M+1 // i = i + 1
@LOOP
0;JMP // Goto LOOP

(END)
@END
0;JMP // Infinite loop

```

#### Comparación entre el while y el for en ensamblador

Después de analizar ambas versiones en ensamblador, se puede concluir que la estructura generada es prácticamente la misma. Ambos programas tienen:

1. Inicialización: La variable i y sum se inicializan antes de entrar al bucle.


2. Condición de terminación: Se compara i con 100 y, si i > 100, el programa salta a END.


3. Cuerpo del bucle: Se suma i a sum, y luego se incrementa i.


4. Salto al inicio: Una vez ejecutadas las instrucciones dentro del bucle, el programa salta de nuevo a la verificación de la condición.



Esto confirma que, a nivel de ensamblador, tanto el while como el for generan un código casi idéntico. La diferencia principal está en el código fuente de alto nivel, donde for es más compacto y legible, pero en ensamblador, la ejecución se mantiene igual.
