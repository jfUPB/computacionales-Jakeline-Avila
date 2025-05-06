### Mi solución a la actividad 1
- Imagen del ejercicio:

![WhatsApp Image 2025-04-01 at 8 40 46 AM](https://github.com/user-attachments/assets/e369e44d-ff9b-47b3-ba86-4caa5b6491ae)

- ¿Cómo se crea la lista enlazada?

R/= La lista enlazada se crea como una instancia de std::list<glm::vec2> en la clase ofApp. 
Esta lista guarda las posiciones de los nodos de la serpiente, donde cada nodo es un objeto de tipo glm::vec2, que tiene las coordenadas x y y.

- ¿Cómo se añaden los primero nodos a la lista?

R/= Los primeros nodos se añaden en el método setup() utilizando el método emplace_back(). Este método agrega un nuevo nodo 
(representado por una posición en el plano, glm::vec2) al final de la lista. Se añaden 20 nodos al principio, todos en la misma posición (en el centro de la pantalla).

- ¿Cómo se añaden nodos adicionales a la lista?

R/=  Los nodos adicionales se añaden a la lista mediante la tecla 'a'. Cuando se presiona esta tecla, se agrega un nodo en una posición aleatoria utilizando nuevamente emplace_back().

- ¿Cómo se eliminan nodos de la lista?

R/= Los nodos se eliminan de la lista con la tecla 'r'. Este código elimina el último nodo de la lista utilizando el método pop_back().

- ¿Cómo se limpia la lista?

R/=  La lista se limpia completamente con la tecla 'c'. El método clear() elimina todos los nodos de la lista.

- ¿Cómo se verifica si la lista está vacía?

R/=  Para verificar si la lista está vacía, se puede usar el método empty(), que devuelve true si la lista no tiene nodos.
