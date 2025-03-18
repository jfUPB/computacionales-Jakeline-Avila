### Mi solución a la actividad 6

- Experimento 5

``` c++
#include <iostream>
#include <cstdlib>

using namespace std;

// Función de ejemplo que muestra la dirección de su variable local estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "var_estatica: " << var_estatica << endl;
    var_estatica++;
}

void funcionSinStatic() {
    int var_no_estatica = 100;
    cout << "var_no_estatica: " << var_no_estatica << endl;
    var_no_estatica++;
}


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 5
    ***********************************************************/

    for (int i = 0; i < 5; i++) {
        cout << "Iteración " << i << endl;
        funcionSinStatic();
        funcionConStatic();
    }

    /********************************************************/

    return 0;
}

```
![Consola de depuración de Microsoft Visual Studio 18_03_2025 9_34_49 a  m](https://github.com/user-attachments/assets/96973b32-6092-48a6-8280-a6cb5ef7542e)

- ¿Por qué ocurre esto?

Variables locales estáticas: Una variable estática mantiene su valor durante toda la ejecución del programa, incluso cuando la función en la que está definida ha terminado de ejecutarse. 
Esto permite que se conserve el valor entre las llamadas a la misma función.

Variables locales no estáticas: Las variables locales no estáticas son reinicializadas cada vez que se invoca la función. Cada vez que se entra en la función, la variable se crea y se inicializa, y 
al salir de la función, se destruye.

- Diferencias entre las variables estáticas y no estáticas:

Persistencia: Las variables estáticas permanecen entre llamadas a la función, mientras que las no estáticas se reinicializan con cada llamada.
Alcance: Ambas son locales a la función, pero las variables estáticas no se destruyen al salir de la función.
Propósito: Las variables estáticas son útiles para almacenar valores que deben persistir entre las ejecuciones de la función, 
mientras que las no estáticas se utilizan para valores que no necesitan ser recordados entre llamadas.

- Experimento 6

``` c++
#include <iostream>
using namespace std;

int main() {
    // Tamaño del arreglo dinámico
    int tam = 5;

    // Asignar memoria en el Heap para un arreglo de enteros
    int* arrayHeap = new int[tam];

    // Inicializar y mostrar los valores y direcciones de memoria
    for (int i = 0; i < tam; i++) {
        arrayHeap[i] = (i + 1) * 10;
        cout << "arrayHeap[" << i << "] = " << arrayHeap[i]
            << " en dirección " << (arrayHeap + i) << endl;
    }

    // Liberar la memoria asignada en el Heap
    delete[] arrayHeap;

    /**********************************************************
        EXPERIMENTO 6
    ***********************************************************/

    cout << arrayHeap[0] << endl;


    /********************************************************/


    return 0;
}

```
- ¿Qué ocurre?
Descripción del comportamiento: El código realiza las siguientes acciones:

Se asigna memoria dinámica en el Heap para un arreglo de enteros.
Se inicializan y muestran los valores del arreglo.
Se libera la memoria usando delete[] para el arreglo dinámico.
Después de liberar la memoria, el programa intenta acceder a arrayHeap[0].
El error ocurre al intentar acceder a la memoria liberada, lo que provoca comportamiento indefinido.

- ¿Por qué ocurre este error?
Acceso a memoria después de liberarla: Después de usar delete[], la memoria que ocupaba arrayHeap ya no es válida. El puntero apunta a una región de memoria que ha sido liberada, por lo que intentar acceder a ella puede dar lugar a errores, como un comportamiento indefinido o segmentation fault.

Comportamiento indefinido: Aunque en algunos casos el acceso a la memoria después de liberar puede no causar un fallo inmediato, es peligroso y puede producir resultados inesperados o incluso corromper la memoria.

Diferencias entre el comportamiento y la gestión del Heap vs Stack:
Stack:
La memoria del stack se gestiona automáticamente. Cuando una función termina, las variables locales se destruyen automáticamente.
Es más rápida, pero su tamaño está limitado.
Si no se gestiona correctamente, puede producir un stack overflow (por ejemplo, si se usa demasiada memoria local en recursión).
Heap:
La memoria del heap se gestiona manualmente. Si asignas memoria con new, debes liberarla con delete.
Es más flexible porque puedes asignar grandes bloques de memoria durante la ejecución, pero es más lenta de gestionar.
Si no se libera la memoria, puede causar fugas de memoria (memory leaks), lo que puede llevar a que el sistema se quede sin memoria.
Consecuencias de no liberar la memoria reservada con new:
Si no liberas la memoria con delete[], el programa tendrá fugas de memoria. Esto significa que la memoria asignada nunca será recuperada, lo que puede llevar a que el sistema se quede sin memoria si el programa se ejecuta durante mucho tiempo o maneja grandes cantidades de memoria dinámica.
¿Por qué es importante usar delete[] para liberar memoria de un arreglo?
Cuando se asigna un arreglo dinámico con new[], se debe usar delete[] para liberar correctamente esa memoria. Si usas solo delete en lugar de delete[], podrías liberar incorrectamente la memoria, lo que puede causar fallos o corrupción de memoria.

