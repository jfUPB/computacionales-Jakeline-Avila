<!--Profundizando en las instrucciones del lenguaje ensamblador
Enunciado: el documento "Machine Language" describe dos tipos de instrucciones en el lenguaje ensamblador Hack: A-instructions y C-instructions (páginas 64-69).

¿Cuál es la función de cada tipo de instrucción?
¿Cómo se representa cada tipo de instrucción en binario?
Proporciona al menos 3 ejemplos de cada tipo de instrucción, explicando qué hace cada una.
Puedes usar las tablas de las páginas 67 y 69 del documento como referencia para los códigos de operación (comp), destinos (dest) y saltos (jump).
Entrega: la solución a cada una de las preguntas planteadas en el enunciado.-->
### Mi solución a la actividad 4


##### ¿Cúal es la función de cada tipo de instrucción?

- A-instruction: Esta instrucción llamada también *address instruction* hace que el ordenador almacene el valor especificado en el registro A. La instrucción A se utiliza para tres propósitos diferentes.
En primer lugar, proporciona la única forma de introducir una constante en el ordenador bajo el control del programa. En segundo lugar, prepara el escenario para una instrucción C
posterior diseñada para manipular una determinada posición de memoria de datos, estableciendo primero A en la dirección de esa posición. En tercer lugar, prepara el escenario para una
instrucción C posterior que especifique un salto, cargando primero la dirección del destino del salto en el registro A.

- C-instruction: La instrucción C llamada también *compute instruction* es la instrucción que lo hace casi todo. El código de la instrucción es una especificación que responde a tres preguntas: (a) qué calcular, (b)
dónde almacenar el valor calculado y (c) qué hacer a continuación. Junto con la instrucción A, estas especificaciones determinan todas las operaciones posibles del ordenador.

##### ¿Cómo se representa cada tipo de instrucción en binario?

- A-instruction: Comienza con un 0 seguido de 15-bits que representan básicamente la dirección o el valor númerico = 0 vvv vvvv vvvv vvvv
- C-instruction: Comienza con los bits iniciales 111 seguidos por comp (7 bits) que es el que especifica la operación osea que computar, seguido de dest (3 bits) que indica donde se almacenará el resultado y sigue jump (3 bits) que especifica
la condicion para realizar el salto, es decir, qué comando obtener y ejecutar a continuación. = 1 1 1 a c1 c2 c3 c4 c5 c6 d1 d2 d3 j1 j2 j3/111a cccc ccdd djjj.

##### Proporciona al menos 3 ejemplos de cada tipo de instrucción, explicando qué hace cada una.

A-instructions:

1. Instrucción: @2  
Binario: 0000000000000010   
Función: Carga el valor 2 en el registro A. Esto podría usarse, por ejemplo, para acceder a la posición de memoria 2.  


2. Instrucción: @5   
Binario: 0000000000000101  
Función: Hace que el ordenador almacene la representación binaria de 5 en el registro A.  


3. Instrucción: @1024  
Binario: 0000010000000000  
Función: Carga la dirección 1024 en el registro A.  

C-instructions:

1. Instrucción: D=A  
Binario: 1110110000010000  
Función: Copia el valor del registro A en el registro D (destino). No modifica la memoria.  


2. Instrucción: M=D+1  
Binario: 1110011111010000  
Función: Suma 1 al valor del registro D y almacena el resultado en la posición de memoria apuntada por el registro A.  


3. Instrucción: D;JGT  
Binario: 1110001100000001   
Función: Realiza un salto condicional si el valor del registro D es mayor que 0. Si la condición no se cumple, la ejecución continúa normalmente.  
