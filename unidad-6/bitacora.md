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
```C++
for (int i = 0; i < 8; ++i) {
    Particle * p = ParticleFactory::createParticle("comet");
    particles.push_back(p); addObserver(p);
}
```
### Keypressed
```C++
case 'o': notify("orbit"); break;
```

# Breakpoints 
## 1.
- Comet
<img width="1455" height="474" alt="image" src="https://github.com/user-attachments/assets/e1d31931-c3d1-4dc5-841d-f83e6e6eabc1" />

- En el depurador se observa que el parámetro type tiene el valor "comet", lo que hace que se ejecute la rama correspondiente del condicional. El objeto particle ya está instanciado en memoria y sus atributos han sido modificados: el tamaño está dentro del rango definido, el color es amarillo (255,255,0) y la velocidad es mayor debido a la multiplicación aplicada.

## 2.
- normal state 
<img width="1501" height="553" alt="image" src="https://github.com/user-attachments/assets/6d680e6b-1a07-4ad6-b59c-5c0fb8ba2a08" />

En el depurador se observa que el flujo del programa entra en NormalState::update. El puntero this indica que el método ejecutado pertenece a la clase NormalState, lo que significa que el estado actual de la partícula es de ese tipo.

-Orbit state
<img width="1460" height="425" alt="image" src="https://github.com/user-attachments/assets/2016511f-1bd0-40a7-87a5-c38e75d32936" />

- Coloqué breakpoints en NormalState::update y OrbitState::update para observar qué implementación del método update se ejecuta dependiendo del estado activo de la partícula.


- En el depurador se observa que inicialmente el flujo entra en NormalState::update, lo que indica que la partícula está en estado normal. Luego, al presionar la tecla correspondiente, el flujo cambia y se ejecuta OrbitState::update. Además, el puntero this muestra que el método ejecutado pertenece a diferentes clases en cada caso.


## 3. 
- tecla o 
<img width="1492" height="462" alt="image" src="https://github.com/user-attachments/assets/bcfa049f-2e67-4716-944d-5c9cd58ba5f0" />

En el depurador se observa que al presionar la tecla 'o', se ejecuta el método keyPressed, donde se llama a notify("orbit"). Además, se puede ver que el objeto tiene un vector de observadores con múltiples partículas registradas.

- OnNotify


<img width="1485" height="533" alt="image" src="https://github.com/user-attachments/assets/c8c47ba0-7175-41c3-a9ac-76883053cf6d" />


- En el depurador se observa que una partícula recibe el evento "orbit" en el método onNotify. El objeto this corresponde a una instancia válida de Particle, y al cumplirse la condición del evento, se ejecuta setState(new OrbitState()), iniciando el cambio de estado.


- <img width="1549" height="575" alt="image" src="https://github.com/user-attachments/assets/ffc6164a-4a2c-4016-8f56-3a2bf5f4a1d1" />

- En el depurador se observa que el puntero state de la partícula es reemplazado por newState, que corresponde a una instancia de OrbitState. Antes de la asignación, el estado anterior es eliminado, y posteriormente se asigna el nuevo estado, lo que modifica el comportamiento de la partícula.

## 4.

<img width="1532" height="463" alt="image" src="https://github.com/user-attachments/assets/bbced096-6dbe-4e50-bcfa-32ac4fe4de25" />

En el depurador se observa que, al ejecutarse setState, el puntero state anterior es eliminado y se asigna un nuevo objeto newState, correspondiente a OrbitState. Este nuevo objeto tiene su propia dirección de memoria, lo que indica que es una instancia independiente.



  





## Bitácora de reflexión

