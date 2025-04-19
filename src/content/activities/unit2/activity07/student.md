<!-- Experimenta con arreglos
Enunciado: los arreglos son colecciones de datos en la memoria.

Considera el siguiente programa

int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}
Implementa el programa anterior en lenguaje ensamblador.
Considera que los datos del arreglo están almacenados desde la dirección 16. Puedes inicializar manualmente el arreglo.
Es fundamental que hagas la simulación paso a paso y analices con detenimiento el funcionamiento del programa.
Entrega: la solución al problema anterior. -->

### Mi solución a la actividad 7

``` js

// se inicializa el arreglo(array)
@1  // array[0] = 1 en RAM [16]
D=A 
@16 
M=D 
@2 // array[1] = 2 en RAM [17]
D=A 
@17 
M=D 
@3 // array[2] = 3 en RAM [18]
D=A 
@18 
M=D 
@4 // array[3] = 4 en RAM [19]
D=A 
@19 
M=D
@5 // array[4] = 5 en RAM [20]
D=A 
@20 
M=D 
@6 // array[5] = 6 en RAM [21]
D=A 
@21 
M=D 
@7 // array[6] = 7 en RAM [22]
D=A 
@22 
M=D 
@8 // array[7] = 8 en RAM [23]
D=A 
@23 
M=D
@9 // array[8] = 9 en RAM [24]
D=A 
@24 
M=D 
@10 // array[9] = 10 en RAM [25]
D=A 
@25 
M=D 
@0 // sum = 0 en RAM[26]
D=A 
@26 
M=D
@16 // Puntero
D=A 
@27
M=D 
@27 // Verificar que el puntero ha llegado a 26
D=M // D= valor de p que es la direccion actual del puntero
@26 
D=D-A // D = P - 26; si p == 26, D=0
D=0 
@56 
D;JEQ // Si D == 0, se han recorrido 10 elementos; salta a la linea 56
@0 
@0 
@0 
@27 // cargar el elemento del arreglo apuntado por P
A=M // A= contenido de p
D=M // D = M[A] = arr[j]
@26 
D=D+M // D = arr[j] + sum
@26 
M=D // sum = nuevo valor
@27 // incrementar el puntero p= p + 1
M=M+1 
0;JMP // ciclo
```
