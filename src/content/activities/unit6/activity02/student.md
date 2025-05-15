### Mi solucion a la actividad 2

- Identifica los Roles:

¿Qué clase actúa como la interfaz Observer? ¿Qué método define?
¿Qué clase actúa como Subject? ¿Qué métodos proporciona para gestionar observadores y notificar?
¿Qué clase es el ConcreteSubject en esta aplicación? ¿Por qué? (Pista: ¿Quién envía las notificaciones?)
¿Qué clase(s) actúan como ConcreteObserver? ¿Por qué? (Pista: ¿Quién recibe y reacciona a las notificaciones?)

- Respuestas:

Interfaz Observer: La clase Observer define el método onNotify(), que debe ser implementado por cualquier clase que desee recibir notificaciones de un sujeto.

Subject: La clase Subject gestiona la lista de observadores, proporcionando los métodos addObserver(), removeObserver(), y notify() para agregar, eliminar y notificar a los observadores respectivamente. El sujeto en este caso es la clase ofApp, que notifica a los observadores (las partículas) cuando el usuario presiona teclas (por ejemplo, "attract", "repel", "stop").

ConcreteSubject: ofApp también actúa como el ConcreteSubject, ya que es quien envía las notificaciones a los observadores. Cuando el usuario presiona una tecla, ofApp llama a notify() para informar a todos los observadores (las partículas) sobre el cambio de estado.

ConcreteObserver: Las instancias de la clase Particle son los ConcreteObservers, ya que implementan onNotify() y reaccionan a los eventos enviados por ofApp, cambiando su estado (por ejemplo, pasando de NormalState a AttractState).

- Sigue el flujo de notificación:

Localiza el método keyPressed en ofApp.cpp. ¿Qué sucede cuando se presiona la tecla ‘a’? ¿Qué método se llama?
Ve al método notify en la clase Subject. ¿Qué hace este método?
Localiza el método que implementa la interfaz Observer en la clase Particle (onNotify). ¿Qué hace este método cuando recibe el evento “attract”?

Respuestas: 

#### Método keyPressed en ofApp.cpp:

Cuando se presiona la tecla 'a', se ejecuta el siguiente bloque de código dentro de keyPressed:

``` c++
if (key == 'a') {
    notify("attract");
}
```
Este bloque llama al método notify() de la clase Subject (que es ofApp en este caso) y pasa el evento "attract".

#### Método notify en la clase Subject:

El método notify recorre la lista de observadores (en este caso, las partículas) y llama a onNotify() de cada uno de ellos:

``` c+
void Subject::notify(const std::string& event) {
    for (Observer* observer : observers) {
        observer->onNotify(event);
    }
}
```
El método se encarga de pasar el evento "attract" a todos los observadores registrados (que son las partículas).

#### Método onNotify en la clase Particle:

La clase Particle implementa la interfaz Observer y su método onNotify(). Cuando una partícula recibe el evento "attract", el método onNotify de la clase Particle se ejecuta:

``` c+
void Particle::onNotify(const std::string& event) {
    if (event == "attract") {
        setState(new AttractState());
    }
    // Otros eventos...
}
```
Cuando el evento es "attract", este método cambia el estado de la partícula llamando a setState(new AttractState()). Esto hace que la partícula cambie su comportamiento, pasando de su estado actual a un nuevo estado de atracción (AttractState).

- Registro y eliminación de observadores:

¿En qué parte del código se añaden las instancias de Particle como observadores de ofApp? (Busca dónde se llama a addObserver).
Aunque no se usa explícitamente en este ejemplo simple, ¿Dónde se eliminarían los observadores si fuera necesario (por ejemplo, si una partícula se destruyera durante la ejecución)? (Busca removeObserver). ¿Por qué es importante el destructor de ofApp en este contexto?

Respuesta:

Las instancias de Particle se añaden como observadores de ofApp en el método setup() de la clase ofApp. Específicamente, se llama a addObserver() para registrar cada partícula en la lista de observadores. Aquí está el código relevante:

``` c+
void ofApp::setup() {
    ofBackground(0);
    // Crear partículas usando la fábrica
    for (int i = 0; i < 100; ++i) {
        Particle* p = ParticleFactory::createParticle("star");
        particles.push_back(p);
        addObserver(p);  // Se agrega la partícula como observador
    }

    for (int i = 0; i < 5; ++i) {
        Particle* p = ParticleFactory::createParticle("shooting_star");
        particles.push_back(p);
        addObserver(p);  // Se agrega la partícula como observador
    }

    for (int i = 0; i < 10; ++i) {
        Particle* p = ParticleFactory::createParticle("planet");
        particles.push_back(p);
        addObserver(p);  // Se agrega la partícula como observador
    }
}
```
En este bloque de código, cada vez que se crea una nueva partícula, se agrega a la lista de observadores de ofApp mediante la llamada a addObserver(p).

Eliminación de Observadores:
Aunque en este ejemplo no se elimina explícitamente ningún observador, si fuera necesario eliminar una partícula de la lista de observadores (por ejemplo, si una partícula se destruye), se usaría el método removeObserver() de la clase Subject. El código para eliminar un observador se vería algo así:

``` c+
void ofApp::removeObserver(Observer* observer) {
    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}
```
Este método recorrería la lista de observadores y eliminaría la partícula que se haya destruido o que ya no quiera recibir notificaciones.

Importancia del Destructor de ofApp:
El destructor de ofApp es importante en este contexto porque, si las partículas se destruyen durante la ejecución, el objeto ofApp necesita asegurarse de que se eliminen adecuadamente de la lista de observadores. Si una partícula se destruye pero no se elimina de la lista de observadores, se produciría un error al intentar notificar a un puntero que ya no es válido (por ejemplo, acceso a memoria que ya ha sido liberada).

Idealmente, el destructor de ofApp debería llamar a removeObserver() para eliminar las partículas que están siendo destruidas antes de que se destruya el objeto ofApp. Esto evitaría tener punteros colgantes (dangling pointers) y garantizaría que no se intente notificar a observadores ya eliminados.

El destructor de ofApp podría verse así:

``` c+
ofApp::~ofApp() {
    // Eliminar todas las partículas como observadores antes de destruirlas
    for (Particle* p : particles) {
        removeObserver(p);  // Elimina la partícula de la lista de observadores
        delete p;  // Destruye la partícula
    }
}
```
