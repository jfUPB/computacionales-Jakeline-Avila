### Mi solución a la actividad 14

1. Explicación de lo aprendido en la unidad:

Durante esta unidad, aprendí diversos conceptos fundamentales de programación orientada a objetos (POO) en C++. A continuación, explicaré algunos de estos conceptos utilizando ejemplos concretos de los códigos que trabajé.

Clases y Objetos:

Uno de los conceptos principales fue aprender cómo crear clases y trabajar con objetos. Las clases definen la estructura de los objetos, mientras que los objetos son instancias de esas clases. Por ejemplo, en el siguiente código creamos una clase llamada Punto que tiene dos atributos (x e y) y métodos para inicializar, imprimir y destruir un objeto de esa clase:

``` c++
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    // Constructor
    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    // Destructor
    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    // Método para imprimir valores
    void imprimir() {
        cout << "Punto(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    // Coloca un breakpoint en la siguiente línea
    Punto p(10, 20);

    // Muestra el contenido del objeto
    p.imprimir();

    return 0;
}
```
En este código, al crear el objeto p, se invoca el constructor, y al salir del bloque, se invoca el destructor automáticamente. Esto muestra cómo los objetos gestionan su ciclo de vida a través de estos métodos especiales.

Paso de Parámetros por Valor y por Referencia:

También comprendí la diferencia entre el paso de parámetros por valor y por referencia. El paso por valor crea una copia del objeto, mientras que el paso por referencia trabaja directamente con la misma instancia. En el siguiente código, el cambio de nombre de un objeto no afecta al original debido al paso por valor:

``` c++
#include <iostream>
#include <string>
using namespace std;

class Punto {
public:
    string name;
    int x;
    int y;

    // Constructor
    Punto(string _name, int _x, int _y) : name(_name),x(_x), y(_y) {
        cout << "Constructor: Punto "<< name <<" (" << x << ", " << y << ") creado." << endl;
    }

    // Destructor
    ~Punto() {
        cout << "Destructor: Punto " << name << "(" << x << ", " << y << ") destruido." << endl;
    }

    // Método para imprimir valores
    void imprimir() {
        cout << "Punto "<< name << "(" << x << ", " << y << ")" << endl;
    }
};

void cambiarNombre(Punto p, string nuevoNombre) {
    p.name = nuevoNombre;
}

int main() {
    // Objeto original
    Punto original("original",70, 80);
    original.imprimir();

    cambiarNombre(original, "cambiado");
    original.imprimir();  // El nombre no cambia en este caso

    return 0;
}
```
En el ejemplo anterior, la función cambiarNombre pasa el objeto por valor, lo que significa que el objeto original no se ve afectado por el cambio de nombre dentro de la función.

Objetos en el Stack y en el Heap:

Un concepto fundamental fue entender la diferencia entre los objetos en el stack y en el heap. Los objetos en el stack se destruyen automáticamente cuando salen de su alcance, mientras que los objetos en el heap deben ser liberados manualmente usando delete. El siguiente código muestra cómo se crean objetos en el stack y en el heap:

``` c++
#include <iostream>
using namespace std;

class Punto {
public:
    int x;
    int y;

    // Constructor
    Punto(int _x, int _y) : x(_x), y(_y) {
        cout << "Constructor: Punto(" << x << ", " << y << ") creado." << endl;
    }

    // Destructor
    ~Punto() {
        cout << "Destructor: Punto(" << x << ", " << y << ") destruido." << endl;
    }

    // Método para imprimir valores
    void imprimir() {
        cout << "Punto(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    // Objeto en el stack
    Punto pStack(30, 40);
    pStack.imprimir();

    // Objeto en el heap
    Punto* pHeap = new Punto(50, 60);
    pHeap->imprimir();

    // Coloca breakpoints en la creación de pStack y pHeap
    // Inspecciona las direcciones de memoria de ambos objetos:
    // - pStack: dirección obtenida directamente.
    // - pHeap: la variable pHeap es un puntero que contiene la dirección del objeto en el heap.

    // Recuerda liberar la memoria del heap
    delete pHeap;

    return 0;
}
```
En este código, pStack se crea en el stack y se destruye automáticamente al salir del bloque. En cambio, pHeap se crea dinámicamente en el heap y debe ser liberado manualmente con delete.

Punteros y Referencias:

Entendí cómo trabajar con punteros para manipular objetos en el heap. El puntero pHeap apunta a un objeto de tipo Punto en la memoria dinámica, lo que me permitió acceder al objeto y modificarlo. En este caso, la memoria se libera con delete para evitar fugas de memoria.

2. Conceptos más desafiantes de la unidad:

El concepto más desafiante para mí fue la gestión de la memoria dinámica, especialmente cuando se trabaja con punteros y objetos en el heap. Asegurarse de liberar correctamente la memoria usando delete es crucial para evitar fugas de memoria. Además, el paso de parámetros por valor y por referencia fue un poco confuso, ya que los objetos se copian cuando se pasan por valor y se manipulan directamente cuando se pasan por referencia.

3. Estrategias utilizadas para comprender los conceptos desafiantes:

Estudiar ejemplos prácticos: Trabajé en varios ejemplos como los que se muestran arriba para entender cómo los objetos se crean, manipulan y destruyen en el stack y el heap.

Depuración paso a paso: Usé el depurador para inspeccionar el comportamiento de los objetos en tiempo de ejecución. Esto fue útil para ver cómo la memoria se asigna y libera, y cómo los punteros apuntan a la memoria dinámica.

4. Estrategias más efectivas:

La estrategia más efectiva fue el uso del depurador paso a paso. Esto me permitió observar cómo la memoria se asigna y libera y cómo los objetos se comportan en tiempo de ejecución. La visualización en vivo de los valores de las variables y las direcciones de memoria me ayudó a entender cómo funcionan los punteros y las referencias.

5. Plan de acción para mejorar la comprensión de los conceptos más desafiantes en futuras unidades:

Practicar más con punteros y memoria dinámica: Crearé más ejemplos que impliquen la creación de objetos dinámicos, así como la gestión de punteros. Me aseguraré de utilizar delete correctamente para evitar fugas de memoria.

Estudiar conceptos avanzados de punteros: Leeré más sobre punteros inteligentes y técnicas avanzadas para gestionar la memoria de manera eficiente.

Resolver más problemas prácticos: Resolveré problemas en línea que impliquen el uso de punteros, clases y memoria dinámica para consolidar lo aprendido.

Con estos pasos, mejoraré mi comprensión de la memoria dinámica y los punteros, y estaré mejor preparado para aplicar estos conceptos en proyectos más grandes.
