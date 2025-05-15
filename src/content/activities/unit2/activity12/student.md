<!-- Consolidación
Enunciado: vas a inventar un ejemplo, diferente a los de la unidad, en lenguaje de alto nivel con su equivalente en lenguaje ensamblador para cada uno de los siguientes conceptos:

Condicionales
Ciclos while
Ciclos for
Escritura de variables por medio de punteros
Lectura de variables por medio de punteros
Manipulación de un arreglo por medio de punteros.
Llamado a funciones con parámetros.
Llamado a funciones con retorno de parámetros (no lo trabajamos en la unidad pero tienes las herramientas para proponer un ejemplo)
NO OLVIDES SIMULAR CADA EJEMPLO en lenguaje ensamblador para asegurar que está correcto

Entrega: el programa en alto nivel y su equivalente en ensamblador. -->

### Mi solución a la actividad 12

- Condicionales

``` C#
    static void Main(string[] args)
    {
        //condicionales

        int x = 5;
        int y = 10;
        if (x < y)
        {

            x = x + 1;
        }
        else
        {

            x = x - 1;
        }
    }
}
```
- Equivalente en lenguaje ensamblador:

``` js
@5
D=A
@0
M=D
@10
D=A
@1
M=D
@0
D=M
@1
D=D-M
@29
D;JGE

@0
M=M+1
@5
0;JMP

@0
M=M-1
0;JMP
```
- Ciclos while

``` C#
int count = 0;
while (count < 3)
{

count++;

}
```

- equivalente a lenguaje ensamblador

``` Js
@0
M=0

@0
D=M
@3
D=D-A
@23
D;JGE
@0
M=M+1
0;JMP
```
- Ciclos for

``` C#
for (int i = 0; i < 3; i++)
{}
```
- Equivalente a lenguaje ensamblador

``` js
@0
M=0

@0
D=M
@3
D=D-A
@23
D;JGE

@0
M=M+1
@05
0;JMP
```
- Escritura de variable por medio de punteros

``` C#
int a = 5;
int* ptr = &a;
*ptr = 10;
```

- Equivalente a lenguaje ensamblador

``` js
@5
D=A
@0
M=D

@0
D=A
@1
M=D

@10
D=A
@1
A=M
M=D
```
- Lectura de variables con punteros

``` C#
int a = 5;
int* ptr = &a;
int b = *ptr;
```

- Equivalente a lenguaje ensamblador

``` js
@5
D=A
@0
M=D

@0
D=A
@1
M=D

@1
A=M
D=M
@2
M=D
```
- Manipulación de un arreglo con punteros

``` C#
int arr[] = {1, 2, 3}
int* ptr = arr;
*(ptr + 1) = 10;
```
- Equivalentes a lenguaje ensamblador

``` js
@1
D=A
@100
M=D
@2
D=A
@101
M=D
@3
D=A
@102
M=D
@100
D=A
@1
M=D

@1
D=A
@1
A=M+D
M=10
```
- Llamado a función con parámetros

``` c#
int Sum(int a, int b) {
return a + b;
}
int result = Sum (3, 4);
```

- Equivalente a lenguaje ensamblador

``` js
@3
D=A
@0
M=D
@4
D=A
@1
M=D
@23
0;JMP

@2
M=D
@0
D=M
@1
D=D+M
@0
0;JMP
```
- Llamado a función con retorno de parámetro

``` c#
int multiply(int a, int b)
{
return a * b;
}
int result = Multiply (3, 4);
```

- Equivalente a lenguaje ensamblador

``` js
@3
D=A
@0
M=D
@4
D=A
@1
M=D

@23
0;JMP

@2
M=D

@0
D=M
@1
D=D*M

@0
0;JMP
```



