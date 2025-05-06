### Mi solucion a la actividad 3
``` c#
// ofApp.h
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
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

// -------------------------------------------------
// RisingParticle
// -------------------------------------------------
class RisingParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float lifetime;
    float age;
    bool exploded;
public:
    RisingParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life)
        : position(pos), velocity(vel), color(col), lifetime(life), age(0), exploded(false) {}

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        velocity.y += 9.8f * dt * 8;
        float explosionThreshold = ofGetHeight() * 0.15 + ofRandom(-30, 30);
        if (position.y <= explosionThreshold || age >= lifetime) exploded = true;
    }

    void draw() override { ofSetColor(color); ofDrawCircle(position, 10); }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// ZigZagParticle
// -------------------------------------------------
class ZigZagParticle : public Particle {
    glm::vec2 position, velocity;
    ofColor color;
    float age, lifetime;
    bool exploded;
public:
    ZigZagParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life)
        : position(pos), velocity(vel), color(col), age(0), lifetime(life), exploded(false) {}

    void update(float dt) override {
        age += dt;
        velocity.y += 9.8f * dt * 5;
        position += velocity * dt;
        position.x += sin(age * 10) * 10;
        if (age >= lifetime || position.y < ofGetHeight() * 0.15) exploded = true;
    }

    void draw() override { ofSetColor(color); ofDrawCircle(position, 8); }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// BouncingParticle
// -------------------------------------------------
class BouncingParticle : public Particle {
    glm::vec2 position, velocity;
    ofColor color;
    float age, lifetime;
    int bounces;
    bool exploded;
public:
    BouncingParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life)
        : position(pos), velocity(vel), color(col), age(0), lifetime(life), bounces(0), exploded(false) {}

    void update(float dt) override {
        age += dt;
        velocity.y += 9.8f * dt * 5;
        position += velocity * dt;
        if (position.y >= ofGetHeight()) {
            if (bounces < 2) { velocity.y *= -0.7; bounces++; }
            else exploded = true;
        }
        if (age >= lifetime) exploded = true;
    }

    void draw() override { ofSetColor(color); ofDrawCircle(position, 8); }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// ExplosionParticle base
// -------------------------------------------------
class ExplosionParticle : public Particle {
protected:
    glm::vec2 position, velocity;
    ofColor color;
    float age, lifetime, size;
public:
    ExplosionParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life, float sz)
        : position(pos), velocity(vel), color(col), age(0), lifetime(life), size(sz) {}

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        color.a = ofMap(age, 0, lifetime, 255, 0, true);
    }

    bool isDead() const override { return age >= lifetime; }
};

class CircularExplosion : public ExplosionParticle {
public:
    CircularExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(80, 200);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }
    void draw() override { ofSetColor(color); ofDrawCircle(position, size); }
};

class RandomExplosion : public ExplosionParticle {
public:
    RandomExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
        velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
    }
    void draw() override { ofSetColor(color); ofDrawRectangle(position.x, position.y, size, size); }
};

class StarExplosion : public ExplosionParticle {
public:
    StarExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(90, 180);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }
    void draw() override {
        ofSetColor(color);
        int rays = 5;
        float outerRadius = size, innerRadius = size * 0.5;
        ofPushMatrix();
        ofTranslate(position);
        for (int i = 0; i < rays; i++) {
            float theta = ofMap(i, 0, rays, 0, TWO_PI);
            float xOuter = cos(theta) * outerRadius, yOuter = sin(theta) * outerRadius;
            float xInner = cos(theta + PI / rays) * innerRadius, yInner = sin(theta + PI / rays) * innerRadius;
            ofDrawLine(0, 0, xOuter, yOuter);
            ofDrawLine(xOuter, yOuter, xInner, yInner);
        }
        ofPopMatrix();
    }
};

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();
    void mousePressed(int x, int y, int button);
    void keyPressed(int key);
    std::vector<Particle*> particles;
    ~ofApp();
private:
    void createRandomParticle();
};
```
``` c#
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    float dt = ofGetLastFrameTime();

    // Actualiza todas las partículas
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->update(dt);
    }

    // Procesa las partículas (iteración en reversa para facilitar eliminación)
    for (int i = particles.size() - 1; i >= 0; i--) {
        if (particles[i]->shouldExplode()) {
            int explosionType = (int)ofRandom(3); // 0: Circular, 1: Random, 2: Star
            int numParticles = (int)ofRandom(20, 30);
            for (int j = 0; j < numParticles; j++) {
                glm::vec2 pos = particles[i]->getPosition();
                ofColor col = particles[i]->getColor();

                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(pos, col));
                } else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(pos, col));
                } else {
                    particles.push_back(new StarExplosion(pos, col));
                }
            }
            delete particles[i];
            particles.erase(particles.begin() + i);
        } else if (particles[i]->isDead()) {
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    for (auto* p : particles) {
        p->draw();
    }
}

//--------------------------------------------------------------
void ofApp::createRisingParticle() {
    float minX = ofGetWidth() * 0.35;
    float maxX = ofGetWidth() * 0.65;
    float spawnX = ofRandom(minX, maxX);
    glm::vec2 pos(spawnX, ofGetHeight());

    glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
    glm::vec2 direction = glm::normalize(target - pos);
    glm::vec2 vel = direction * ofRandom(250, 350);

    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5);

    int type = (int)ofRandom(3); // 0: Rising, 1: ZigZag, 2: Bouncing
    if (type == 0) {
        particles.push_back(new RisingParticle(pos, vel, col, lifetime));
    } else if (type == 1) {
        particles.push_back(new ZigZagParticle(pos, vel, col, lifetime));
    } else {
        particles.push_back(new BouncingParticle(pos, vel, col, lifetime));
    }
}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
    createRisingParticle();
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == ' ') {
        for (int i = 0; i < 1000; i++) {
            createRisingParticle();
        }
    }
    if (key == 's') {
        ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
    }
}

//--------------------------------------------------------------
ofApp::~ofApp() {
    for (auto* p : particles) {
        delete p;
    }
    particles.clear();
}

```

