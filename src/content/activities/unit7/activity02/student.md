### Mi solución a la actividad 2

- opengl32.lib: Esta biblioteca viene con Windows y te da acceso a las funciones básicas de OpenGL (hasta la versión 1.1). Es importante porque te permite arrancar OpenGL, pero no tiene las funciones más avanzadas.

- GLFW: Esta es la biblioteca que te ayuda a crear la ventana donde vas a mostrar los gráficos y también se encarga de gestionar las entradas como el teclado y el ratón. Hay dos archivos principales:

- glfw3.lib: Es el que le dice a Visual Studio dónde encontrar las funciones de GLFW cuando compilas el código.

- glfw3.dll: Este es el archivo que tiene el código real que se usa cuando ejecutas el programa. Si no está, aunque el programa compile, no se ejecutará.

- GLAD: OpenGL tiene funciones avanzadas que no están en opengl32.lib, por eso necesitamos GLAD. GLAD se encarga de cargar esas funciones modernas directamente desde los drivers de tu tarjeta gráfica. Para poder usarlas, tienes que agregar los archivos de GLAD a tu proyecto.

- GLM (opcional): Esta biblioteca es útil si necesitas hacer cálculos de matemáticas para gráficos 3D, como trabajar con matrices y vectores. No necesitas ningún archivo extra, solo los encabezados para incluirla en tu proyecto.

#### ¿Cómo se relacionan todas estas partes?
- GLFW es la que crea la ventana y se encarga de los eventos (teclado, ratón).

- opengl32.lib arranca OpenGL, pero solo tiene funciones básicas.

- GLAD es lo que te permite acceder a las funciones más avanzadas de OpenGL, porque las carga desde los drivers de la tarjeta gráfica.

- GLM es útil para las matemáticas que necesitas hacer en gráficos 3D, pero no es obligatoria.
