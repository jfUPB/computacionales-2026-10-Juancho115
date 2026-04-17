# Unidad 6

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

`OfApp.h`
### Nuevo State
```C++
class OrbitState : public State {
public:
    void update(Particle * particle) override;
};
```
`OfApp.cpp`
### Estado nuevo 
```C++
void OrbitState::update(Particle * particle) {
    ofVec2f center(ofGetMouseX(), ofGetMouseY());
    ofVec2f dir = particle->position - center;

    float angle = atan2(dir.y, dir.x);
    angle += 0.05f;

    float radius = dir.length();

    particle->position.x = center.x + cos(angle) * radius;
    particle->position.y = center.y + sin(angle) * radius;
}
```
### Notify
```C++
else if (event == "orbit") {
    setState(new OrbitState());
}
```
### Particle Factory
```C++
else if (type == "comet") {
    particle->size = ofRandom(4.0f, 7.0f);
    particle->color = ofColor(255, 255, 0);
    particle->velocity *= 4.0f;
}
```
### Particle Setup
for (int i = 0; i < 8; ++i) {
    Particle * p = ParticleFactory::createParticle("comet");
    particles.push_back(p); addObserver(p);
}
### Keypressed
```C++
case 'o': notify("orbit"); break;
```

# Breakpoints 

<img width="938" height="641" alt="image" src="https://github.com/user-attachments/assets/dbc65b9f-2ad2-4286-b88e-c2c596d842d2" />






## Bitácora de reflexión

