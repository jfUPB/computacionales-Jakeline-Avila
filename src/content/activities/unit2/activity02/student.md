<!--Carga el programa en el simulador y ejecuta paso a paso cada instrucción. Trata de predecir el resultado de la instrucción antes de ejecutarla.
¿En qué direcciones de memoria se implementan las variables i, sum?
Basado en esta experiencia, ¿Cuál es la diferencia entre la dirección de una variable y su contenido?
Explica cómo se implementa la condición i <= 100
Entrega: responde a las cuestiones anteriores en tu bitácora.-->

#### Mi solución a la actividad 2

- ¿En qué direcciones de memoria se implementan las variables i, sum?
- i: @16 y sum: @17, las direcciones de memoria se implementan en la RAM con los respectivos números y contendrán por ejemplo RAM[16] el valor inicial de 1 (valor de i) y RAM[17] contendrá 0 que es el valor de sum; Durante la ejecución estos valores van a cambiar pero sus direcciones en la memoria van a permanecer constantes.

- Basado en esta experiencia, ¿Cuál es la diferencia entre la dirección de una variable y su contenido?
- La dirección se podría decir que es un identificador único dentro de la memoria donde se almacena la variable mientras que el contenido es el valor que se guarda en esta dirección.

- Explica cómo se implementa la condición i <= 100:
- Se implementa utilizando una comparación y salto condicional. Primero se carga i en el registro D (D=M) luego se resta 100 (D=D-A). Si el resultado es positivo (D>0) significa que i es mayor que 100 y el programa salta a la
etiqueta (END), terminando la ejecución del bucle. Si D es menor o igual a 0, el programa continua ejecutando el cuerpo del bucle, sumando i a sum y aumentando i en 1, repitidiendo hasta que i supere 100.
