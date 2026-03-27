# Unidad 5
## Bitácora de proceso de aprendizaje
```C#
using System;
using System.Collections.Generic;

public abstract class Figura
{
    private string nombre;

    public string Nombre
    {
        get { return nombre; }
        protected set { nombre = value; }
    }

    public Figura(string nombre)
    {
        this.Nombre = nombre;
    }

    public abstract void Dibujar();
}

public class Circulo : Figura
{
    public double Radio { get; private set; }

    public Circulo(double radio) : base("Círculo")
    {
        this.Radio = radio;
    }

    public override void Dibujar()
    {
        Console.WriteLine($"Dibujando un {Nombre} de radio {Radio}.");
    }
}

public class Rectangulo : Figura
{
    public double Base { get; private set; }
    public double Altura { get; private set; }

    public Rectangulo(double b, double h) : base("Rectángulo")
    {
        this.Base = b;
        this.Altura = h;
    }

    public override void Dibujar()
    {
        Console.WriteLine($"Dibujando un {Nombre} de {Base}x{Altura}.");
    }
}

public class Programa
{
    public static void Main()
    {
        List<Figura> misFiguras = new List<Figura>();

        misFiguras.Add(new Circulo(5.0));
        misFiguras.Add(new Rectangulo(4.0, 6.0));
        misFiguras.Add(new Circulo(10.0));

        foreach (Figura fig in misFiguras)
        {
            fig.Dibujar();
        }
    }
}
```

## Bitácora de aplicación 

### Fase 2

#### Evidencia 1

Se eligió la siguiente linea para el breakpoint:

<img width="540" height="137" alt="image" src="https://github.com/user-attachments/assets/3fdc85f6-c829-4f64-b1be-89445931f351" />

Por que en esta linea se itera sobre todas las particulas que existen, asi que eventualmente es posible ver cada uno de los tipos de particulas posibles

<img width="1241" height="303" alt="image" src="https://github.com/user-attachments/assets/abe5b5c1-0119-4d75-8263-8e70a96af01c" />

El depurador muestra que la variable `particles[i]` contiene el objeto `SpiralParticle` y como este hereda de `RisingParticle` y de `Particle`

#### Evidencia 2

Usando el mismo breakpoint de la evidencia anterior.

La `_vtable` de `SpiralParticle`:
<img width="1244" height="229" alt="image" src="https://github.com/user-attachments/assets/078c9b3c-2a7f-4ac3-ad6d-63f5ba2180b0" />

La `_vtable` de `RisingParticle`:
<img width="1250" height="232" alt="image" src="https://github.com/user-attachments/assets/9ae3acbf-dcc9-464b-9c47-7f9ec490e278" />

Se puede evidenciar que la diferencia de `_vtable` entre ambas son los métodos `draw` y `update`, y el deconstructor, el resto de métodos son iguales porque `SpiralParticle` los hereda de `RisingParticle`.

#### Evidencia 3

El breakpoint se ubico en la siguiente linea:

<img width="686" height="103" alt="image" src="https://github.com/user-attachments/assets/39cb95c7-676d-4de8-9d52-5bf79957977c" />

Ya que cada tipo de particula implementa su version del metodo `draw`, visible en el indice 2 del `_vtable`.

<img width="1873" height="139" alt="image" src="https://github.com/user-attachments/assets/af7cc955-4816-40bc-aed9-90ac4e460f66" />

<img width="1518" height="142" alt="image" src="https://github.com/user-attachments/assets/0d08e0f5-6a0e-4645-ade7-900fbe029d1c" />

Para un `SpiralParticle` el metodo `draw` es diferente que el de un `RisingParticle`.

#### Evidencia 4

Reutilizando el mismo breakpoint de la evidencia anterior

<img width="1919" height="274" alt="image" src="https://github.com/user-attachments/assets/948db8fe-1c5c-491f-a869-cd89678ce9bb" />

En el debugger se puede evidenciar que los atributos privados estan indicados con un candado como se muestra en el `ZigZagParticle`, a diferencia de los otros atributos como se ve en en los atributos heredados del `RisingParticle`, ademas los atributos protegidos de RisingParticle son accesibles desde la subclase, mientras que los privados no lo serían, lo que refleja el principio de encapsulamiento.


## Bitácora de reflexión
