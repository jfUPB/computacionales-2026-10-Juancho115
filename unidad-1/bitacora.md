# Unidad 1

## Bitácora de proceso de aprendizaje
### Actividad 01
- En lo que observo es que es un programa que usa bastante la logica a pesar de ser algo que realiza paso a paso es muy facil poder perderte en el proceso si no se está atento
- LA diferencia de datos entre la ROM y la RAM esta en que en la Rom se encuentra lo que se va a ejecutar y en la RAm se guardan los datos especificos por parte de la ROM y la CPU

### Actividad 02
- La ALU se utiliza en donde haya cualquier operación aritmetica
- El PC (program counter) es el que indica la posicion del procesador dentro del programa
- La diferencia entre "@i" y "@READKEYBOARD" es que una es una variable creada por el usuario y la otra una dirección del propio programa
- Para mostrar información en la pantalla
- El bucle en la primera parte funciona porque pide comparar un numero que al final tiene la instruccíon hacer jump en caso de que el numero no sea igual a 0 y como el valor nunca cambia, por eso se mantiene en bucle
- Es cuando funciona como un if 

## Bitácora de aplicación 
### Actividad 04 
-
```
@12
M=0

@13
M=1

(LOOP)
@13
D=M
@5
D=D-A
@END
D;JGT

@13
D=M
@12
M=M+D

@13
M=M+1

@LOOP
0;JMP

(END)
@END
0;JMP
```

<img width="1553" height="901" alt="Captura de pantalla 2026-01-29 202135" src="https://github.com/user-attachments/assets/959305e2-55da-4d25-88ec-5d8eccfd284d" />

## Bitácora de reflexión
### Actividad 05
- Fetch: trae las instrucciones de la memoria
  Decode: es la operacion de las instrucciones de la memoria
  Execute: es la ejecucuion de las instrucciones anterirores
  PC: es quien indica la direccion de la instrucción
- Registro A: funciona como para dar un valor inmediato por ejemplo @14 etc (me falta)

- Registro D: Es un registro para almacenar datos
  Registro A: Es un registro que indica la dirección de donde se quiere hacer algo.
  ALU: Es Arithmetic Logic Unit que se encarga de todo lo que tenga que ver con operaciones

-  con una etiqueta de salto ejemplo: D;JGT
-  Un Loop se implementa por medio de operaciones y con ayudas de los tag (Loop) y condiciones de JMP 
```
@0
M=O
(LOOP)
@0
M=M+1
@LOOP
0;JMP
```
- M=D: es que se almacene el valor de D en la RAM  .
  D=M: el valor almacenado en la RAM lo registra la D

- Ir a la dirección de KBD y leer lo que haya en la RAM


