### Mi solución a la actividad 7

<!-- Autoevaluación: reflexiona sobre tu ProcesoSección titulada «Autoevaluación: reflexiona sobre tu Proceso»
🎯 Enunciado

Esta actividad te invita a reflexionar sobre tu experiencia de aprendizaje en esta unidad. Evalúa tu propio proceso, identifica qué funcionó bien para ti, qué desafíos encontraste y cómo podrías mejorar tu aprendizaje en el futuro. La honestidad y la autocrítica constructiva son clave.

Responde las siguientes preguntas de manera reflexiva y elaborada (intenta escribir al menos 5 líneas por respuesta):

Comprensión previa vs. actual: antes de esta unidad, ¿Qué sabías sobre los patrones de diseño Observer, Factory y State? ¿Consideras que ahora los entiendes 
mejor y, sobre todo, sabes cuándo y por qué aplicarlos? Justifica tu respuesta comparando tu conocimiento previo con el actual.
Facilidad y dificultad: ¿Qué partes de esta unidad (conceptos, análisis del caso de estudio, implementación en tu proyecto) te resultaron
más fáciles de comprender o realizar? ¿Por qué crees que fue así?
Retos y soluciones: ¿Qué parte te pareció más difícil o te tomó más tiempo? ¿Fue entender un patrón en particular, aplicarlo correctamente en tu
proyecto, depurar errores relacionados con los patrones, o algo más? ¿Cómo lograste superar esa dificultad? Describe el proceso que seguiste.
Mejora del aprendizaje: si tuvieras la oportunidad de volver a realizar esta unidad, ¿Qué harías de manera diferente para profundizar tu comprensión
o mejorar tu eficiencia? (Ej: dedicar más tiempo al diseño inicial, probar de forma diferente, consultar otras fuentes, etc.).
Transferencia y utilidad futura: ¿Crees que los conocimientos y habilidades adquiridas sobre estos patrones de diseño te serán útiles en futuros cursos, 
proyectos personales o incluso en tu carrera profesional? ¿Por qué sí o por qué no? ¿Puedes imaginar escenarios específicos donde podrías aplicarlos?
Relevancia interdisciplinar: Lee el siguiente texto sobre la importancia de la programación para artistas (proporcionado en la descripción original de la Unidad 5 sobre OOP,
enfocado en animación pero extensible a otras áreas creativas):
Aprender a programar puede ser muy valioso para un artista […]. Automatización […], Mayor control y personalización […], Arte generativo y animación procedural […], Interactividad y
nuevos medios […], Mejor integración con otras disciplinas […], Acceso a inteligencia artificial […], 
Independencia y creación de herramientas propias […]. Ahora, piensa específicamente en los patrones de diseño que acabas de estudiar. 
¿Crees que entender estos patrones (que ayudan a estructurar código complejo) podría ser útil incluso para alguien en un campo creativo que programa ocasionalmente para
sus proyectos (como arte generativo, instalaciones interactivas, herramientas personalizadas)? ¿Por qué sí o por qué no? ¿Podrían estos patrones ayudar a que sus herramientas o proyectos 
sean más robustos, mantenibles o extensibles? -->

- Comprensión previa vs. actual: antes de esta unidad, ¿Qué sabías sobre los patrones de diseño Observer, Factory y State? ¿Consideras que ahora los entiendes 
mejor y, sobre todo, sabes cuándo y por qué aplicarlos? Justifica tu respuesta comparando tu conocimiento previo con el actual.

R/= State ya lo conocía desde antes por lo que aprendí en programación orientada a objetos, por lo tanto no se me hizo nuevo pero si el factory y diseño observer.

Después de haber trabajado con estos patrones, mi comprensión de ellos ha cambiado significativamente. Ahora puedo ver claramente cómo cada patrón resuelve un problema específico en la organización del código y cuándo aplicarlos. La diferencia entre mi conocimiento previo y actual es bastante notoria.

Observer: Ahora entiendo que este patrón es útil cuando un objeto necesita notificar a otros objetos sin que estén directamente acoplados. 
Antes pensaba que era solo para recibir actualizaciones, pero ahora sé que ayuda a mantener un sistema flexible, donde los objetos pueden reaccionar a eventos de manera independiente. 
Lo usé en mi proyecto para que las partículas pudieran reaccionar a las teclas presionadas sin tener que estar directamente relacionadas con la clase que maneja la entrada del usuario.

