### Mi solucion a la actividad 7

1. ¿Cuál es la diferencia entre un constructor y un destructor en C++?
Constructor: Es un método especial que se ejecuta automáticamente cuando se crea un objeto de una clase. Su propósito es inicializar los miembros del objeto y asignar valores a sus propiedades. En el caso del código que compartiste, el constructor Punto(int _x, int _y) inicializa las coordenadas x e y cuando se crea un objeto Punto.

Destructor: Es otro método especial que se ejecuta automáticamente cuando un objeto es destruido. Su objetivo es liberar cualquier recurso que el objeto haya podido adquirir durante su vida. En el código, el destructor ~Punto() se ejecuta cuando el objeto Punto p es destruido al salir del ámbito de la función main().

2. ¿Cuál es la diferencia entre un objeto y una clase en C++?
Clase: Es una plantilla o molde que define las propiedades y comportamientos comunes a todos los objetos de ese tipo. En el ejemplo, la clase Punto define dos propiedades (x e y) y un par de métodos (el constructor, destructor y imprimir).

Objeto: Es una instancia de una clase. Es la representación concreta de una clase en la memoria. El objeto p es una instancia de la clase Punto con valores específicos para x e y (10 y 20, respectivamente).

3. ¿Qué diferencia notas entre el objeto Punto en C++ y C#?
En C++, Punto p(10, 20); es un objeto en el stack. La memoria para el objeto se asigna en la pila, y el objeto se destruye automáticamente cuando sale del alcance (en este caso, cuando la función main() termina).

En C#, Punto p = new Punto(10, 20); es un objeto en el heap. El objeto p es creado en el heap, y p es una referencia al objeto. La memoria del objeto se maneja automáticamente por el recolector de basura (garbage collector), y el destructor se invoca cuando el recolector de basura decide liberar la memoria.

4. ¿Qué es p en C++ y qué es p en C#?
En C++, p es un objeto real que se almacena directamente en el stack. Es un objeto que ocupa espacio de memoria en la pila y se destruye cuando sale del alcance de la función o del bloque donde fue creado.

En C#, p es una referencia a un objeto. En realidad, lo que se almacena en la variable p es una dirección de memoria en el heap donde está almacenado el objeto. El objeto no se destruye hasta que el recolector de basura lo considere innecesario.

5. ¿En qué parte de memoria se almacena p en C++ y en C#?
En C++, p es un objeto almacenado en el stack. Cuando se declara, su memoria se asigna de forma estática, y al finalizar la ejecución de la función, esa memoria se libera automáticamente.

En C#, p es una referencia que apunta a un objeto almacenado en el heap. El stack contiene solo la dirección de memoria (referencia) del objeto en el heap.


Un objeto en C++ es una instancia de una clase, y la memoria para ese objeto se asigna en el stack si es creado de forma local (como en el caso de Punto p(10, 20);). Un objeto ocupa un bloque contiguo de memoria, donde sus miembros (en este caso x y y) están almacenados en la pila.

Sobre la arquitectura little-endian y big-endian:
Little-endian es el orden en que los bytes de una palabra se almacenan en memoria, comenzando con el byte de menor peso (menos significativo). Esto significa que los números de menor peso se colocan primero en las direcciones de memoria menores.

Si tu arquitectura fuera big-endian, el byte más significativo se almacenaría primero, es decir, en la dirección de memoria más baja.

Si observaras los valores 0a y 14 en hexadecimal, y los convirtieras a decimal:

0a en hexadecimal es 10 en decimal.
14 en hexadecimal es 20 en decimal.
Esto muestra cómo los valores de las variables x y y se almacenan en memoria en orden. En little-endian, los valores menos significativos van primero.


![C__Users_B09S114est_source_repos_ConsoleApplication7_x64_Debug_ConsoleApplication7 exe 20_03_2025 8_57_37 a  m](https://github.com/user-attachments/assets/f012ce40-0a67-4436-a493-0d2464b55ab8)

![ConsoleApplication7 (Depuración) - Microsoft Visual Studio 20_03_2025 9_01_08 a  m](https://github.com/user-attachments/assets/bd5e4be0-cfa2-4f6c-9cae-fc8628891992)

