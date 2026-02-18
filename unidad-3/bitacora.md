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



## Bitácora de reflexión
