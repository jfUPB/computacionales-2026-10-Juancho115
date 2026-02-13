# Unidad 2

## Bitácora de proceso de aprendizaje
### Actividad 01
<img width="1489" height="287" alt="image" src="https://github.com/user-attachments/assets/f88f35e5-dddf-492d-9f24-9af1a439f096" />

### Actividad 02
<img width="1492" height="237" alt="image" src="https://github.com/user-attachments/assets/1586070c-e936-4da6-b29b-177de691d8c8" />

### Actividad 03
```
(start)
// i es igual a screen 
@SCREEN
D=A
@i
M=D
// Inicio la pantalla pintando una linea
@SCREEN
M=-1

(LOOP)
@KBD
D=M
@100
D=D-A
@derecha
D;JEQ

@KBD
D=M
@105
D=D-A
@izquierda
D;JEQ
@LOOP
0;JMP



@LOOP
0;JMP

(derecha)
@i
A=M
M=0
A=A+1
M=-1
D=A
@i
M=D
@LOOP
0;JMP

(izquierda)
@i
A=M
M=0
A=A-1
M=-1
D=A
@i
M=D
@LOOP
0;JMP

@fin
(fin)
0;JMP
```

### Actividad 05
- <img width="1062" height="486" alt="image" src="https://github.com/user-attachments/assets/8fcbeae3-6c3a-48b4-8e79-3c52945b62bf" />

- <img width="763" height="558" alt="image" src="https://github.com/user-attachments/assets/c476d3fa-b907-43a3-b8b6-71f1a262b404" />

### Actividad 06

```

@1
D=A
@16
M=D

@20
D=A
@17
M=D

@13
D=A
@18
M=D

@24
D=A
@19
M=D

@55
D=A
@20
M=D

@96
D=A
@21
M=D

@87
D=A
@22
M=D

@83
D=A
@23
M=D

@98
D=A
@24
M=D

@102
D=A
@25
M=D

@R0
M=0


@16
D=A
@R1
M=D


@10
D=A
@R2
M=D


(LOOP)

@R2
D=M
@END
D;JEQ

// D = puntero
@R1
A=M
D=M

// sum =puntero
@R0
M=D+M

// punterto
@R1
M=M+1

// count--
@R2
M=M-1

@LOOP
0;JMP

(END)
@END
0;JMP
```
 - <img width="1548" height="801" alt="image" src="https://github.com/user-attachments/assets/58a2e024-2129-43ab-9fb7-3e7e04441dae" />

 - <img width="1541" height="799" alt="image" src="https://github.com/user-attachments/assets/3c5e4af6-0cbb-42d8-8cfe-f38cb5605945" />

 - <img width="1546" height="796" alt="image" src="https://github.com/user-attachments/assets/8cf2cf6f-2154-491c-88f5-8d2b20106af9" />
 
 - <img width="1548" height="762" alt="image" src="https://github.com/user-attachments/assets/ab8f773a-7fda-452b-929b-368a8af653e0" />

 ### Actividad 07 


### Actividad 08
- a
```
@10
D=A
@a
M=D


@20
D=A
@b
M=D


@a
D=A
@R0
M=D

@b
D=A
@R1
M=D

@RET_SWAP
D=A
@R15
M=D


@swap
0;JMP

(RET_SWAP)


(END)
@END
0;JMP



(swap)


    @R0
    A=M
    D=M
    @tmp
    M=D


    @R1
    A=M
    D=M
    @R0
    A=M
    M=D


    @tmp
    D=M
    @R1
    A=M
    M=D


    @R15
    A=M
    0;JMP
```
- Hasta el momento se guardaron los valores de a y b respectivamente en "RAM 16" y "RAM 17"
  <img width="1547" height="726" alt="image" src="https://github.com/user-attachments/assets/b888083e-e3cd-4f70-b616-85646f1be8a0" />

- Aqui se está apuntando a la dirección RAM 16
  <img width="1546" height="647" alt="image" src="https://github.com/user-attachments/assets/187e0ced-d030-46fe-971b-42c917ab577a" />

- Aqui se salta al Swap
  <img width="1545" height="733" alt="image" src="https://github.com/user-attachments/assets/4a5c9a10-2cd8-4f58-900b-b57340a12cb0" />

- Ahora el valor de b está en a RAM 16
  <img width="1546" height="723" alt="image" src="https://github.com/user-attachments/assets/9498e687-e5d9-424e-94d9-8770d5f6da2c" />

- Ahora el valor de a está en b RAM 17
  <img width="1543" height="714" alt="image" src="https://github.com/user-attachments/assets/e941c7ca-772e-4991-8acb-96c1afaf14d0" />

- Salta a un Loop para acabar el programa
  <img width="1549" height="723" alt="image" src="https://github.com/user-attachments/assets/0c5be766-ea20-4eb6-b37d-5fc0223d3018" />





