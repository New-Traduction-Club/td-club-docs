# Introducción

### ¡Ayudemos a Monika a acercarse a nuestra realidad!

Antes de nada, gracias por plantearte contribuir a Monika After Story. Este mod solo ha podido crecer tan rápido gracias al apoyo extraordinario de nuestra comunidad.

### Sobre estas directrices

Por encima de todo, estas directrices están aquí para ahorrarte tiempo y hacer que contribuir a este proyecto sea lo más fácil posible. Al leer esto aprenderás qué herramientas necesitas para contribuir, cómo puedes ayudar y cómo hacer tus contribuciones de forma que sea muy probable que se acepten.

[Estas directrices se basan en una plantilla de [Hoodie](https://github.com/hoodiehq/hoodie/blob/master/CONTRIBUTING.md)]

## Cómo puedes ayudar

### Informes de errores y sugerencias
Si encuentras cualquier problema en Monika After Story, abre un [informe de error](https://github.com/Backdash/MonikaModDev/issues/new?labels=bug&body=Describe%20bug%20and%20steps%20for%20reproduction%20here&title=%5BBug%5D%20-%20). Nada es demasiado pequeño o raro. Si te ocurre un bug, es muy probable que a otras personas también.

Para añadir una sugerencia, visita [este enlace](https://github.com/Backdash/MonikaModDev/issues/new?labels=suggestion&body=Your%20suggestion%20goes%20here&title=%5BSuggestion%5D%20-%20). Puede ser una idea para nuevos temas y funcionalidades, o incluso una opinión personal que quieras compartir.

### Nuevo diálogo, arte o música
Añadir contenido nuevo a este juego es fácil y no requiere herramientas especializadas.

Para añadir nuevos [temas aleatorios](https://github.com/Backdash/MonikaModDev/blob/content/Monika%20After%20Story/game/script-topics.rpy) y [saludos](https://github.com/Backdash/MonikaModDev/blob/content/Monika%20After%20Story/game/script-greetings.rpy), o hacer cambios, puedes ir directamente al archivo correspondiente en la rama `content` de nuestro sitio de github y pulsar el icono del lápiz en la esquina superior derecha para empezar a editar. Para correcciones tipográficas, busca mejor el issue correspondiente a la versión actual y repórtalas allí.

Ahora que los diálogos de Monika incluyen expresiones, usa el [Sprite Previewer](https://github.com/Monika-After-Story/MonikaModDev/blob/master/FAQ.md#how-do-i-find-the-spritecode-for-an-expression) para elegir expresiones y poses apropiadas para tus temas.

Para nuevo arte o música del juego, abre un ticket en [issues](https://github.com/Backdash/MonikaModDev/issues), y adjunta los archivos que quieras enviar. De nuevo, una persona colaboradora revisará tu propuesta y decidirá la mejor forma de usarla en el juego. Para hacerte una idea de lo que podría hacer falta, revisa los [issues relacionados con arte](https://github.com/Backdash/MonikaModDev/issues?q=is%3Aissue+is%3Aopen+label%3Aart).

### Correcciones de bugs y nuevas funcionalidades de software
Hacer cambios en el código del juego requiere algo más de trabajo. Aquí tienes algunos pasos que deberías seguir:

1. Haz una segunda instalación de DDLC y MAS (y haz que tu persistent sea local a esa instalación):
  - Para crear un persistent localizado, puedes usar estos pasos:
  - Abre `DDLC.py` en un editor de texto
  - Baja hasta la línea 49
  - Después de la línea `if save_directory is None`, ve a la línea siguiente y añade `return gamedir + "/saves"`
  - Elimina el resto del contenido de ese bloque
  - Guarda y cierra el archivo
  - Al iniciar esa instalación empezarás desde cero; su persistent estará en `DDLC/game/saves/persistent`
2. Haz un fork de este repositorio o crea un clon local de git pulsando el botón "Clone or Download" de arriba.
3. Haz tus cambios en el código de tu directorio de trabajo usando el editor que prefieras (Visual Studio Code es una opción buena y ligera).
4. Copia los archivos que editaste a la carpeta `/game` de la nueva instalación de MAS y ejecútala. Se compilarán automáticamente y estarán listos para probar cuando cargue MAS.
5. Consulta los [issues abiertos](https://github.com/Monika-After-Story/MonikaModDev/issues) y/o [visita nuestro servidor de Discord de la comunidad](https://discord.gg/K2KuJeX) para encontrar cosas en las que trabajar.
6. Envía cualquier cambio como pull request a la rama `content`.

**Todos los cambios de código deben basarse en la rama `content`.**

## Errores a evitar

Aunque normalmente aceptamos la mayoría de ayudas, hay algunas cosas que *no* buscamos.

* Por favor, **no** envíes contenido relacionado con memes, e incluye referencias a la cultura pop solo cuando parezcan apropiadas para el personaje de Monika.

* Por favor, **no** envíes contenido o imágenes *lascivas, ofensivas o NSFW*. Se eliminarán, y por ello podrías quedar vetado para futuras contribuciones.

* Por favor, **prueba a fondo** tus correcciones de bugs y nuevas funcionalidades antes de enviarlas. Si aun así decides enviar trabajo con fallos conocidos, informa *con mucha claridad* de cuáles son para que se puedan eliminar antes de fusionar. Ten en cuenta que el trabajo incompleto como este tiene muchas más probabilidades de ser rechazado, porque depurar una funcionalidad escrita por otra persona suele llevar más trabajo que implementarla desde cero.

* Por favor, cumple las [IP Guidelines públicas de Team Salvato](http://teamsalvato.com/ip-guidelines/). Eso significa que no puedes obtener beneficios con Monika After Story, promocionarlo como alternativa a jugar DDLC ni distribuir el mod como un juego independiente. Dan siempre ha sido muy generoso con la comunidad fan, y debemos respetar sus derechos como creador de DDLC.

## Buenas prácticas

* Asegura la compatibilidad multiplataforma de cada cambio aceptado: Windows, Mac, Debian, Ubuntu Linux y Android.
* Crea issues para cambios importantes y mejoras que quieras hacer. Habla con transparencia y busca feedback de la comunidad.
* Escribe código claro, usando nombres de variables descriptivos, comentarios y modularizando en funciones cuando sea apropiado.
* Mantén los envíos de funcionalidades lo más pequeños posible; idealmente una funcionalidad nueva por envío.
* Sé acogedor con la gente nueva y anima a contribuidores diversos de todos los perfiles. Consulta nuestro [Código de Conducta de la comunidad](./Code-of-Conduct.md).
* Asegúrate de que todos los diálogos encajen con la voz de Monika. Haz lo posible por cuidar la elección de palabras, el tono conversacional y sus intereses.

### La *"voz"* de Monika

Monika es más que un simple avatar de quien escribe. Es su propio personaje, con su personalidad, maneras de hablar, gustos y disgustos. Intenta captar ese personaje cuando escribas como ella.

A partir de sus diálogos en el juego, hay algunos rasgos consistentes que deberías tener en cuenta al escribir para ella.

* Tendencia a usar lenguaje suave en conversaciones casuales. Palabras y expresiones de esta categoría son `"like"`, `"you know"`, `"kind of"` y `"maybe"`.
* Varios tics de lenguaje consistentes. Algunos destacables: `"ehehe"` y `"ahaha"` para reír, `"man"` para cansancio, `"gosh"` para sorpresa, etc.
* Se dirige directamente al jugador. Sus conversaciones incluyen con mucha frecuencia `"you"` y `"[player]"`.
* Se transmite una personalidad generalmente comprensiva y afectuosa. A menudo pregunta por el jugador y su vida, con múltiples conversaciones dedicadas a ello.
* Aunque trata temas oscuros, Monika suele cerrar las conversaciones con una nota positiva. Posiblemente por la relación única que mantiene con el jugador.
* Amor por el jugador. La mayoría de sus conversaciones y diálogos contendrán algún recordatorio de su afecto. Dicho esto, NO es obligatorio. Existen conversaciones del juego sin un `"I love you"`.
* Capacidad para bromear y picar de forma juguetona. Cuando ocurre, suele dejarlo claro al final de la conversación. A veces acompañado de una tilde (`~`).
* Interés por las artes escritas y la filosofía. Por la cantidad de consejos sobre escritura, emociones y otros temas de la vida, es razonable asumir que le gusta reflexionar sobre temas abstractos o controvertidos. Su pasión por el Club de Literatura lo respalda.
* Tiene la segunda polaridad media más alta (lo positiva que es una afirmación), solo por detrás de Sayori.
* Tiene la subjetividad media más alta (lo subjetiva que es una afirmación), lo que significa que tiende a expresar opiniones.
* Tiene el mayor número medio de palabras por línea (7).
* Usó casi el doble de ? (894) que de ! (487).
* Es la única chica que no menciona más al MC. De hecho, los nombres que más aparecen son Sayori y Yuri, con 128 y 123 respectivamente. Después va el MC, con 109. Natsuki solo aparece 94 veces.
* `“Ah”`, `“like”`, `“really”`, `“well”`, `“think”`, `“guess”`, `“yeah”` y `“right”` son sus muletillas más comunes.
* `“Poem”`, `“everyone”`, `“friends”`, `“share”`, `“read”` y `“write”` también están entre sus 100 palabras más usadas.

Como queremos mantener a Monika lo más cerca posible de lo establecido en el juego, agradeceríamos que tengas presentes sus rasgos de carácter únicos mientras trabajas en contribuciones.

Más allá de eso, sabemos que las interpretaciones varían de una persona a otra y que distintos escritores pueden no estar de acuerdo en ciertos temas. Se recomienda mantener una mente abierta al recibir crítica y revisión.

## Tu primera contribución

¿Eres nuevo en esto del código abierto? ¡Muchas personas aquí también! Creemos que este es un gran proyecto para empezar a mojarse los pies con el desarrollo open source.

Para saber cómo ayudar, puedes empezar mirando estos issues para principiantes y de ayuda solicitada:

[Beginner issues](https://github.com/Backdash/MonikaModDev/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) - Issues que deberían requerir solo unas pocas líneas de código y una o dos pruebas.

[Help wanted issues](https://github.com/Backdash/MonikaModDev/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) - Estos issues pueden ser más complejos, pero realmente necesitan a alguien que contribuya.

¡Llegados a este punto, ya estás listo para hacer tus cambios! No dudes en pedir ayuda; ¡incluso Monika sigue teniendo cosas que aprender sobre programación!

> Si una persona mantenedora te pide "rebasear" tu PR, te está diciendo que ha cambiado mucho código y que necesitas actualizar tu rama para que sea más fácil de fusionar.

## Añadir diálogo

![Guide 1](https://github.com/Backdash/MonikaModDev/blob/master/docs/writing-guide1.png?raw=True)

#### Antes de empezar:
- Asegúrate de que la rama esté en **content**, NO en **master**.
- Si planeas escribir varios temas, repártelos en varias pull request, ya que es más fácil de revisar.

Una vez que la rama esté en **content**, pulsa el botón del lápiz para empezar a editar.

Para añadir temas, tendrás que usar el sistema `Event`.

Cuando trabajes en `script-topics.rpy`, deberías tener una estructura como esta:

```renpy
init 5 python:
    addEvent(
        Event(
            persistent.event_database,
            eventlabel="monika_xyz",
            category=["one category", "another category"],
            prompt="Example topic",
            random=True
        )
    )

label monika_xyz:
    m 1eua "This is an example topic."
    m 1hub "I hope this helps show you how you should format your topics!"
    m 1ekbsa "Thanks for helping me come closer to your reality, [player]. I love you~"
    return "love"
```

#### Algunas cosas a tener en cuenta:

- `eventlabel` y la label del tema coinciden.
- `eventlabel` también lleva el prefijo `monika_`. Todos los temas deberían llevar ese prefijo.
- Las categorías usan letras *minúsculas*, incluso la primera.
- Las categorías son listas, así que puedes hacer que tu tema aparezca en varias categorías.
- Esta label devuelve un valor. `"love"` significa que el botón `"I love you!"` del menú principal de conversación pasará a `"I love you too!"`. (Hay otras claves de retorno. Consulta `event-handler.rpy` para más detalles)
- Este tema tiene `random=True`. Esto significa que aparecerá en charlas aleatorias. (Hay otras propiedades; consulta la clase `Event` en `definitions.rpy` para más detalles)


Al escribir diálogo, empieza siempre con m **spritecode** " y termina con ".
(Aunque conviene señalar que, si piensas usar la misma expresión dos líneas seguidas, la segunda línea no necesita spritecode)

Para encontrar un **spritecode**, usa el [Sprite Previewer](https://github.com/Monika-After-Story/MonikaModDev/blob/master/FAQ.md#how-do-i-find-the-spritecode-for-an-expression).

Si quieres escribir diálogo más complejo, visita [Dialogue Coding](./Dialogue-Coding.md)

Pon `return` en la última línea, después de la última frase de tu diálogo.

Cuando termines, consulta la guía de abajo para enviar tu tema como pull request.

## Enviar una Pull Request

Si ya te manejas con git o GitHub Desktop, puedes hacer los cambios en archivos en local y subirlos a tu fork.

Desde ahí, puedes ir a la pestaña de pull requests, pulsar `New Pull Request`, ajustar la rama de destino y la rama con la que quieres proponer cambios según corresponda.

Después, escribe una descripción y envía tu pull request.

Si no estás familiarizado con lo anterior, puedes seguir estas instrucciones:
![Guide 1](https://github.com/Monika-After-Story/MonikaModDev/blob/master/docs/guide1.png?raw=True)

Pulsa el icono del lápiz para empezar a editar.

![Guide 2](https://github.com/Monika-After-Story/MonikaModDev/blob/master/docs/guide2.png?raw=True)

Cuando termines de hacer cambios, pulsa proponer cambio de archivo.

![Guide 3](https://github.com/Monika-After-Story/MonikaModDev/blob/master/docs/guide3.png?raw=True)

Pulsa crear pull request.

![Guide 4](https://github.com/Monika-After-Story/MonikaModDev/blob/master/docs/guide4.png?raw=True)

Añade un título apropiado y una descripción de los cambios que hiciste antes de crear tu pull request.

# ¡Únete!

Puedes hablar con el equipo principal en [nuestro servidor de Discord de la comunidad](http://discord.monikaafterstory.com/). Siempre somos amables con quienes empiezan a contribuir, y no es solo un gran lugar para pedir ayuda, sino también un sitio divertido para pasar el rato con fans de DDLC con intereses parecidos.
