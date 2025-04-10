### Mi solucion a la actividad 4

¿Qué es una cola?
Concepto:
Una cola es una estructura de datos donde los elementos se agregan al final (cola) y se eliminan desde el frente. Es como una línea de espera: el primer elemento que se ingresa es el primero en salir.

  [A] <- front      rear -> [B] [C] [D]
En este dibujo:

A es el primer elemento que entró y está en la parte delantera (front).

D es el último elemento que se añadió y está en la parte trasera (rear).

¿Cómo se implementa enqueue() y dequeue()?
enqueue()

Función: Agrega un nuevo elemento al final de la cola.

Pasos:

Crea un nuevo nodo con los datos que quieres almacenar.

Si la cola está vacía, asigna ese nodo tanto a front como a rear.

Si no está vacía, enlaza el nodo actual de rear al nuevo nodo y actualiza rear para que apunte a este último.

Analogía: Es como cuando una nueva persona llega a la fila, se pone al final de la fila.

dequeue()

Función: Elimina el elemento del frente de la cola, que es el que ha estado más tiempo en la fila.

Pasos:

Verifica que la cola no esté vacía.

Guarda en una variable temporal el nodo que está en front.

Actualiza front para que apunte al siguiente nodo en la fila.

Libera la memoria del nodo eliminado.

Si después de eliminar se queda la cola vacía, asegúrate de actualizar también rear a nullptr.

Analogía: Es como cuando la persona que está en la parte delantera de la fila es atendida y se retira.

Un error común y cómo evitarlo
Error:
No actualizar correctamente los punteros front y rear.

Problema:
Si en dequeue() olvidas actualizar rear cuando se elimina el último nodo, podrías tener un puntero colgante (dangling pointer) que apunta a memoria ya liberada. Esto puede generar errores o comportamientos inesperados en tu programa.

Cómo evitarlo:
Después de eliminar el nodo del frente, revisa si la cola quedó vacía. Si es así, asigna rear = nullptr. Esto garantiza que ambos punteros reflejen correctamente el estado vacío de la cola.

Resumen visual de la operación
Antes de dequeue():


front -> [A] -> [B] -> [C] -> nullptr
         ↑
        El que se eliminará
Después de dequeue():


front -> [B] -> [C] -> nullptr
En resumen, la implementación de una cola requiere:

Agregar elementos al final con enqueue().

Eliminar el elemento del frente con dequeue(), siempre cuidando de actualizar correctamente los punteros.

Mantener la coherencia de la estructura para evitar errores como punteros colgantes o fugas de memoria.
