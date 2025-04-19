### Mi solucion a la actividad 3

Archivo: ofApp.h
``` c++
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();
    
    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};

// Constructor: inicializa punteros y tamaño
BrushQueue::BrushQueue(int _maxSize)
    : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor: libera la memoria de los nodos
BrushQueue::~BrushQueue() {
    clear();
}

// Agrega un nuevo nodo al final de la cola. Si se supera el límite, elimina el nodo más antiguo.
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    Node* newNode = new Node(x, y, radius, color, opacity);
    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
    size++;

    if (size > maxSize) {
        dequeue();
    }
}

// Elimina el nodo más antiguo de la cola (FIFO)
void BrushQueue::dequeue() {
    if (!isEmpty()) {
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;
        if (isEmpty()) {
            rear = nullptr;
        }
    }
}

// Elimina todos los nodos de la cola
void BrushQueue::clear() {
    while (!isEmpty()) {
        dequeue();
    }
}

// Retorna true si la cola está vacía
bool BrushQueue::isEmpty() {
    return (front == nullptr);
}

class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    // Constructor: inicializa la cola con un tamaño máximo de 50
    ofApp() : strokes(50) {}

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};

``` 
Archivo: ofApp.cpp
``` c++
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    // Si el mouse está presionado, agrega un nuevo trazo
    if (ofGetMousePressed()) {
        float x = ofGetMouseX();
        float y = ofGetMouseY();
        float radius = 10;  // Radio fijo (se puede modificar)
        // Genera un color aleatorio usando HSB
        ofColor color = ofColor::fromHsb(ofRandom(255), 255, 255);
        float opacity = 255;  // Opacidad inicial completa
        strokes.enqueue(x, y, radius, color, opacity);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Fondo con gradiente dinámico basado en backgroundHue
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // Dibuja los trazos almacenados en la cola
    Node* current = strokes.front;
    int index = 0;
    while (current != nullptr) {
        // Ajusta la opacidad para crear un efecto de desvanecimiento:
        // Los nodos más antiguos (con índice 0) tendrán menor opacidad.
        float newOpacity = ofMap(index, 0, strokes.size - 1, 50, 255, true);
        current->opacity = newOpacity;
        ofSetColor(current->color, current->opacity);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        index++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        // Limpia la cola de trazos
        strokes.clear();
    }
    if (key == 'a') {
        // Alterna entre cola de tamaño 50 y 100
        if (strokes.maxSize == 50) {
            strokes.maxSize = 100;
        } else {
            strokes.maxSize = 50;
            // Si existen más nodos que el nuevo límite, elimina los excedentes
            while (strokes.size > strokes.maxSize) {
                strokes.dequeue();
            }
        }
    }
    else if (key == 's') {
        // Guarda la imagen actual en un archivo
        ofSaveScreen("screenshot.png");
    }
}
``` 
- Resumen de la Implementación
BrushQueue:

enqueue(): Crea un nodo nuevo, lo agrega al final y, si se excede el tamaño máximo, elimina el nodo más antiguo (FIFO).

dequeue(): Elimina el nodo en la cabeza de la cola y libera su memoria.

clear(): Recorre y elimina todos los nodos.

isEmpty(): Retorna true si la cola está vacía.

ofApp

update(): Cada vez que el mouse está presionado, se agrega un nuevo trazo con parámetros aleatorios para el color. Además, se actualiza el fondo de forma dinámica.

draw(): Recorre la cola de trazos y dibuja círculos en pantalla. Se usa ofMap para ajustar la opacidad de cada trazo, generando el efecto de desvanecimiento.

keyPressed():

'c' limpia la cola.

'a' alterna el tamaño máximo entre 50 y 100 (y elimina nodos excedentes si es necesario).

's' guarda una captura de pantalla.

- Depuración y Pruebas
Depuración en Visual Studio:

Se colocaron puntos de interrupción en los métodos enqueue(), dequeue() y clear() para inspeccionar los punteros front y rear y el valor de size en cada operación.

Se verificó que, al llegar a un número mayor de nodos que maxSize, dequeue() eliminara el nodo más antiguo y que no existieran fugas de memoria.

Lista de Pruebas:

Prueba de Inserción:

Acción: Mover el mouse para agregar trazos.

Resultado esperado: Cada movimiento agrega un nodo y se dibuja un círculo con color aleatorio.

Resultado obtenido: Se observó la aparición de trazos en pantalla, cumpliendo la función.

Prueba FIFO:

Acción: Continuar agregando trazos hasta superar el límite (maxSize).

Resultado esperado: Los trazos más antiguos se eliminan conforme se agregan nuevos.

Resultado obtenido: Se verifica que la cola mantiene el tamaño definido y se elimina el primer nodo al exceder el límite.

Prueba de Vaciado:

Acción: Presionar 'c'.

Resultado esperado: Se limpia la pantalla y la cola queda vacía.

Resultado obtenido: La cola se vació correctamente.

Prueba de Alternancia de Tamaño:

Acción: Presionar 'a' para alternar entre 50 y 100 trazos.

Resultado esperado: La cola cambia el límite de nodos; al disminuir, se eliminan los excedentes.

Resultado obtenido: El límite se alterna correctamente y la cola se ajusta según el nuevo tamaño.
