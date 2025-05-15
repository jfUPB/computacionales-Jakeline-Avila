### Mi solucion a la actividad 11

Análisis de la Clase Contador
La clase Contador tiene dos tipos de miembros:

Miembro de Instancia (valor):

Naturaleza: Cada objeto creado de la clase Contador posee su propia copia de la variable valor.

Ubicación en memoria:

Cuando se crea un objeto en el stack (por ejemplo, c1 y c2), su miembro valor se almacena junto con el objeto en la pila.

Cuando se crea un objeto de forma dinámica (por ejemplo, el objeto al que apunta c3), el objeto se aloja en el heap.

Ejemplo:

c1 y c2 están en el stack, y sus respectivos valor están dentro de sus bloques de memoria en la pila.

La variable c3 es un puntero (almacenado en el stack) que apunta al objeto Contador que se ha creado en el heap. Por lo tanto, el puntero c3 está en el stack, pero el objeto al que apunta (donde se encuentra su miembro valor) está en el heap.

Miembro Estático (total):

Naturaleza:

total es compartido por todas las instancias de la clase.

Se incrementa cada vez que se crea un objeto de la clase Contador.

Ubicación en memoria:

Los miembros estáticos se almacenan en un segmento global de la memoria (normalmente en la sección de datos globales o en el segmento de datos estáticos), no dentro del stack de cada objeto.

Observación:

Al inspeccionar con el depurador, verás que Contador::total tiene la misma dirección (o ubicación en el espacio global) independientemente del objeto desde el cual se acceda.

Experimentos con el Depurador y Resultados
Creación y Ubicación de c1 y c2 (Objetos en el Stack):

Al crear Contador c1(5); y Contador c2(10); en main, ambos objetos se asignan en el stack.

Cada uno contiene su propio miembro valor en su bloque de memoria.

Al utilizar el depurador, al inspeccionar &c1 y &c2, se muestran direcciones diferentes propias del stack.

Creación y Ubicación de c3 (Objeto en el Heap):

La variable c3 es declarada como un puntero en el stack:

``` 
Contador* c3 = new Contador(15);
``` 
c3 (la variable puntero):

Se encuentra en el stack, ya que es una variable local en main.

El objeto al que apunta c3:

Se encuentra en el heap, ya que se ha asignado dinámicamente con new.

Al inspeccionar con el depurador, notarás que:

La dirección de c3 (usando &c3) corresponde a la ubicación del puntero en el stack.

El valor almacenado en c3 (la dirección a la que apunta) corresponde al objeto en el heap. Si inspeccionas esa dirección (por ejemplo, en la ventana Memory1), verás los datos del objeto, incluido su valor.

Miembro Estático Contador::total:

Independientemente de dónde se creen los objetos, Contador::total se aloja en un área global de memoria (datos estáticos).

Al añadir un watch en el depurador para Contador::total, verás que su valor se incrementa con cada creación de objeto y su ubicación es común a todos.

Conclusiones sobre Miembros Estáticos e Instancia
Miembros de Instancia (valor):

Gestión:
Cada objeto tiene su propia copia de los miembros de instancia.
Se almacenan en el stack si el objeto es local, o en el heap si se crea dinámicamente.

Ventajas:
Permiten que cada objeto mantenga su estado individual.
Son fáciles de gestionar sin preocupaciones de sincronización entre objetos.

Desventajas:
Cada copia ocupa espacio adicional en memoria.

Miembros Estáticos (total):

Gestión:
Son compartidos por todos los objetos de la clase y se almacenan en un segmento global (o datos estáticos).
Se inicializan una única vez y persisten durante la vida del programa.

Ventajas:
Permiten llevar un control o compartir información común entre todas las instancias sin necesidad de copiar datos.
Útiles para contadores globales, configuraciones o recursos compartidos.

Desventajas:
Se debe tener cuidado con la sincronización en entornos multihilo, ya que varios objetos pueden modificar el mismo dato.

Resumen de la Ubicación en Memoria
c1 y c2:

Se almacenan en el stack.

Cada uno contiene su propio miembro valor dentro de su bloque de memoria.

c3:

La variable c3 (puntero):

Está almacenada en el stack.

El objeto al que apunta c3:

Se aloja en el heap (por asignación dinámica con new).

Contador::total:

Almacenado en el segmento global o de datos estáticos, accesible por todas las instancias.