Factory: Este patrón ahora lo veo como una forma de delegar la creación de objetos a una clase especializada. La mayor ventaja es que desacopla la lógica de creación del código principal,
lo que hace que el código sea más limpio y fácil de extender. En mi proyecto, lo usé para crear diferentes tipos de partículas sin tener que escribir lógica de creación dentro del código principal,
lo que facilitó agregar nuevos tipos de partículas sin modificar la estructura general.

- Facilidad y dificultad: ¿Qué partes de esta unidad (conceptos, análisis del caso de estudio, implementación en tu proyecto) te resultaron
más fáciles de comprender o realizar? ¿Por qué crees que fue así?

R/= Se me hizo más fácil entender las de investigación, despues de todo era solo experimentar y leer, además de que pedía mi opinion primero y me daba una pista de como sería.

- Retos y soluciones: ¿Qué parte te pareció más difícil o te tomó más tiempo? ¿Fue entender un patrón en particular, aplicarlo correctamente en tu
proyecto, depurar errores relacionados con los patrones, o algo más? ¿Cómo lograste superar esa dificultad? Describe el proceso que seguiste.

R/= La actividad 5, no hice un proyecto completamente nuevo pero si uno diferente al otro. Al estilo que me basé en el de caso de estudio para poder realizarlo. Superé
esa dificultad al estar experimentando en mover cosas y preguntarme que pasaría si hago esto o como funciona.

- Mejora del aprendizaje: si tuvieras la oportunidad de volver a realizar esta unidad, ¿Qué harías de manera diferente para profundizar tu comprensión
o mejorar tu eficiencia? (Ej: dedicar más tiempo al diseño inicial, probar de forma diferente, consultar otras fuentes, etc.).

R/= Más a la experimental y práctica, siento que esta es una unidad mas que todo de experimentación. Dure mucho tiempo en la actividad 5 pero la logré entender.

- Transferencia y utilidad futura: ¿Crees que los conocimientos y habilidades adquiridas sobre estos patrones de diseño te serán útiles en futuros cursos, 
proyectos personales o incluso en tu carrera profesional? ¿Por qué sí o por qué no? ¿Puedes imaginar escenarios específicos donde podrías aplicarlos?

R/= Sí, los conocimientos adquiridos sobre los patrones de diseño serán útiles en futuros proyectos. 
Ayudan a estructurar el código de forma más organizada y escalable. Los patrones como Observer, Factory y State facilitan el mantenimiento y la extensión del código, 
lo que es clave tanto en proyectos personales como profesionales.

Por ejemplo, Observer podría usarse en aplicaciones interactivas donde varios elementos deben actualizarse a la vez, Factory en la creación de objetos de manera modular y 
State en sistemas que cambian de comportamiento según su estado. Estos patrones serán esenciales en proyectos grandes y colaborativos, donde la claridad y el desacoplamiento del código son fundamentales.

- Relevancia interdisciplinar: Lee el siguiente texto sobre la importancia de la programación para artistas (proporcionado en la descripción original de la Unidad 5 sobre OOP, enfocado en animación pero extensible a otras áreas creativas):
Aprender a programar puede ser muy valioso para un artista […]. Automatización […], Mayor control y personalización […], Arte generativo y animación procedural […], Interactividad y nuevos medios […], Mejor integración con otras disciplinas […], Acceso a inteligencia artificial […], Independencia y creación de herramientas propias […]. Ahora, piensa específicamente en los patrones de diseño que acabas de estudiar. ¿Crees que entender estos patrones (que ayudan a estructurar código complejo) podría ser útil incluso para alguien en un campo creativo que programa ocasionalmente para sus proyectos (como arte generativo, instalaciones interactivas, herramientas personalizadas)? ¿Por qué sí o por qué no? ¿Podrían estos patrones ayudar a que sus herramientas o proyectos sean más robustos,
 mantenibles o extensibles?

R/= Sí, entender los patrones de diseño como Observer, Factory y State podría ser muy útil para un artista que programa ocasionalmente en proyectos creativos. Estos patrones ayudan a estructurar el código de manera más clara y organizada, lo que facilita la creación de herramientas personalizadas o proyectos de arte generativo.





