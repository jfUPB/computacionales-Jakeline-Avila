<!-- Enunciado: considera el siguiente programa en lenguaje de máquina. Salva el programa en un archivo "test.hack" y cárgalo en el simulador. Una vez cargado lo puedes visualizar en formato asm.

0100000000000000
1110110000010000
0000000000010000
1110001100001000
0110000000000000
1111110000010000
0000000000010011
1110001100000101
0000000000010000
1111110000010000
0100000000000000
1110010011010000
0000000000000100
1110001100000110
0000000000010000
1111110010101000
1110101010001000
0000000000000100
1110101010000111
0000000000010000
1111110000010000
0110000000000000
1110010011010000
0000000000000100
1110001100000011
0000000000010000
1111110000100000
1110111010001000
0000000000010000
1111110111001000
0000000000000100
1110101010000111

Traduce este programa a un lenguaje de alto con el que estés familiarizado, puede ser C#, java o C++. Trata el teclado como la variable KBD y la pantalla como el arreglo SCREEN. Recuerda que cada posición del arreglo SCREEN representa 16 pixeles de la pantalla. En total la pantalla tienen 512*256 pixeles (Entonces ¿Cuále es el tamaño del arreglo SCREEN?)
Entrega: en tu bitácora la traducción del programa a alto nivel.-->

### Mi solución a la actividad 9

- Como se ve el código en asm:

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
- Traduciendolo a C#

``` C#
namespace computacionales
{

    using System;
    using System.Reflection;

    internal class Program
    {
      
           // constantes definidas
            const int SCREEN_WIDTH = 512;
            const int SCREEN_HEIGHT = 256;
            const int PIXELS_FOR_PALABRA = 16;
        //Tamaño que va a tomar el array Screen (512*256)/16 = 8192

            const int SCREEN_SIZE = (SCREEN_HEIGHT * SCREEN_WIDTH) / PIXELS_FOR_PALABRA;
        // Dirección base de la pantalla (screen) y del teclado (KBD)

        const int SCREEN_BASE = 16384;
        const int KBD_ADRESS = 24576;

        //Aquí se simula la memoria de la palabra
        static int[] SCREEN = new int[SCREEN_SIZE];
           
        //Un puntero equivalente a RAM[16] 
        static int pointer = SCREEN_BASE;

        // Variable que representa el estado del teclado KBD
        static int KBD = 0;

        static void Main()
        {
            // Inicialmente, el puntero se establece en la base de la pantalla

            pointer = SCREEN_BASE;

            // Ahora viene la parte del bucle infinito

            while (true)
            {
                //Segun mi logica aqui debo actualizar la variable KBD según la entrada del usuario

                //Por ejemplo KBD = ObtenerEntradaTeclado();

                //Si no se ha presionado ninguna tecla (KBD ==0)

                if (KBD == 0)
                {
                    //Se calcula pointer - screen_base. Si es <= 0 no podemos borrar más.

                    if (pointer - SCREEN_BASE > 0)
                    {

                        // Se decrementa el puntero (Equivalente a "AM=M-1"
                        pointer--;

                        //Se borra el contenido de la celda screen correspondiente osea colocamos el 0
                        // El indice con SCREEN es pointer - SCREEN_BASE, ya que SCREEN[0] corresponde a la dirección 16384.
                        SCREEN[pointer - SCREEN_BASE] = 0;
                        //
                    }
                }
                else
                {

                    // Si se ha presionado una tecla (KBD diferente de 0)

                    if (pointer < KBD)
                    {

                        //escribimos -1 en la celda de SCREEN apuntada osea encender los pixeles

                        SCREEN[pointer - SCREEN_BASE] = -1;

                        pointer++;

                    }
                }
            }
        }
        
    }
}

```
