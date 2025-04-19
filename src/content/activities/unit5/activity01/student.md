### Mi solución a la actividad 1


![Captura de pantalla 2025-04-10 085132](https://github.com/user-attachments/assets/b10df770-66f3-4c16-bdd8-4bd398a27fd7)


- Primero con el mouse se crea una sola particula que se va actualizando gracias al update, esta tiene un tiempo de vida que cuando ya está mas vieja explota (La explosion usa la misma de CreateRisingParticles que crea más
particulas al terminar la vida de la anterior), lo cual se llama random a un tipo de forma como circulo, rectangulo y estrella.
- Segundo con la barra espaciadora se crean mil particulas que explotan de la misma forma como lo que pasó en el mouse.
- El canvas se crea como siempre, en este nuevo experimento hay un funcion privada que puede ser publica pero solo para experimentación se puso privada y que sea evidencia de los diferentes metodos que hay.
- Las particulas siguen la trayectoria puesta por el vector velocidad.
- En el caso de las estrellas se guarda la forma en una matriz para luego ser rotada pero la forma sigue guardada sin alteraciones en sus puntos.
- La funcion update son llamadas en cada frame.
- Despues de update viene draw.
- Si la particula no deberia explotar se elimina.
- Se guarda con "S" el .png
