### Mi solución a la actividad 4

<!-- Experimento 1: modificar el segmento de texto:

#include <iostream>
#include <cstdlib>

using namespace std;


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 1
    ***********************************************************/

    void* ptr = reinterpret_cast<void*>(&main);
    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
    *reinterpret_cast<int*>(ptr) = 0;

    /********************************************************/

    return 0;
}
¿Qué ocurre? ¿Por qué? -->

- Experimento 1:

``` c++
#include <iostream>
#include <cstdlib>

using namespace std;


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 1
    ***********************************************************/

    void* ptr = reinterpret_cast<void*>(&main);
    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
    *reinterpret_cast<int*>(ptr) = 0;

    /********************************************************/

    return 0;
}
```
- Ocurre una excepción.

![ConsoleApplication6 (Depuración) - Microsoft Visual Studio 18_03_2025 8_56_50 a  m](https://github.com/user-attachments/assets/3ca2de23-5160-4d31-9e77-2f47bf7b11ba)

- ¿Por qué? El segmento de texto (o código) está diseñado para ser de solo lectura en la mayoría de las implementaciones modernas.
Esto es para prevenir que las instrucciones del programa sean alteradas accidentalmente o maliciosamente, lo que podría llevar a un fallo en el sistema o a un ataque de ejecución de código malicioso.

- Experimento 2:

``` c++
#include <iostream>
#include <cstdlib>

using namespace std;

// Constante global
const char* const mensaje_ro = "Hola, memoria de solo lectura";


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;


    /**********************************************************
        EXPERIMENTO 2
    ***********************************************************/

    char* ptr = (char*)&mensaje_ro;
    cout << "Voy a modificar la memoria en la dirección: " << ptr << endl;
    *ptr = 0;

    /********************************************************/

    return 0;
}
```
- Se produce otra excepción:

![ConsoleApplication6 (Depuración) - Microsoft Visual Studio 18_03_2025 8_56_50 a  m](https://github.com/user-attachments/assets/aca7beff-8c02-426f-89c3-2bc0e4577c78)

- ¿Por qué? La variable mensaje_ro es constante y está almacenada en una región de memoria que es de solo lectura,
lo cual está protegido por el sistema operativo y el compilador. Esta región está destinada a almacenar datos que no deben ser modificados durante la ejecución del programa.   
El uso de const en C++ indica que el valor de mensaje_ro no puede ser alterado, pero aún más importante es que la cadena literal que apunta la constante también se encuentra en una
región de solo lectura, y cualquier intento de modificación de esa memoria generará una violación de acceso.


