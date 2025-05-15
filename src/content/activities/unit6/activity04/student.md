### Mi solución a la actividad 4

1. Explicación del Patrón State
El Patrón State es un patrón de diseño de comportamiento que permite a un objeto alterar su comportamiento cuando su estado interno cambia. El objeto parece cambiar de clase debido a que delega su comportamiento a diferentes objetos de estado. Este patrón evita el uso de grandes bloques de if/else o switch dentro del objeto principal, lo que mejora la modularidad, la legibilidad y la facilidad de mantenimiento.

Cuándo es útil aplicarlo:
El patrón State es útil cuando un objeto tiene múltiples comportamientos que dependen de su estado interno. Es especialmente eficaz cuando los estados son numerosos o complejos y es necesario evitar una lógica de transición de estado dispersa en toda la clase.

2. Análisis del Caso de Estudio:
Componentes del Patrón State:
Contexto (Context):

La clase Contexto en este caso es Particle, ya que es la clase que mantiene el estado actual y delega el comportamiento en los objetos de estado.

El miembro que mantiene el estado actual es el puntero State* state, que apunta al estado actual de la partícula.

Interfaz State:

La interfaz State está definida por la clase abstracta State.

Los métodos importantes son:

update(Particle* particle): Este método define el comportamiento específico de cada estado al ser llamado en el contexto de la partícula.

onEnter(Particle* particle): Método opcional que se llama cuando una partícula entra en un estado específico.

onExit(Particle* particle): Método opcional que se llama cuando una partícula sale de un estado.

ConcreteState (Estados Concretos):

Las clases que implementan comportamientos específicos son:

NormalState: Representa el estado cuando la partícula se mueve normalmente.

AttractState: Representa el estado cuando la partícula es atraída por el ratón.

RepelState: Representa el estado cuando la partícula es repelida por el ratón.

StopState: Representa el estado cuando la partícula está detenida.

3. Delegación del Comportamiento:
El método Particle::update() delega la lógica de actualización al estado actual de la partícula:

Método Particle::update():

Este método llama a state->update(this), que delega la responsabilidad de la actualización al estado actual de la partícula.

Cada estado tiene su propia implementación de update, por lo que el comportamiento cambia dependiendo del estado.

Comparación de los Métodos update() en los Estados:
NormalState::update(): La partícula se mueve normalmente según su velocidad.

``` c++
particle->position += particle->velocity;
AttractState::update(): La partícula se mueve hacia la posición del ratón (atraída).
```
``` c++
ofVec2f direction = mousePosition - particle->position;
direction.normalize();
particle->velocity += direction * 0.05;
RepelState::update(): La partícula se mueve en dirección opuesta al ratón (repelida).
```
``` c++
ofVec2f direction = particle->position - mousePosition;
direction.normalize();
particle->velocity += direction * 0.05;
StopState::update(): La partícula no se mueve (su velocidad se detiene).
```
``` c++
particle->velocity.x = 0;
particle->velocity.y = 0;
```
Cada clase encapsula un comportamiento específico relacionado con el estado de la partícula.

4. Transiciones de Estado:
¿Cómo cambia una Particle de un estado a otro?

El cambio de estado se maneja a través del método setState(State* newState) en la clase Particle. Este método actualiza el puntero state para apuntar al nuevo estado.

Método setState():

Dentro de setState(), cuando el estado de la partícula cambia, el método primero llama a onExit() del estado anterior (si es que se usó). Luego, el nuevo estado se asigna y se llama a onEnter() del nuevo estado. Esto permite que se gestionen las transiciones correctamente.

Importancia de onEnter y onExit:

onEnter: Se llama cuando una partícula entra en un nuevo estado. Es útil para inicializar o configurar propiedades que son específicas de ese estado.

onExit: Se llama cuando la partícula sale de un estado. Es útil para limpiar o ajustar propiedades antes de cambiar a otro estado.

Ejemplo de uso de onEnter en AttractState: Podría inicializar la velocidad de la partícula para que siempre se mueva hacia el ratón desde el principio.

Ejemplo de uso de onExit en StopState: Podría restablecer propiedades relacionadas con el movimiento, como la velocidad, para evitar que la partícula retenga valores no deseados.

Evento externo que desencadena la llamada a setState():

El evento externo que desencadena la llamada a setState() es un mensaje recibido a través del patrón Observer. En el método Particle::onNotify(), dependiendo del evento recibido (como "attract", "repel", "stop", o "normal"), se llama a setState() para cambiar el estado de la partícula.

5. Resumen y Reflexión:
Propósito del Patrón State:
El patrón State permite que un objeto cambie su comportamiento según su estado interno, evitando el uso de estructuras condicionales grandes. Es útil cuando un objeto debe exhibir comportamientos diferentes en función de su estado, y permite modificar o agregar nuevos comportamientos sin alterar el código que maneja el objeto.

Ventajas de Usar el Patrón State en Particle:
Cohesión: Cada estado es responsable de su propio comportamiento, lo que aumenta la cohesión en las clases de estado.

Extensibilidad: Es fácil agregar nuevos estados sin tener que modificar la lógica de transición o las clases existentes. Solo hay que crear una nueva clase State y gestionar sus transiciones.

Principio Abierto/Cerrado: El patrón sigue este principio, ya que podemos agregar nuevos estados sin modificar el código existente de Particle ni cambiar su lógica central.

Métodos onEnter y onExit:
Estos métodos gestionan la inicialización y la limpieza de las propiedades de la partícula al entrar y salir de un estado. Aunque no todos los estados usan estos métodos extensamente, pueden ser muy útiles para manejar las transiciones de manera organizada y flexible.

6. Diagrama de Estados de la Partícula:
Un diagrama simple de estados de la partícula podría verse así:

```
                +-----------+
                |  Normal   |
                +-----------+
                    |
            "attract" | "repel"
                    |
                +-----------+
                |  Attract  |
                +-----------+
                    |
              "stop" | "normal"
                    |
                +-----------+
                |  Stop     |
                +-----------+
                    |
              "repel" | "attract"
                    |
                +-----------+
                |  Repel    |
                +-----------+
```
