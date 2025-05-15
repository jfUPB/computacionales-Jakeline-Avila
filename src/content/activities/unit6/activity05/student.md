### Mi solución a la actividad 5

![image](https://github.com/user-attachments/assets/0e2109a7-cbde-4b2d-82f5-b54001e1579d)


#### Descripción del Proyecto
Mi proyecto es una aplicación de arte generativo interactivo en la que un conjunto de partículas se mueve por la pantalla de forma autónoma, pero su comportamiento cambia dependiendo de la interacción del usuario. Al presionar ciertas teclas del teclado, las partículas cambiarán su comportamiento, como moverse hacia el mouse, alejarse de él, detenerse o volver a su comportamiento normal.

El usuario interactúa con las partículas mediante el teclado:

'a': las partículas se sienten atraídas hacia el mouse (usando el patrón State para cambiar el comportamiento).

'r': las partículas se repelen del mouse.

's': las partículas se detienen.

'n': las partículas vuelven a su comportamiento normal.

Cada partícula tiene un tipo único (como estrellas, cometas y planetas), lo cual es gestionado por una fábrica de partículas.

#### Diseño con Patrones
Observer
Sujeto: En este caso, el sujeto es la clase ofApp, que maneja la interacción del usuario y controla el flujo general del programa.

Observadores: Los observadores son las partículas (Particle). Cada partícula está registrada como observadora del sujeto y responde a eventos como cambios de estado (atracción, repulsión, etc.).

Eventos: Los eventos que se notifican son los cambios de estado, como "attract", "repel", "stop", y "normal". Estos eventos son enviados a todas las partículas, que luego reaccionan de acuerdo a su estado actual.

Prueba: La notificación se realiza en el método keyPressed de la clase ofApp. Dependiendo de la tecla presionada, el sujeto notifica a todos los observadores (las partículas) que cambien su comportamiento.

Fragmento de código:

``` c++
void ofApp::keyPressed(int key) {
    if (key == 'a') {
        notify("attract");
    }
    else if (key == 'r') {
        notify("repel");
    }
    else if (key == 's') {
        notify("stop");
    }
    else if (key == 'n') {
        notify("normal");
    }
}
```
#### Factory Method
Clase Factory: La clase ParticleFactory es responsable de crear diferentes tipos de partículas. Tiene un método estático createParticle, que acepta un tipo de partícula y devuelve una nueva instancia de una partícula con las características específicas de ese tipo.

Productos: La fábrica crea tres tipos de partículas: "star" (estrella), "comet" (cometa) y "planet" (planeta), con diferentes características como el tamaño, color y velocidad.

Razón para usar la factory: Usé la fábrica porque quería desacoplar la creación de partículas del código principal. Esto facilita la extensión del sistema en el futuro si quisiera agregar más tipos de partículas sin cambiar la lógica principal.

Prueba: La fábrica crea las partículas con las características apropiadas dependiendo del tipo y luego las devuelve. Verifiqué que se crearan correctamente a través de los métodos ParticleFactory::createParticle() y que las partículas respondieran adecuadamente a la interacción del usuario.

Fragmento de código:

``` c++
Particle* ParticleFactory::createParticle(const std::string& type) {
    Particle* particle = new Particle();

    if (type == "star") {
        particle->size = ofRandom(5, 10);
        particle->color = ofColor(255, 255, 0);  // Yellow
    }
    else if (type == "comet") {
        particle->size = ofRandom(10, 15);
        particle->color = ofColor(255, 0, 0);  // Red
        particle->velocity *= 2;
    }
    else if (type == "planet") {
        particle->size = ofRandom(12, 18);
        particle->color = ofColor(0, 0, 255);  // Blue
    }

    return particle;
}
```
State
Contexto: En este caso, el contexto es la clase Particle, que cambia su comportamiento basado en su estado actual.

Estados: Los estados definidos son:

NormalState: El comportamiento de la partícula es moverse aleatoriamente.

AttractState: La partícula se mueve hacia el mouse.

RepelState: La partícula se aleja del mouse.

StopState: La partícula se detiene.

Transiciones de estado: Los cambios de estado ocurren cuando el usuario presiona diferentes teclas, lo que notifica a las partículas que cambien su estado. La transición es gestionada por el patrón State, y el comportamiento cambia en consecuencia.

Prueba: Probé que los estados funcionen cambiando el comportamiento de las partículas al presionar las teclas correspondientes. Usé std::cout y ofLogNotice para verificar que las partículas cambiaban de estado correctamente.

Fragmento de código:

``` c++
void NormalState::update(Particle* particle) {
    particle->position += particle->velocity;
}

void AttractState::update(Particle* particle) {
    ofVec2f mousePos(((ofApp*)ofGetAppPtr())->mouseX, ((ofApp*)ofGetAppPtr())->mouseY);
    ofVec2f direction = mousePos - particle->position;
    direction.normalize();
    particle->velocity += direction * 0.1;
    particle->position += particle->velocity;
}

void RepelState::update(Particle* particle) {
    ofVec2f mousePos(((ofApp*)ofGetAppPtr())->mouseX, ((ofApp*)ofGetAppPtr())->mouseY);
    ofVec2f direction = particle->position - mousePos;
    direction.normalize();
    particle->velocity += direction * 0.1;
    particle->position += particle->velocity;
}

void StopState::update(Particle* particle) {
    particle->velocity = ofVec2f(0, 0);
}
```
#### Integración de los Tres Patrones
Los tres patrones se integran de la siguiente manera:

Observer: El ofApp es el sujeto y notifica a todas las partículas (observadores) cuando un evento (como una tecla presionada) ocurre. Las partículas responden a estos eventos cambiando su estado.

Factory Method: La clase ParticleFactory crea diferentes tipos de partículas, y las partículas se gestionan dentro de la clase ofApp. Al agregar nuevas partículas, las características específicas (como el tipo de partícula) se manejan mediante la fábrica.

State: Cada partícula tiene un estado que define su comportamiento. Dependiendo de los eventos, las partículas pueden cambiar su estado, lo que a su vez cambia su comportamiento (movimiento hacia el mouse, alejándose, etc.).

Un escenario de interacción sería el siguiente:

El usuario presiona la tecla 'a' para atraer las partículas hacia el mouse. El sujeto (de la clase ofApp) notifica a todas las partículas que deben cambiar su comportamiento a AttractState. Las partículas luego se mueven hacia el mouse gracias al comportamiento definido en AttractState.

#### Desafíos y Soluciones
Desafío: El mayor desafío fue integrar correctamente los tres patrones sin que se superpongan o interfieran entre sí. En particular, asegurarse de que la notificación del patrón Observer se realizara correctamente y que las partículas pudieran cambiar su comportamiento sin generar errores.

Solución: Para resolver esto, probé cada patrón por separado en fases. Primero, aseguré que las partículas pudieran cambiar de estado sin problemas, luego implementé la notificación de eventos con Observer, y finalmente integré la fábrica para crear diferentes tipos de partículas. El uso de mensajes de depuración (std::cout y ofLogNotice) me permitió verificar cada parte del proceso.

Código completo:

Ofapp.h

``` c++
#pragma once

#include "ofMain.h"
#include <vector>
#include <string>

// Observer Pattern
class Observer {
public:
    virtual void onNotify(const std::string& event) = 0;
};

class Subject {
public:
    void addObserver(Observer* observer);
    void removeObserver(Observer* observer);
protected:
    void notify(const std::string& event);
private:
    std::vector<Observer*> observers;
};

// State Pattern
class State {
public:
    virtual void update(class Particle* particle) = 0;
    virtual void onEnter(class Particle* particle) {}
    virtual void onExit(class Particle* particle) {}
    virtual ~State() = default;
};

// Particle Class as an Observer
class Particle : public Observer {
public:
    Particle();
    ~Particle();

    void update();
    void draw();
    void onNotify(const std::string& event) override;
    void setState(State* newState);

    ofVec2f position;
    ofVec2f velocity;
    float size;
    ofColor color;

private:
    State* state;
};

// Concrete States
class NormalState : public State {
public:
    void update(Particle* particle) override;
    void onEnter(Particle* particle) override;
};

class AttractState : public State {
public:
    void update(Particle* particle) override;
};

class RepelState : public State {
public:
    void update(Particle* particle) override;
};

class StopState : public State {
public:
    void update(Particle* particle) override;
};

// Particle Factory
class ParticleFactory {
public:
    static Particle* createParticle(const std::string& type);
};

// ofApp: Subject
class ofApp : public ofBaseApp, public Subject {
public:
    void setup();
    void update();
    void draw();
    void keyPressed(int key);

private:
    std::vector<Particle*> particles;
};

```

Ofapp.cpp

``` c++
#include "ofApp.h"

// Observer Pattern Implementation
void Subject::addObserver(Observer* observer) {
    observers.push_back(observer);
}

void Subject::removeObserver(Observer* observer) {
    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string& event) {
    for (Observer* observer : observers) {
        observer->onNotify(event);
    }
}

// Particle Class Implementation
Particle::Particle() {
    position = ofVec2f(ofRandomWidth(), ofRandomHeight());
    velocity = ofVec2f(ofRandom(-1.0f, 1.0f), ofRandom(-1.0f, 1.0f));
    size = ofRandom(5, 15);
    color = ofColor(255);
    state = new NormalState();  // Initial state
}

Particle::~Particle() {
    delete state;
}

void Particle::setState(State* newState) {
    if (state != nullptr) {
        state->onExit(this);
        delete state;
    }
    state = newState;
    if (state != nullptr) {
        state->onEnter(this);
    }
}

void Particle::update() {
    if (state != nullptr) {
        state->update(this);
    }

    // Prevent particles from going off-screen
    if (position.x < 0 || position.x > ofGetWidth()) velocity.x *= -1;
    if (position.y < 0 || position.y > ofGetHeight()) velocity.y *= -1;
}

void Particle::draw() {
    ofSetColor(color);
    ofDrawCircle(position, size);
}

void Particle::onNotify(const std::string& event) {
    if (event == "attract") {
        setState(new AttractState());
    }
    else if (event == "repel") {
        setState(new RepelState());
    }
    else if (event == "stop") {
        setState(new StopState());
    }
    else if (event == "normal") {
        setState(new NormalState());
    }
}

// Concrete States Implementation
void NormalState::update(Particle* particle) {
    particle->position += particle->velocity;
}

void NormalState::onEnter(Particle* particle) {
    particle->velocity = ofVec2f(ofRandom(-1.0f, 1.0f), ofRandom(-1.0f, 1.0f));
}

void AttractState::update(Particle* particle) {
    ofVec2f mousePos(((ofApp*)ofGetAppPtr())->mouseX, ((ofApp*)ofGetAppPtr())->mouseY);
    ofVec2f direction = mousePos - particle->position;
    direction.normalize();
    particle->velocity += direction * 0.1;
    particle->position += particle->velocity;
}

void RepelState::update(Particle* particle) {
    ofVec2f mousePos(((ofApp*)ofGetAppPtr())->mouseX, ((ofApp*)ofGetAppPtr())->mouseY);
    ofVec2f direction = particle->position - mousePos;
    direction.normalize();
    particle->velocity += direction * 0.1;
    particle->position += particle->velocity;
}

void StopState::update(Particle* particle) {
    particle->velocity = ofVec2f(0, 0);
}

// Particle Factory Implementation
Particle* ParticleFactory::createParticle(const std::string& type) {
    Particle* particle = new Particle();

    if (type == "star") {
        particle->size = ofRandom(5, 10);
        particle->color = ofColor(255, 255, 0);  // Yellow
    }
    else if (type == "comet") {
        particle->size = ofRandom(10, 15);
        particle->color = ofColor(255, 0, 0);  // Red
        particle->velocity *= 2;
    }
    else if (type == "planet") {
        particle->size = ofRandom(12, 18);
        particle->color = ofColor(0, 0, 255);  // Blue
    }

    return particle;
}

// ofApp Implementation
void ofApp::setup() {
    ofBackground(0);
    // Create particles using the factory
    for (int i = 0; i < 10; ++i) {
        Particle* p = ParticleFactory::createParticle("star");
        particles.push_back(p);
        addObserver(p);
    }

    for (int i = 0; i < 5; ++i) {
        Particle* p = ParticleFactory::createParticle("comet");
        particles.push_back(p);
        addObserver(p);
    }

    for (int i = 0; i < 10; ++i) {
        Particle* p = ParticleFactory::createParticle("planet");
        particles.push_back(p);
        addObserver(p);
    }
}

void ofApp::update() {
    for (Particle* p : particles) {
        p->update();
    }
}

void ofApp::draw() {
    for (Particle* p : particles) {
        p->draw();
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'a') {
        notify("attract");
    }
    else if (key == 'r') {
        notify("repel");
    }
    else if (key == 's') {
        notify("stop");
    }
    else if (key == 'n') {
        notify("normal");
    }
}

```
