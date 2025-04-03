### Mi solucion a la actividad 2

1. Dibujo de una lista enlazada con 3 nodos y luego con 4 nodos:

``` cpp
[Head] -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | Next] -> [Nodo3 | pos3 | nullptr]
Al agregar un cuarto nodo, la estructura sería:​
``` 
``` cpp
[Head] -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | Next] -> [Nodo3 | pos3 | Next] -> [Nodo4 | pos4 | nullptr]
``` 
Aquí, cada nodo contiene una posición (pos) y un puntero al siguiente nodo (Next). El último nodo apunta a nullptr, indicando el final de la lista.​



``` cpp
[LinkedList]
  head -> [Nodo1 | pos1 | Next]
  tail -> [Nodo3 | pos3 | nullptr]
  size = 3

``` 
En este caso, head apunta al primer nodo, tail al último, y size indica el número total de nodos en la lista.​

3. Importancia de los punteros head, tail y la variable size:

Sin head: No podríamos acceder al inicio de la lista, lo que imposibilitaría recorrerla o manipular sus elementos.​

Sin tail: Agregar un nodo al final requeriría recorrer toda la lista para encontrar el último nodo, aumentando la complejidad temporal de la operación.​

Sin size: No tendríamos una forma rápida de conocer el número de elementos en la lista, lo que podría ser ineficiente en ciertas operaciones que dependen del tamaño.​

4. Importancia del destructor en LinkedList:

El destructor libera la memoria de todos los nodos al destruirse una instancia de LinkedList. Si no se liberara esta memoria, se producirían fugas de memoria, ya que los nodos creados dinámicamente no serían eliminados, consumiendo recursos innecesarios y potencialmente llevando a que el programa se quede sin memoria.​

5. Datos en LinkedList y su relación con los nodos:

LinkedList contiene punteros a head y tail, y la variable size. Estos miembros permiten gestionar y manipular la lista de nodos de manera eficiente. Los nodos contienen la información específica (en este caso, la posición) y el puntero al siguiente nodo, formando la estructura de la lista enlazada.​

6. Gestión de memoria en C++ vs. C#:

En C++, la gestión de memoria es manual; el programador es responsable de asignar y liberar memoria. En C#, existe un recolector de basura que automatiza la liberación de memoria no utilizada. Por ello, en C++ es esencial liberar la memoria de los objetos para evitar fugas, mientras que en C# el recolector de basura maneja esta tarea automáticamente.​

7. Dibujos de LinkedList antes y después de agregar nodos:

Cuando size es 0:

Antes:​

``` cpp
  [LinkedList]
    head -> nullptr
    tail -> nullptr
    size = 0
``` 
Después de agregar un nodo:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | nullptr]
    tail -> [Nodo1 | pos1 | nullptr]
    size = 1
``` 
Cuando size es 1:

Antes:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | nullptr]
    tail -> [Nodo1 | pos1 | nullptr]
    size = 1
``` 
Después de agregar un nodo:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | nullptr]
    tail -> [Nodo2 | pos2 | nullptr]
    size = 2
``` 
Cuando size es 2:

Antes:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | nullptr]
    tail -> [Nodo2 | pos2 | nullptr]
    size = 2

``` 
Después de agregar un nodo:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | Next] -> [Nodo3 | pos3 | nullptr]
    tail -> [Nodo3 | pos3 | nullptr]
    size = 3
``` 
8. Dibujos de LinkedList antes y después de eliminar nodos:

Cuando size es 1:

Antes:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | nullptr]
    tail -> [Nodo1 | pos1 | nullptr]
    size = 1
``` 
Después de eliminar el nodo:​
``` cpp

  [LinkedList]
    head -> nullptr
    tail -> nullptr
    size = 0
``` 
Cuando size es 2:

Antes:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | Next] -> [Nodo2 | pos2 | nullptr]
    tail -> [Nodo2 | pos2 | nullptr]
    size = 2

``` 
Después de eliminar el último nodo:​

``` cpp
  [LinkedList]
    head -> [Nodo1 | pos1 | nullptr]
    tail ->
::contentReference[oaicite:52]{index=52}
``` 
 
