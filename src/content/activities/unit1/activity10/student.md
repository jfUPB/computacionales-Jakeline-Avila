<!-- Dibujando un punto en la pantalla
Enunciado: la pantalla del computador Hack se controla a través de un mapa de memoria que comienza en la dirección 16384 (SCREEN). 
Cada bit en este mapa de memoria representa un pixel en la pantalla (1 = negro, 0 = blanco). Escribe un programa que dibuje un punto negro en la esquina superior izquierda de la pantalla. 
(Recuerda que la esquina superior izquierda corresponde al primer bit del primer word en la dirección SCREEN).

Entrega: el código del programa y una captura de pantalla del simulador mostrando el punto negro en la esquina superior izquierda de la pantalla. -->

### Mi solución a la actividad 10:

``` js
@16384 
M=1 
@0 
0;JMP
```
![image](https://github.com/user-attachments/assets/dbe160c8-2a9b-4edd-8398-035a72890f57)
