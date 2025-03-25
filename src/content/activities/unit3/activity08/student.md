### Solucion a la actividad 8

- Explicación de la Diferencia entre Objetos en el Stack y el Heap
Stack (pStack):

Almacenamiento y Gestión: Los objetos creados en el stack se asignan automáticamente cuando se declara la variable y se destruyen al salir del bloque de código (por ejemplo, al finalizar la función main).

Velocidad: La asignación y liberación de memoria en el stack es muy rápida.

Limitaciones: El stack tiene un tamaño limitado, por lo que para objetos muy grandes o un número elevado de objetos, podría producirse un desbordamiento de pila.

Heap (pHeap):

Almacenamiento y Gestión: Los objetos creados en el heap se asignan dinámicamente con new y deben ser liberados manualmente usando delete para evitar fugas de memoria.

Flexibilidad: Permite la creación de objetos con tiempos de vida controlados manualmente y no está limitado por el tamaño del stack.

Costo: La asignación y liberación en el heap suele ser más lenta que en el stack, y se requiere un manejo cuidadoso para evitar errores de memoria.

Análisis de las Variables
pStack:

Naturaleza: Es un objeto real creado en el stack.

Dirección: Su dirección se obtiene usando &pStack y corresponde a la ubicación de memoria del objeto.

¿Objeto o Referencia? Es un objeto, no una referencia. La variable pStack contiene directamente los datos (los miembros x e y) del objeto Punto.

pHeap:

Naturaleza: Es una variable puntero que almacena la dirección de un objeto creado en el heap.

Contenido del Puntero: El valor de pHeap es la dirección en memoria donde se encuentra el objeto Punto dinámicamente asignado.

¿Objeto o Referencia? pHeap es una referencia (más precisamente, un puntero) a un objeto en el heap. No es el objeto en sí; solo contiene la dirección a la que se puede acceder para interactuar con el objeto.

- Observación en Memory1
Procedimiento:

En la ventana Memory1 del depurador, se introduce la dirección &pHeap (la dirección de la variable puntero en el stack).

Al presionar Enter, se muestra el contenido de esa dirección de memoria. Este contenido es el valor almacenado en pHeap, es decir, la dirección del objeto en el heap (por ejemplo, 0x00B5F8D0).

Comparación con Locals:

La dirección mostrada en Memory1 coincide exactamente con el valor de pHeap que se visualiza en la pestaña Locals.

Significado: Esto confirma que la variable pHeap almacena efectivamente la dirección del objeto en el heap. Es una validación de que el puntero apunta correctamente a la región de memoria donde se encuentra el objeto creado con new.
