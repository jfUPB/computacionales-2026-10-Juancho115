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



## Bitácora de aplicación 



## Bitácora de reflexión


