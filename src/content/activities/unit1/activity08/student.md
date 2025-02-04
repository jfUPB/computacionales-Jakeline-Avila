<!-- Control de flujo con saltos
Enunciado: escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. 
Si el valor en la dirección 5 es menor que 10, guarda el valor 1 en la dirección 7. Si el valor en la dirección 5 es mayor o igual a 10, guarda el valor 0 en la dirección 7.

Entrega: El código del programa y una captura de pantalla del simulador mostrando el resultado en la dirección 7
para dos casos: cuando el valor en la dirección 5 es menor que 10 y cuando es mayor o igual a 10. -->

### Mi solución a la actividad 8

``` js
@5 
D=M 
@10 
D=D-A 
D;JLT 
@7 
M=1 
@15 
0;JMP 
@7 
M=0
```
![WhatsApp Image 2025-02-04 at 8 30 41 AM (1)](https://github.com/user-attachments/assets/5f82d443-cd75-420e-8eb1-9509defa316c)
![WhatsApp Image 2025-02-04 at 8 30 41 AM](https://github.com/user-attachments/assets/5aa26fdb-7925-4ff9-8c29-c44157adf7f3)