- b
```
@10
D=A
@arr
M=D

@15
D=A
@arr1
M=D

@2
D=A
@arr2
M=D

@3
D=A
@arr3
M=D

@50
D=A
@arr4
M=D

@arr
D=A
@R0
M=D

@5
D=A
@R1
M=D

@RET_SUM
D=A
@R15
M=D

@calSum
0;JMP

(RET_SUM)


(END)
@END
0;JMP


    @sum
    M=0

    @i
    M=0

(LOOP)

    @i
    D=M
    @R1
    D=D-M
    @END_LOOP
    D;JGE

    @R0
    D=M

    @i
    A=D+M

    D=M       

    @sum
    M=D+M

    @i
    M=M+1

    @LOOP
    0;JMP

(END_LOOP)

    @sum
    D=M
    @R0
    M=D

    @R15
    A=M
    0;JMP
```

- Aqui se guardan los datos de los Array del 1-5
  <img width="1544" height="759" alt="image" src="https://github.com/user-attachments/assets/31f67fe3-bde1-4f17-80df-a54628954bc3" />

- Aqui se guarda el tamaño del array
  <img width="1546" height="766" alt="image" src="https://github.com/user-attachments/assets/1f7d9c95-7a6f-4ad3-ba87-9807624ec151" />

- Aqui se videnci el resultado final del problema la suma de 80
   <img width="1547" height="756" alt="image" src="https://github.com/user-attachments/assets/ef0548ac-fe22-4a45-a0e8-852faebcd813" />



## Bitácora de aplicación 
### Actividad 09 

```
(START)
    @LOOP
    0;JMP

(LOOP)

    @KBD
    D=M

    @LOOP
    D;JEQ // si no hay tecla, se continua a la siguiente iteracion del loop

    @key
    M=D

    // comparar con 'd'
    @100
    D=A
    @key
    D=M-D
    @DRAW_CALL
    D;JEQ

    // comparar con 'e'
    @101
    D=A
    @key
    D=M-D
    @ERASE
    D;JEQ

    @LOOP
    0;JMP



// ============================================
// LLAMAR FUNCIÓN draw
// ============================================

(DRAW_CALL)

    // desplazamiento = 0
    @0
    D=A
    @R0
    M=D

    // guardar dirección retorno en R15
    @RET_DRAW
    D=A
    @R15
    M=D

    @draw
    0;JMP

(RET_DRAW)

(WAIT_RELEASE_D)
    @KBD
    D=M
    @WAIT_RELEASE_D
    D;JNE

    @LOOP
    0;JMP



// ============================================
// BORRAR PANTALLA
// ============================================

(ERASE)

    @SCREEN
    D=A
    @addr
    M=D

(CLEAR_LOOP)

    @addr
    A=M
    M=0

    @addr
    M=M+1

    @24576
    D=A
    @addr
    D=M-D
    @END_CLEAR
    D;JEQ

    @CLEAR_LOOP
    0;JMP

(END_CLEAR)

(WAIT_RELEASE_E)
    @KBD
    D=M
    @WAIT_RELEASE_E
    D;JNE

    @LOOP
    0;JMP

(draw)
	@SCREEN
	D=A
	@R0
	AD=D+M
	// row 1
	@8
	D=D+A
	A=D-A
	M=D-A
	// row 2
	D=A
	@32
	AD=D+A
	@20
	D=D+A
	A=D-A
	M=D-A
	// row 3
	D=A
	@32
	AD=D+A
	@34
	D=D+A
	A=D-A
	M=D-A
	// row 4
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 5
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 6
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 7
	D=A
	@32
	AD=D+A
	@83
	D=D+A
	A=D-A
	M=D-A
	// row 8
	D=A
	@32
	AD=D+A
	@101
	D=D+A
	A=D-A
	M=D-A
	// row 9
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 10
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 11
	D=A
	@32
	AD=D+A
	@73
	D=D+A
	A=D-A
	M=D-A
	// row 12
	D=A
	@32
	AD=D+A
	@34
	D=D+A
	A=D-A
	M=D-A
	// row 13
	D=A
	@32
	AD=D+A
	@20
	D=D+A
	A=D-A
	M=D-A
	// row 14
	D=A
	@32
	AD=D+A
	@8
	D=D+A
	A=D-A
	M=D-A

	// return
	@R15
	A=M
	D;JMP
 ```
<img width="420" height="588" alt="image" src="https://github.com/user-attachments/assets/8b12a364-884d-4619-8b15-1edc34bea406" />

<img width="1541" height="215" alt="image" src="https://github.com/user-attachments/assets/b816a1dd-fb3f-485d-b3ae-d1b6f1aabc31" />




## Bitácora de reflexión




