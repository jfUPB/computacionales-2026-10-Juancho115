# Unidad 3

## Bitácora de proceso de aprendizaje
### Actividad 01
- Por referencia 
``` C++
#include <iostream>

using namespace std;


void swapPorValor(int a, int b) {
    int c = b;
    b = a;
    a = c;
    
}


void swapPorReferencia(int& a, int& b) { 
    int c = b;
    b = a;
    a = c;
    
    
}


void swapPorPuntero(int* a, int* b) {

}

int main() {
    int a = 10;
    int b = 30;
    
    swapPorReferencia(a, b);

    cout << "a" << a << endl;
    cout << "b" << b << endl;

    


    return 0;
}
```
- Por Puntero
``` C++
#include <iostream>

using namespace std;


void swapPorValor(int a, int b) {
    int c = b;
    b = a;
    a = c;
    
}


void swapPorReferencia(int& a, int& b) { 
    int c = b;
    b = a;
    a = c;
    
    
}


void swapPorPuntero(int* a, int* b) {
    int c = *b;
     *b = *a;
     *a = c;

}

int main() {
    int a = 10;
    int b = 30;
    
    swapPorPuntero(&a, &b);

    cout << "a" << a << endl;
    cout << "b" << b << endl;

    


    return 0;
}
```

## Bitácora de aplicación 

### Errores
- Podemos observar el primer problema del codigo es que las estadisticas son un puntero y cuando se crea la copia del heroe son las mismas estadisticas, es decir que siempre van a ser compartidas, no independientes por cada personaje 
<img width="707" height="374" alt="Screenshot 2026-02-25 215949" src="https://github.com/user-attachments/assets/c2dbd37c-c098-4b04-ad7e-19bd309f2484" />

- El segundo problema del codigo es cuando se sale del scope de la funcion se destruyen los heroes pero no las estadisticas, entonces las estadisticas siguen ocupando espacio en memoria despues de que los personbajes dejend e existir
<img width="701" height="508" alt="Screenshot 2026-02-25 220625" src="https://github.com/user-attachments/assets/e51d5903-2de8-4e51-a85d-a6d94c1cab98" />

- El primer problema es la posible causa de los crashes aleatorios, porque en al algun momento el progama quiere acceder a las estadisticas que puden haber sido borradas y esto genera un error de segmentación
- El segundo problema seria la causa del memory leak porque nbo se esta liberando la memoria que se uso para las estadisticas cuando la variable del heroe sale de scope.

### Solucion  
-  
```cpp
#include <iostream>
#include <string>
#include <array>

class Personaje {
public:
    std::string nombre;
    std::array<int, 3> estadisticas;

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```
- Aqui podemos ver muestra que las estadisticas son separadas del hereo general y la copia es de cir ya no se compartesn las mismas estadisticas. Esto sacando las estadisticas del Heap y colocandolas en el stack
```cpp
class Personaje {
public:
    std::string nombre;
    std::array<int, 3> estadisticas;
```
<img width="712" height="599" alt="Screenshot 2026-02-25 222146" src="https://github.com/user-attachments/assets/ac6f7087-bea3-4406-84cd-4259044bd6fe" />

- Aqui se muestra que cuando se sale del scope las estadisiticas stambien desaparecen junto con el personaje.
<img width="709" height="451" alt="Screenshot 2026-02-25 222217" src="https://github.com/user-attachments/assets/25d04e04-8e6d-4224-b8a5-3e9dd52517de" />




## Bitácora de reflexión
### 01
- El heap seria una cocina y el stack son lugares de memoria que cada uno tiene una funcion independeiente, el heap es para cuando algo en la memoria se quiere que se pueda usar en cualquier lado y el stack es algo de mas corto uso, que se crea y se destruye al rato.
### 02
- Por 'valor' se genera una copia independiente de lo que se esté llamando y lo que ocurre en el la memoria seria:
```
(Original)          (Copia)
------------        ----------------
a = 5      --->     x = 5 (copia)
```
Asi si se modifica cualquiera de las 2 independientemente

- Por 'referencia' es como si se pudiera modificar desde cualquier lado lo que se esta llamando lo que pasa en memoria es:
```
b = 5
x ----> referencia a b
```
- Por 'puntero' pasa la dirección de memoria y apunta a lo que haya ahí, lo que pasa en memoria es:
```
a = 5
x = dirección de a
```
### 3
- Variable local es la que se pone en el stack y solo existe en una función si se sale de ahi se destruye 
- Variable global es la que está accesible en cualquier momento del programa, se puede llamar donde sea y siempre está 'viva' en el programa encuentra en el heap
- variable local estatica  es una combinación entre global y local siempre esta 'viva' pero solo se puede encontrar dentro de la función
### 4
