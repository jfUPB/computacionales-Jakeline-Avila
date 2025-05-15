### Mi solucion a la actividad 9

Comportamiento en C++
Código y Ejecución
En el código C++ se crea un objeto llamado original en el stack y, luego, se copia en otro objeto llamado copia mediante la asignación:

``` c++
Punto original("original", 70, 80);
original.imprimir();
Punto* p = &original;  // p apunta a original

// Copia del objeto
Punto copia = original;
copia.name = "copia";
copia.x = 100;
copia.y = 200;
copia.imprimir();
original.imprimir();


// Modificamos original a través del puntero p
p->name = "p";
p->x = 300;
p->y = 400;
p->imprimir();
original.imprimir();
```
Observaciones en el Depurador
Direcciones de Memoria Diferentes:
Al colocar breakpoints en la creación de original y en la línea de la copia, se observa que original y copia tienen direcciones de memoria distintas. Esto confirma que se han creado dos instancias independientes.

Modificación Independiente:
Cuando se modifica copia, los cambios no afectan a original. Por ejemplo, al asignar nuevos valores a los miembros de copia, la impresión posterior de original muestra sus valores originales (o los que se hayan modificado directamente sobre él), indicando que se trata de objetos separados.

Conclusión para C++
¿Qué es copia en C++?
La instrucción Punto copia = original; utiliza el constructor de copia para crear una nueva instancia.

¿Es una copia independiente de original?
Sí, es una copia independiente: cada objeto reside en su propia dirección de memoria (lo puedes corroborar en el depurador) y las modificaciones en uno no afectan al otro.

Comportamiento en C#
Código y Ejecución
En el ejemplo de C#, se utiliza una clase para definir a Punto y se realiza la siguiente asignación:

``` c++
Punto original = new Punto("original", 70, 80);
original.Imprimir();

Punto copia = original;
copia.name = "copia";
copia.x = 100;
copia.y = 200;
copia.Imprimir();
original.Imprimir();
``` 
Observaciones en el Depurador
Misma Dirección de Memoria:
En C#, las clases son tipos de referencia. Al hacer Punto copia = original;, copia no se crea como una nueva instancia, sino que se copia la referencia a la misma instancia que original. En el depurador se observa que ambas variables apuntan a la misma dirección de memoria.

Modificación Compartida:
Dado que copia y original refieren al mismo objeto, cualquier modificación realizada a través de copia afecta directamente a original. Por eso, al cambiar los valores de los atributos mediante copia, la impresión posterior de original muestra esos cambios.

Conclusión para C#
¿Qué es copia en C#?
La asignación Punto copia = original; copia la referencia al objeto, no el objeto en sí.

¿Es una copia independiente de original?
No, no es independiente. Ambas variables apuntan a la misma instancia. Para obtener una copia independiente, se debería implementar un mecanismo de clonación (por ejemplo, mediante un método Clone) o usar un struct en lugar de una clase (ya que los structs son tipos de valor y se copian por valor).

Resumen de Diferencias
C++:

Copia por Valor: La copia de un objeto crea una nueva instancia en una dirección de memoria distinta.

Constructor de Copia: Se invoca el constructor de copia, lo que permite personalizar la copia si es necesario.

Independencia: Las modificaciones en la copia no afectan al objeto original.

C#:

Copia por Referencia: Al asignar un objeto de una clase, solo se copia la referencia, por lo que ambos nombres (variables) apuntan al mismo objeto en memoria.

Misma Instancia: Las modificaciones realizadas a través de cualquiera de las variables afectan al mismo objeto.

Clonación Necesaria para Independencia: Para obtener una copia independiente se debe implementar un método de clonación o utilizar tipos de valor (structs).

