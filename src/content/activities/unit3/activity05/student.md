### Mi solución a la actividad 5

- Experimento 3:

``` c++
#include <iostream>
#include <cstdlib>

using namespace std;

// Variables globales
int global_inicializada = 42;
int global_no_inicializada;


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 3
    ***********************************************************/

    cout << "global_inicializada: " << global_inicializada << endl;
    cout << "global_no_inicializada: " << global_no_inicializada << endl;


    global_inicializada = 69;
    global_no_inicializada = 666;

    cout << "global_inicializada: " << global_inicializada << endl;
    cout << "global_no_inicializada: " << global_no_inicializada << endl;

    /********************************************************/

    return 0;
}
```
![Consola de depuración de Microsoft Visual Studio 18_03_2025 9_08_47 a  m](https://github.com/user-attachments/assets/feae566d-90e5-406b-9840-e4adada87db3)

- Variables globales: Las variables globales se almacenan en una sección de memoria llamada "datos" (o segmento de datos), que se encuentra en una región de memoria que no es de solo lectura. Esto permite que las variables globales sean modificadas durante la ejecución del programa.
- global_inicializada tiene un valor inicial explícito (42), por lo que ese valor es asignado en el momento de la declaración.
- global_no_inicializada, al no ser inicializada explícitamente, puede contener cualquier valor aleatorio (basado en la memoria residual), pero luego se le asigna el valor 666

- Experimento 4:

``` c++
#include <iostream>
#include <cstdlib>

using namespace std;

// Función de ejemplo que muestra la dirección de su variable local estática
void funcionConStatic() {
    static int var_estatica = 100;
    cout << "Dirección de var_estatica (static): " << &var_estatica << endl;
}


int main() {
    // Variable local (stack)
    int a = 10;
    int b = 20;

    /**********************************************************
        EXPERIMENTO 4
    ***********************************************************/

    var_estatica = 42;

    cout << "var_estatica: " << var_estatica << endl;

    /********************************************************/
    return 0;
}

```
![ConsoleApplication6 - Microsoft Visual Studio 18_03_2025 9_13_16 a  m](https://github.com/user-attachments/assets/f58d93f3-9387-46b4-a930-a1c9eb7f8aaf)

- Error de compilación, ¿por qué?  El compilador generará un error porque var_estatica no es accesible fuera de la función funcionConStatic(). Las variables locales estáticas solo son visibles dentro de la función en la que se definen, aunque persisten durante toda la ejecución del programa.

##### ¿Qué pasa con las variables cada que entras y sales de la función?

- Variables locales no estáticas:
Las variables locales no estáticas se crean y destruyen cada vez que entras y sales de la función.
Esto significa que al entrar a la función se asigna espacio en el stack para ellas, y cuando sales de la función, esas variables dejan de existir.
- Variables locales estáticas:
Las variables estáticas no se destruyen ni se recrean con cada entrada o salida de la función.
Su valor persiste durante toda la ejecución del programa, lo que permite que conserven su valor entre invocaciones sucesivas de la misma función. Aunque están localizadas dentro de la función, su vida útil es igual a la del programa.

###### En relación a la pregunta anterior ¿Qué pasa con las variables locales estáticas?
- Las variables locales estáticas se inicializan solo una vez, la primera vez que se llama a la función.
Posteriormente, su valor se mantiene entre las llamadas a la función, pero sigue siendo local a esa función en términos de acceso.
- Si accedes a la función varias veces, la variable estática conservará su valor entre las llamadas.
Esto es útil cuando necesitas que la variable conserve su valor entre ejecuciones, pero no necesitas que sea accesible fuera de la función.
