<!-- Operaciones aritméticas básicas
Enunciado: Escribe un programa en ensamblador Hack que realice las siguientes operaciones:

Guarda el valor 5 en el registro A.
Guarda el valor 10 en el registro D.
Suma el contenido del registro A y el registro D, y guarda el resultado en el registro D.
Resta el valor 3 al contenido del registro D y guarda el resultado en la memoria en la dirección 10.
Entrega: el código del programa en ensamblador Hack y una captura de pantalla del simulador mostrando el estado final de los registros y la memoria (para verificar los resultados). -->

### Solución a la actividad 7


``` asm
@5 
D=A 
@10 
D=D+A 
@3 
D=D-A 
@10 
M=D 
@0 
0;JMP
```
![WhatsApp Image 2025-01-30 at 8 22 34 AM](https://github.com/user-attachments/assets/b3d3c5a1-9d2d-44f1-8dba-f4989a20bc55)
