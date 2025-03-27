### Mi solucion a la actividad 10

Función que recibe el objeto por valor
``` c++
void cambiarNombre(Punto p, string nuevoNombre) {
    p.name = nuevoNombre;
}
```
Comportamiento:
Pasaje por valor:
Cuando llamas a cambiarNombre(original, "cambiado"), se crea una copia local del objeto original. Dentro de la función, se modifica el atributo name de esa copia.

Destrucción de la copia:
Al salir de la función, la copia (la variable local p) se destruye. Esto genera el mensaje
Destructor: Punto cambiado(70, 80) destruido.
porque la copia, ya modificada, es destruida.

Objeto original intacto:
El objeto original que se creó en main permanece en el stack y no es modificado, ya que la función trabajó sobre una copia. Por ello, cuando se vuelve a llamar a original.imprimir(), se observa el nombre original ("original").

Ubicación en memoria:
original:
Se encuentra en el stack, en una dirección asignada para variables locales de main.

p (la copia dentro de cambiarNombre):
También se ubica en el stack, pero en un marco de pila (stack frame) correspondiente a la función cambiarNombre.
No son el mismo objeto: La copia tiene su propia dirección de memoria, diferente de la de original.

2. Función que recibe el objeto por referencia
Modificación de la función:
``` c+++
void cambiarNombre(Punto& p, string nuevoNombre) {
    p.name = nuevoNombre;
}
```
Comportamiento:
Pasaje por referencia:
Se pasa una referencia al objeto original. Esto significa que la función recibe un alias directo del objeto en main.

Modificación directa:
Al cambiar p.name, se está modificando directamente el objeto original.
Por ello, cuando se llame a original.imprimir(), se verá el nombre modificado ("cambiado").

No hay copia ni destrucción:
Al no crearse una copia, no se invoca el destructor para ningún objeto temporal.
Solo se modifica el mismo objeto.

3. Función que recibe el objeto por puntero
Modificación de la función y llamada en main:

``` c++
void cambiarNombre(Punto* p, string nuevoNombre) {
    p->name = nuevoNombre;
}

int main() {
    // Objeto original en el stack
    Punto original("original", 70, 80);
    original.imprimir();

    cambiarNombre(&original, "cambiado");
    original.imprimir();
    return 0;
}
```
Comportamiento:
Pasaje por puntero:
Se pasa la dirección de memoria de original a la función. El puntero p apunta al objeto que está en el stack.

Modificación a través del puntero:
Al hacer p->name = nuevoNombre; se modifica directamente el objeto en main, ya que p apunta a original.

Resultado:
El objeto original se actualiza y su estado se refleja en la impresión posterior.

Diferencias entre pasar un objeto por valor, por referencia y por puntero
Por Valor:

Qué ocurre: Se crea una copia completa del objeto.

Ventaja: La función trabaja sobre una copia y el objeto original no se altera.

Desventaja: Existe un costo de copia y el destructor de la copia se invoca al salir de la función.

Por Referencia:

Qué ocurre: Se pasa un alias del objeto original.

Ventaja: No se crea una copia, lo que mejora el rendimiento, y se puede modificar el objeto original.

Precaución: Hay que tener cuidado con las modificaciones no deseadas, ya que se afecta directamente el objeto original.

Por Puntero:

Qué ocurre: Se pasa la dirección del objeto original.

Ventaja: Similar a la referencia en cuanto a eficiencia y capacidad de modificación del objeto original.

Diferencia sintáctica: Se usa la sintaxis de punteros (por ejemplo, p->atributo), y es necesario pasar la dirección del objeto (usando &).

En resumen, mientras que el pasaje por valor crea una copia independiente (lo que se refleja en la creación y destrucción de la copia en el stack), tanto el pasaje por referencia como por puntero permiten modificar el objeto original ya que se trabaja directamente con él.
