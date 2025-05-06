### Mi solucion a la actividad 4

-  ¿Dónde estás aplicando el concepto de encapsulamiento?
Encapsulamiento significa proteger los datos internos de una clase y acceder a ellos solo a través de métodos públicos. En mi código, todas las variables internas de las partículas están declaradas como protected o private, y su acceso/control se hace a través de métodos public:

```
class RisingParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float lifetime;
    float age;
    bool exploded;
public:
    void update(float dt) override;
    void draw() override;
    bool isDead() const override;
    bool shouldExplode() const override;
    glm::vec2 getPosition() const override;
    ofColor getColor() const override;
};
```
Aquí se encapsulan position, velocity, color, etc., y se accede a través de métodos como getPosition() o shouldExplode().

- ¿Dónde estás aplicando el concepto de herencia?
Herencia permite que una clase derive de otra. En el código, la clase Particle es una clase base abstracta, y otras clases como RisingParticle, ZigZagParticle, y ExplosionParticle heredan de ella:

```
class Particle {
public:
    virtual ~Particle() {}
    virtual void update(float dt) = 0;
    virtual void draw() = 0;
    virtual bool isDead() const = 0;
    virtual bool shouldExplode() const { return false; }
    virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
    virtual ofColor getColor() const { return ofColor(255); }
};

class RisingParticle : public Particle { ... };
class ZigZagParticle : public Particle { ... };
class BouncingParticle : public Particle { ... };
class ExplosionParticle : public Particle { ... };
```
Esto permite reutilizar la interfaz común Particle y extenderla según el comportamiento de cada tipo de partícula.

- ¿Dónde estás aplicando el concepto de polimorfismo?
Polimorfismo permite que objetos de diferentes clases se manejen a través de una misma interfaz. Esto lo estoy aplicando al guardar punteros a diferentes tipos de partículas (como RisingParticle, ZigZagParticle, ExplosionParticle) en un vector de Particle*.

Implementación del polimorfismo:

```
class Particle {
    virtual void update(float dt) = 0;
    virtual void draw() = 0;
};
```
Uso del polimorfismo (métodos polimórficos llamados en ofApp.cpp):

```
for (int i = 0; i < particles.size(); i++) {
    particles[i]->update(dt);
    particles[i]->draw();
}
```
Aquí, aunque particles[i] es de tipo Particle*, en tiempo de ejecución se llama el update y draw del tipo real (por ejemplo, ZigZagParticle o StarExplosion). Esto es polimorfismo en tiempo de ejecución gracias a los métodos virtuales.

- ¿Qué es un objeto? ¿Qué es una clase?
Un objeto es una instancia concreta de una clase. Representa una entidad con datos (atributos) y comportamientos (métodos).

Una clase es un plano o plantilla que define cómo serán los objetos. Define qué atributos y métodos tendrán.

Por ejemplo, RisingParticle es una clase, y cada vez que creo una con new RisingParticle(...), estoy creando un objeto de esa clase.

- ¿Cómo se ve en memoria un objeto de una clase que hereda de otra clase?
Un objeto de una clase derivada contiene los datos de la clase base primero, seguidos por los propios datos de la clase derivada. Si la clase tiene métodos virtuales, el objeto también contiene un puntero oculto a la tabla de funciones virtuales (vtable).

Por ejemplo:

```
[ vtable pointer ]
[ atributos de Particle ]
[ atributos de RisingParticle ]
```
Esto permite que, usando un puntero a Particle, el programa llame a los métodos correctos definidos en RisingParticle, gracias a la vtable.
