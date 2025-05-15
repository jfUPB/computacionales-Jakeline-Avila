### Mi solución a la actividad 2

``` c++
#include <iostream>

using namespace std;

// Intercambio por valor (NO MODIFICA LAS VARIABLES ORIGINALES)
void swapPorValor(int a, int b) {
    a = a + b;
    b = a - b;
    a = a - b;
}

// Intercambio por referencia (MODIFICA LAS VARIABLES ORIGINALES)
void swapPorReferencia(int& a, int& b) {
    a = a + b;
    b = a - b;
    a = a - b;
}

// Intercambio por puntero (MODIFICA LAS VARIABLES ORIGINALES)
void swapPorPuntero(int* a, int* b) {
    *a = *a + *b;
    *b = *a - *b;
    *a = *a - *b;
}

int main() {
    int x = 5, y = 10;

    cout << "Valores iniciales: x = " << x << ", y = " << y << endl;

    // Prueba de swap por valor
    swapPorValor(x, y);
    cout << "Despues de swapPorValor: x = " << x << ", y = " << y << " (No cambia)" << endl;

    // Restablecer valores originales
    x = 5;
    y = 10;

    // Prueba de swap por referencia
    swapPorReferencia(x, y);
    cout << "Despues de swapPorReferencia: x = " << x << ", y = " << y << " (Cambia)" << endl;

    // Restablecer valores originales
    x = 5;
    y = 10;

    // Prueba de swap por puntero
    swapPorPuntero(&x, &y);
    cout << "Despues de swapPorPuntero: x = " << x << ", y = " << y << " (Cambia)" << endl;

    return 0;
}
```

#### Solucion a preguntas:

1. ¿Por qué la versión de swapPorValor no logra intercambiar los valores de x e y en main()?

- swapPorValor(int a, int b) recibe copias de x e y, por lo que cualquier cambio dentro de la función no afecta a las variables originales en main().

- Se modifica solo en la función, pero al salir de ella, esas modificaciones se pierden.



2. ¿Cómo y por qué logran las otras dos funciones (swapPorReferencia y swapPorPuntero) modificar las variables originales?

- swapPorReferencia(int &a, int &b) usa referencias, que son alias de x e y, por lo que cualquier cambio en a y b afecta a las variables originales.

- swapPorPuntero(int *a, int *b) recibe las direcciones de x e y. Usando *a y *b, se modifican directamente los valores originales.



3. ¿Cuáles son las ventajas y consideraciones de usar referencias versus punteros en este caso?

- Referencias

- Más seguras y fáciles de usar porque no requieren desreferenciación (*).

- No pueden ser nullptr, evitando errores de acceso a memoria inválida.

- Siempre refieren a la misma variable.


- Punteros

- Más flexibles, permiten apuntar a diferentes direcciones en tiempo de ejecución.

- Necesitan verificación (nullptr), ya que pueden apuntar a memoria no válida.

- Útiles en estructuras dinámicas y manejo de memoria.
