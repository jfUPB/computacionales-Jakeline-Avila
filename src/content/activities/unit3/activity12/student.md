### Mi solución a la actividad 12

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
    {
        cout << "Inicio del bloque" << endl;
        Punto pBloque(100, 200);
        pBloque.imprimir();
    }
    cout << "Fuera del bloque" << endl;
    // Creación dinámica:
    Punto* pDinamico = new Punto(300, 400);
    pDinamico->imprimir();
    delete pDinamico;

    {
        cout << "Inicio del bloque 2" << endl;
        Punto* pBloque2 = new Punto(500, 600);
        pBloque2->imprimir();
    }
    pBloque2->imprimir();  // ERROR
    delete pBloque2;  // ERROR

    return 0;
}

```

¿Compila el código anterior?
- No, no compila debido a los siguientes errores:

- pBloque2 no es accesible fuera de su bloque. El puntero pBloque2 es creado dentro de un bloque, lo que significa que su vida está limitada al bloque en el que se declaró. Cuando intentas acceder a pBloque2 fuera de ese bloque (después de la segunda impresión), el compilador reporta un error porque el puntero ya ha salido de su ámbito.

- El alcance de la variable pBloque2 está restringido al bloque en el que fue declarada, por lo que al intentar usarla fuera de su bloque, se incurre en un error de compilación.

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
    {
        cout << "Inicio del bloque" << endl;
        Punto pBloque(100, 200);
        pBloque.imprimir();
    }

    Punto* pBloque2 = nullptr;  // Declarado fuera del bloque
    {
        cout << "Inicio del bloque 2" << endl;
        pBloque2 = new Punto(500, 600);
        pBloque2->imprimir();
    }
    pBloque2->imprimir();  // Ahora es válido
    delete pBloque2;

    return 0;
}

```

- ¿Qué ocurre y por qué?
pBloque2 se declara fuera del bloque, lo que significa que tiene un alcance global en el main(). Esto permite que se acceda a él desde cualquier parte del main().

En el bloque, pBloque2 se inicializa con new, lo que crea un objeto dinámicamente en la memoria heap. El puntero pBloque2 sigue apuntando al objeto creado en la heap, y, por lo tanto, el objeto persiste incluso después de salir del bloque.

Después del bloque, pBloque2 sigue siendo accesible y, como el objeto sigue existiendo en la heap, se puede invocar delete para liberar la memoria correctamente.

#### Respuesta a las preguntas clave:
- ¿Por qué el objeto pBloque se destruye al salir del bloque y pBloque2 no?

pBloque es un objeto en el stack, por lo que se destruye automáticamente cuando sale del bloque. En cambio, pBloque2 es un puntero a un objeto en el heap, lo que significa que la memoria del objeto persiste hasta que se invoque delete.

- ¿pBloque2 es un objeto o una referencia a un objeto?

pBloque2 es un puntero (referencia) a un objeto. No es el objeto en sí, sino una dirección de memoria donde el objeto reside.

- ¿En qué parte de la memoria se almacena pBloque2?

El puntero pBloque2 se almacena en la pila (stack), ya que es una variable local. Sin embargo, el objeto al que apunta se almacena en la memoria dinámica (heap), ya que fue creado con new.

- ¿En qué parte de la memoria se almacena el objeto al que apunta pBloque2?

El objeto al que pBloque2 apunta está en la memoria dinámica (heap), porque fue creado usando new.
