### Mi solucion a la actividad 13

``` c++
#include <iostream>
#include <string>
using namespace std;

class Empleado {
public:
    string nombre; // Se almacena la cadena de caracteres
    int edad;
    static int cantidadEmpleados; // Contador estático para la cantidad de empleados

    // Constructor que inicializa los atributos
    Empleado(string _nombre, int _edad) : nombre(_nombre), edad(_edad) {
        cantidadEmpleados++;  // Aumenta el contador de empleados
        cout << "Constructor: Se ha creado el empleado " << nombre << ", Edad: " << edad << endl;
    }

    // Destructor que decrementa el contador de empleados
    ~Empleado() {
        cantidadEmpleados--;
        cout << "Destructor: Se ha destruido el empleado " << nombre << endl;
    }

    // Método para imprimir la información del empleado
    void imprimirInformacion() const {
        cout << "Empleado: " << nombre << ", Edad: " << edad << endl;
    }

    // Método estático para obtener la cantidad de empleados
    static int obtenerCantidadEmpleados() {
        return cantidadEmpleados;
    }

    // Método para modificar la edad del empleado
    void modificarEdad(int nuevaEdad) {
        edad = nuevaEdad;
    }
};

// Inicialización de la variable estática
int Empleado::cantidadEmpleados = 0;

int main() {
    // Creación de un objeto en el stack
    cout << "Creando empleado en el stack..." << endl;
    Empleado empStack("Juan", 30);
    empStack.imprimirInformacion();

    // Creación de un objeto en el heap
    cout << "Creando empleado en el heap..." << endl;
    Empleado* empHeap = new Empleado("Ana", 28);
    empHeap->imprimirInformacion();

    // Modificación de la edad del empleado en el stack
    int nuevaEdad = 35;
    empStack.modificarEdad(nuevaEdad);
    cout << "Después de modificar la edad de empStack: ";
    empStack.imprimirInformacion();

    // Mostrar la cantidad de empleados usando el método estático
    cout << "Cantidad de empleados: " << Empleado::obtenerCantidadEmpleados() << endl;

    // Eliminar el empleado en el heap
    cout << "Eliminando empleado en el heap..." << endl;
    delete empHeap;

    // Mostrar la cantidad de empleados después de eliminar empHeap
    cout << "Cantidad de empleados después de eliminar empHeap: " << Empleado::obtenerCantidadEmpleados() << endl;

    return 0;
}

```
- Explicación de los conceptos aplicados
- Clases y Objetos:

La clase Empleado representa la entidad que tiene atributos como nombre (tipo string) y edad (tipo int), además de métodos como imprimirInformacion(), que imprime los valores de estos atributos.

El objeto empStack es creado en el stack (memoria local) y el objeto empHeap es creado en el heap (memoria dinámica).

- Paso de parámetros por valor y por referencia:

El constructor de Empleado recibe los parámetros por valor: el nombre se pasa por valor como una cadena string, y la edad también se pasa por valor.

El método modificarEdad recibe un parámetro por valor y lo usa para modificar el atributo edad.

- Constructores y Destructores:

Constructor: Inicializa los objetos de la clase Empleado. El constructor se llama cuando creamos un objeto, ya sea en el stack o en el heap. Cada vez que se crea un objeto, el constructor incrementa la variable estática cantidadEmpleados.

Destructor: Decrementa la variable estática cantidadEmpleados cuando un objeto es destruido, lo cual ocurre cuando el objeto sale de su alcance en el stack o cuando se hace delete en un objeto del heap.

- Métodos y Atributos:

Métodos: El método imprimirInformacion() imprime el nombre y la edad de cada empleado. El método estático obtenerCantidadEmpleados() devuelve la cantidad actual de empleados, y el método modificarEdad() cambia la edad del empleado.

Atributos: Los atributos nombre y edad son los datos del objeto Empleado. La variable estática cantidadEmpleados mantiene el conteo total de empleados activos.

- Objetos en el stack y en el heap:

El objeto empStack se crea en el stack, lo que significa que su memoria se libera automáticamente cuando sale del alcance (al final de la función main).

El objeto empHeap se crea en el heap usando new, lo que significa que su memoria debe ser liberada explícitamente con delete al final del uso del objeto.

- Punteros y referencias:

Puntero: El objeto empHeap es creado como puntero (Empleado* empHeap = new Empleado(...)), lo que nos permite manejar la memoria dinámica.

Referencia: El objeto empStack se pasa y se manipula como referencia en las funciones que lo reciben.

- Variables estáticas:

cantidadEmpleados es una variable estática, lo que significa que es compartida por todos los objetos de la clase Empleado y mantiene el conteo total de los empleados. Se inicializa fuera de la clase.

- Depuración:

A través de la impresión de mensajes en la consola (cout), es posible depurar el programa y verificar en qué momento se crean y destruyen los objetos, así como cuántos empleados están activos en cualquier momento.

También se puede utilizar un depurador de código para hacer una depuración paso a paso y observar cómo cambian los valores en memoria.

- Análisis detallado de la memoria
Memoria del Stack:

empStack es un objeto creado en el stack. Cuando se crea este objeto, su memoria se asigna en la pila de la función main y se libera automáticamente cuando el objeto sale del alcance de la función main. El constructor de Empleado se llama al momento de la creación del objeto, y el destructor se invoca automáticamente cuando el objeto se destruye.

Memoria del Heap:

empHeap es un puntero que apunta a un objeto creado dinámicamente en el heap con new. Esta memoria no se libera automáticamente cuando el objeto sale del alcance, por lo que se debe llamar explícitamente a delete empHeap para liberar la memoria. El puntero en sí está en el stack, pero el objeto al que apunta está en el heap.

Segmentos de memoria:

Stack: El puntero empHeap (que almacena la dirección del objeto en el heap), el objeto empStack, y las variables locales como nuevaEdad están almacenados en el stack.

Heap: El objeto real al que empHeap apunta está en el heap, y la memoria es gestionada dinámicamente por el sistema.
