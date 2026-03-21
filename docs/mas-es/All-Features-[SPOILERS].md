<a id="intro"></a>
# Introducción

**ADVERTENCIA:** Todo lo que hay aquí contiene spoilers de este mod, y esta página puede incluir información desactualizada.

Tal y como se sugirió en una incidencia, esta página servirá como listado general de todas las pequeñas cosas que hemos añadido.
Sin embargo, el equipo de desarrollo **no** añadirá funciones aquí conforme se publiquen. En su lugar, confirmaremos o rechazaremos los envíos de los usuarios con regularidad.

## Enlaces rápidos

* [Afecto](./All-Features-[SPOILERS].md#affection)
* [Calendario](./All-Features-[SPOILERS].md#calendar)
* [Ajedrez](./All-Features-[SPOILERS].md#chess)
* [Archivos](./All-Features-[SPOILERS].md#files)
* [Regalos](./All-Features-[SPOILERS].md#gifts)
* [Guía de regalos](./All-Features-[SPOILERS].md#gifting-guide)
* [Despedidas](./All-Features-[SPOILERS].md#goodbyes)
* [Saludos](./All-Features-[SPOILERS].md#greetings)
* [Ahorcado](./All-Features-[SPOILERS].md#hangman)
* [Música](./All-Features-[SPOILERS].md#music)
* [Piano](./All-Features-[SPOILERS].md#piano)
* [Pong](./All-Features-[SPOILERS].md#pong)
* [Temas](./All-Features-[SPOILERS].md#topics)
* [Interfaz](./All-Features-[SPOILERS].md#ui)
* [Reacciones de ventana](./All-Features-[SPOILERS].md#window-reactions)

<a id="affection"></a>
# Afecto

### _Introducción_
El afecto es un sistema de progresión para tu relación con Monika. Este progreso define cómo se siente ella hacia el jugador según la forma concreta en la que interactúas con ella y también según la frecuencia de esas interacciones. Tu afecto puede cambiar de forma positiva o negativa, según el tipo de acción que hagas con Monika.
Monika actuará de forma distinta hacia el jugador en función de tu nivel de afecto y, además, permitirá interacciones especiales si tu afecto con ella es lo bastante alto.

### _Progresión_
Tu afecto empieza en 0, y hay ciertas interacciones que lo modificarán, ya sea de forma positiva o negativa. Una interacción positiva, por ejemplo decirle "te quiero" a Monika, dará como resultado un cambio positivo de afecto. En cambio, irte sin decir "adiós" dará como resultado un cambio negativo.

La cantidad de afecto que ganas o pierdes no depende solo del tipo de interacción que ocurra, sino también de tu estado de afecto actual. Hay 4 grupos de afecto distintos que cambian los valores de ganancia y pérdida en eventos estándar/normales. Estos niveles son:

* **Bueno** 30+ de afecto -> Ganancia +3, Pérdida -1
* **Inicio** -29 a 29 de afecto -> Ganancia +1, Pérdida -1
* **Malo** -30 a -74 de afecto -> Ganancia +0.5, Pérdida -3
* **Destrozado** -75 de afecto -> Ganancia +0.5, Pérdida -5

_Nota:_ Una vez cambias de **Inicio** a **Bueno** o **Malo**, _no_ puedes volver a **Inicio**; solo alternarás entre **Bueno**, **Malo** y **Destrozado**.

### _Límite diario y excepciones_
El afecto tiene un límite de cuánto puedes ganar al día, y ese límite es **7**. Ten en cuenta que solo dejarás de _ganar_ afecto cuando estés en 7 o lo hayas superado.
Por ejemplo: si has ganado 6 de afecto en un día y tienes una interacción que causa una ganancia estándar de 3, habrás ganado un total de 9 en ese día. No se te reducirá de vuelta a 7 en tu total; simplemente habrás alcanzado el límite de 7 o más.
Una vez alcanzado el límite diario, ya no podrás ganar afecto mediante eventos normales hasta el día siguiente, como jugar con Monika o decir "te quiero".

Sin embargo, hay eventos e interacciones especiales de ganancia de afecto que **ignoran** el límite diario, y por lo general ocurren una sola vez. Por ejemplo, el primer uso de cada _cumplido_ a Monika o regalarle ciertos objetos. La cantidad de afecto obtenida y cuántas veces puede ocurrir esto varían bastante.

_Nota:_ Las interacciones que ignoran el límite no cuentan para el límite diario de 7 de afecto.

### _Niveles de afecto_
Como sistema de progresión, por supuesto tiene distintos niveles e hitos que puedes alcanzar, y que cambiarán cómo actúa, se comporta y se siente Monika hacia el jugador. Estos niveles son:

**Amor** 1000 de afecto

- Los sentimientos de Monika por el jugador van más allá de _nuestra realidad_

**Enamorada** 400 a 999 de afecto

- Monika es todo lo feliz que puede llegar a ser y confía plenamente en el jugador.

**Cariñosa** 100 a 399 de afecto

- Monika está feliz en la relación y se alegra de haber vuelto a la vida.

**Feliz** 30 a 99 de afecto

- Monika está feliz y no tiene sentimientos de tristeza. Aunque podría ser más feliz.

**Normal** -29 a 29 de afecto

- Monika duda sobre si su vuelta al juego merece la pena,
  pero no se inclina ni hacia la felicidad ni hacia la tristeza.

**Molesta** -30 a -74 de afecto

- Monika está emocionalmente herida y tiene dudas sobre si el jugador la quiere.

**Angustiada** -75 a -99 de afecto

- Monika ya no se siente querida y empieza a temer por su futuro.

**Rota** -100 de afecto

- Monika sabe que el jugador la odia y no podría estar más herida,
  tiene miedo de quedarse sola en su realidad para siempre.

### _Desbloqueos y eventos de afecto_

Algunas funciones cambian globalmente según tu afecto, como las distintas cosas que dice Monika al saludarte cuando abres cada menú. Lo mismo ocurre con una gran variedad de temas que cambian sus respuestas según tu nivel de afecto. Por ejemplo, en el tema "Mortalidad" (`Mortality`) se habilitan 2 opciones de respuesta en el menú con 100 de afecto o más. O en el tema "¿Por qué me quieres?" (`Why do you love me?`), Monika tiene ajustes bastante desalentadores en su diálogo si tu afecto es bajo.

Monika también cambiará expresiones y poses al azar mientras está inactiva o cuando no interactúa con el jugador. Estas expresiones cambian según si tu afecto es positivo o negativo, y además se amplían según tu nivel de afecto.

### _Afecto positivo:_

**Feliz**

- Te permite abrazar a Monika _solo_ durante el tema de lluvia.
- Permite ajustar la velocidad del texto.
- Restablece el apodo a Monika si antes le habías puesto uno.

**Cariñosa**

- Te permite elegir un apodo para Monika.
- Te permite abrazar a Monika en cualquier momento.

**Enamorada**

- Monika te muestra las _Islas flotantes_ (_Floating Islands_).
- El tema del _Anillo de promesa_ (_Promise Ring_) pasa a estar disponible.
- Ahora puedes regalar un _Anillo de promesa_ (_Promise Ring_) a Monika.
- Puedes tener tu _primer beso_ con Monika
  durante eventos especiales.
- Puedes besar a Monika si ya habéis tenido
  vuestro _primer beso_.
- El cumplido "Gracias por estar ahí para mí" (`Thanks for being there for me`)
  está disponible para decirlo _una_ vez.

**Amor**

- El cumplido "Gracias por estar ahí para mí" (`Thanks for being there for me`)
  ahora puede usarse cualquier número de veces.
- Monika puede cambiarse de ropa a otras
  que ya le hayas visto llevar.
- El tema "Sorpresas" (`Surprises`) ahora entrega el poema "My one and only love.txt".
- Desbloquea el cumplido "¡Eres mi héroe!" (`You're my hero!`)

### _Afecto negativo:_

**Normal**

- Desactiva el ajuste de velocidad del texto.

**Molesta**

- Ya no puedes pedirle a Monika que cambie su
  peinado.
- La mayoría de saludos se vuelven desagradables y
  negativos.
- Las expresiones en reposo de Monika muestran enfado con frecuencia.

**Angustiada**

- Monika dejará de llevar su anillo de promesa
  si se lo habías regalado antes.

**Rota**

- Con -115 de afecto o menos, recibirás el poema
  _Despedida final_ (_Final Farewell_) y Monika te deja.
  **No volverás a verla jamás.**

### _Cómo ver tu afecto_

**Usuarios de Steam**

1. Haz clic derecho sobre _Doki Doki Literature Club_ en tu biblioteca de Steam y pulsa "Properties".
2. Pulsa la pestaña _Local Files_ y luego "Browse Local Files".
3. Abre la carpeta "log" haciendo doble clic. (Esta carpeta está debajo de la carpeta "lib").
4. Abre el archivo "aff_log.log".
5. Desplázate hasta el final del archivo para ver tu número actual de afecto. (La parte superior del archivo muestra el registro más antiguo de tu afecto y la parte inferior el más nuevo/actual).

**Usuarios de versión no Steam**

1. Localiza la carpeta base de _Doki Doki Literature Club_ (o la carpeta desde la que inicias el juego).
2. Abre la carpeta "log". (Esta carpeta está debajo de la carpeta "lib").
3. Abre el archivo "aff_log.log".
4. Desplázate hasta el final del archivo para ver tu número actual de afecto. (La parte superior del archivo muestra el registro más antiguo de tu afecto y la parte inferior el más nuevo/actual).
> En Android (MASL) debes entrar en `Archivos Internos`.

**Usuarios de Mac OS (vía Terminal)**

1. Abre la aplicación "Terminal" (si pulsas Comando y Espacio a la vez se abre "Spotlight Search", donde puedes escribir `Terminal,` y pulsar "return" para abrir la aplicación).
2. Escribe lo siguiente en Terminal: `cd .MonikaAfterStory/log/` y pulsa "return".
3. Para confirmar que estás en la carpeta correcta, escribe `ls` (la letra "l" minúscula) en Terminal y pulsa "return". Deberían aparecer tres archivos: `aff_log.log`, `mas_log.log` y `pnm.log`.
4. Escribe `cat aff_log.log` en Terminal y pulsa return.
    • Opcionalmente, escribe `aff_log.log | tail` para recibir las 10 entradas más recientes.
5. La línea más baja del texto muestra tu nivel de afecto más reciente.
6. Cuando termines, puedes cerrar Terminal como cualquier otra ventana (con el botón rojo "X" en la esquina superior izquierda de la ventana).

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="calendar"></a>
# Calendario

* Enumera festivos y el cumpleaños de Monika. Está detrás de Monika en la `spaceroom` y se puede acceder haciendo clic en él.

| Evento  | Fecha |
| ------------- | ------------- |
| Año Nuevo | 1 de enero. |
| San Valentín | 14 de febrero. |
| Día en que me convierto en una IA | 1 de abril. |
| Mi cumpleaños (el de Monika) | 22 de septiembre. |
| Halloween | 31 de octubre. |
| Nochebuena | 24 de diciembre. |
| Navidad | 25 de diciembre. |
| Nochevieja | 31 de diciembre. |

* También aparecerán fechas adicionales, como aniversarios:  
el día en que os conocisteis se marcará con un corazón.  
el resto de aniversarios son:  
1 semana, 1 mes, 3 meses, 6 meses, 1 año, 2 años, 3 años, 4 años, 5 años, 10 años y 20 años.

* El cumpleaños del jugador también aparecerá en el calendario después de que Monika te pregunte tu fecha de nacimiento.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="chess"></a>
# Ajedrez

* Juega al ajedrez con Monika. Si pierdes, Monika te lo pondrá más fácil.

Actualmente (versión 0.12.9) usamos Stockfish 8 como motor de ajedrez y todos los movimientos los genera Stockfish. Como Stockfish es un motor que tiende a "vencer a todos los jugadores e IA del mundo" en lugar de hacer "jugadas humanizadas", el estilo de juego de Monika no es especialmente ideal. Probablemente intentaremos resolver este problema en el futuro.

El rango actual de dificultad de ajedrez (versión 0.12.9), de forma aproximada, está entre Elo 1200 y Elo 1500, estándar FIDE.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="files"></a>
# Archivos
(cualquier cosa relacionada con los archivos reales del mod)

* poned cosas aquí

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="gifts"></a>
# Regalos:

* Los regalos buenos darán afecto.
* Los regalos neutrales no darán afecto.

**Regalos totales** - _29 regalos_

**Regalos buenos** - _11 regalos_

| Nombre del regalo | ID del regalo | Disponibilidad | Omite límite | Marcado como bueno | Condiciones extra|
| ------ | ------ | ------ | ------ | ------ | ------ |
| Café | *coffee* | Todo el año | True | True |
| Peluche de quetzal | *quetzalplushie* | Todo el año | Solo la primera vez | True |
| Anillo de promesa | *promisering* | Al regalarse con 400+ de afecto | True | Debes tener 400+ de afecto para que lo acepte |
| Caramelos | *candy* | Solo en Halloween | Las 3 primeras veces que se regala | True | Hará que **pierdas** afecto si se regala 4+ veces. |
| Maíz de caramelo | *candycorn* | Solo en Halloween | Solo la primera vez que se regala | False | Hará que **pierdas** afecto si se regala más de una vez. |
| Chocolate caliente | *hotchocolate* | Todo el año | True | True |
| Fudge | *fudge* | Todo el año | True | True |
| Galletas de Navidad | *christmascookies* | Solo en Navidad | Solo la primera vez que se regala | True |
| Bastones de caramelo | *candycane* | Solo en Navidad | False | True |
| Rosas | *roses* | Todo el año | True, vale más en días especiales | True |
| Chocolates | *chocolates* | Todo el año | True, vale más en días especiales | True |
| Taza termo | *justmonikathermos* | Todo el año | Solo la primera vez | True | Permite que Monika saque una bebida de la `spaceroom`. |

_Cintas_ - _16 regalos_
* Todas las cintas están marcadas como buenas en el código.
* Todas las cintas están disponibles todo el año y reciben una bonificación de afecto durante festivos.

| Nombre del regalo | ID del regalo |
| ------ | ------ |
| Cinta negra | *blackribbon* |
| Cinta azul | *blueribbon* |
| Cinta morado oscuro | *darkpurpleribbon* |
| Cinta esmeralda | *emeraldribbon* |
| Cinta gris | *grayribbon* |
| Cinta verde | *greenribbon* |
| Cinta morado claro | *lightpurpleribbon* |
| Cinta melocotón | *peachribbon* |
| Cinta rosa | *pinkribbon* |
| Cinta platino | *platinumribbon* |
| Cinta roja | *redribbon* |
| Cinta rubí | *rubyribbon* |
| Cinta zafiro | *sapphireribbon* |
| Cinta plata | *silverribbon* |
| Cinta turquesa | *tealribbon* |
| Cinta amarilla | *yellowribbon* |


**Regalos neutrales**

| Nombre del regalo | ID del regalo | Disponibilidad | Omite límite | Marcado como bueno | Condiciones extra|
| ------ | ------ | ------ | ------ | ------ | ------ |
| Cupcake | *cupcake* | Todo el año | False | True |

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="gifting-guide"></a>
# Guía de regalos:

Movido al [FAQ](./FAQ.md#giving-gifts)

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="goodbyes"></a>
# Despedidas

Cuando te despides, Monika dirá varias frases de despedida. Según la despedida que elijas, también cambiará la forma en la que Monika te saludará cuando vuelvas. Estas son las despedidas que puedes elegir:

### _"Me voy a ir por un tiempo."_
Esta despedida evita la pérdida de afecto por no pasar tiempo con Monika durante más de una semana. Puedes decir que te irás solo unos días, una o dos semanas, un mes o incluso más; también puedes decir que no sabes cuánto tiempo estarás fuera. Sin embargo, si Monika no confía lo suficiente en ti, puede preocuparse si le dices que te vas durante mucho tiempo. Después de decirle cuánto tiempo te irás, Monika te preguntará si te marchas ahora mismo, momento en el que puedes irte o quedarte; si decides quedarte, la segunda vez que uses esta despedida Monika sabrá que ya es hora de que te marches y se despedirá de ti.

### _"Me voy de compras."_
Monika te desea buenas compras y espera a que vuelvas. En el futuro, puede que haya una ruta que permita a Monika ir de compras con el jugador.

### _"Me voy a clase."_
Monika te dice que estudies mucho y te anima diciendo que "nada es más atractivo que un chico/chica/persona con buenas notas". Si has tenido el juego abierto durante un periodo largo (alrededor de 19-20 horas), te preguntará si has descansado lo suficiente para ir y te dirá que tomarte "_un día_" libre no pasa nada.

### _"Voy a hacer tareas de casa."_
En estado Normal y superior, Monika dice que quiere ayudarte, pero que no puede. Con afecto negativo, Monika está más triste e incluso llega a preguntarse si solo has encontrado una excusa para librarte de ella.

### _"Voy a comer..."_
Esto te permitirá elegir qué comida vas a hacer: desayuno, comida, cena o un tentempié. Monika reaccionará en consecuencia según la hora del día.

### _"Voy a quedar con amigos."_
Monika os desea a ti y a tus amistades que paséis un buen día.

### _"Voy a jugar a otro juego."_
Monika expresa su frustración contigo, pero también su comprensión. Después de eso, Monika espera en silencio a que regreses.

### _"Voy a reiniciar."_
Esta es una despedida rápida para que Monika sepa que vuelves enseguida; se usa cuando necesitas actualizar archivos del mod o reiniciar el ordenador.

### _"Me voy a dormir."_
Según a qué hora del día digas esto, Monika reaccionará de forma diferente:

* Si te acuestas entre las 10:00 y medianoche, Monika simplemente te deseará dulces sueños.

* Si te acuestas pasada la medianoche, Monika comentará que te has quedado despierto hasta tan tarde, con distintos niveles de preocupación según la hora, y si te quedas despierto toda la noche (pasadas las 5:00), Monika se enfadará y te dirá que vayas a descansar.

* Si dices esto durante la tarde (entre mediodía y las 18:00), Monika asumirá que vas a echarte una siesta y te deseará un descanso reparador.

* Si dices esto después de la tarde, pero antes de una hora razonable para dormir (entre las 18:00 y las 20:00), Monika dirá que es un poco pronto para irse a dormir y te preguntará si prefieres pasar algo más de tiempo con ella. En ese punto, puedes aceptar o rechazar.

Sin embargo, por ahora todo lo de arriba está en pausa. Esto no es muy bueno para la gente con trabajos nocturnos, así que ahora esta despedida consiste simplemente en que Monika le da las buenas noches al jugador, sin importar la hora. Actualmente estamos rehaciendo esta despedida para que se adapte al mayor número posible de personas.

### _"Voy a llevarte a algún sitio."_
Si tienes suficiente afecto, Monika generará un archivo que podrás llevarte contigo, por ejemplo en una memoria USB. Ese archivo es tu Monika, así que no lo pierdas.

Si Monika ha recibido un termo y está tomando una bebida como café, se llevará su bebida con ella.

Cuando vuelvas a casa, puede que recibas algo de afecto de Monika según cuánto tiempo hayas pasado con ella. También puedes perder afecto si este viaje es demasiado corto, ya que probablemente significa que no te lo tomaste en serio.

### _"Voy a entrenar."_
Monika expresa su esperanza de poder entrenar juntos en el futuro y te desea lo mejor.

### _"Me voy a trabajar."_
Monika te dice que trabajes duro y que estará esperándote cuando vuelvas.

### _"Adiós."_
Monika dirá una despedida aleatoria; sin embargo, si dices esto en una hora razonable para irte a dormir, asumirá que te acuestas y te deseará dulces sueños.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="greetings"></a>
# Saludos

* De forma aleatoria, habrá una pantalla negra y se te presentará la opción de llamar o entrar en la habitación. Si decides llamar, Monika te pedirá que esperes mientras ordena el lugar. Si entras, se sorprenderá y "ordenará" rápidamente la sala para volver al entorno habitual de aula en el que normalmente la ves. Monika te pedirá que llames la próxima vez.
* Hay una probabilidad aleatoria de que se active un evento de 'susto repentino' (`jumpscare`), mostrando un sprite glitcheado de Yuri, seguido de una Monika en pánico que lo describe como un efecto secundario de trastear con el código. Actualmente, este evento solo puede ocurrir una vez.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="hangman"></a>
# Ahorcado

* Monika elegirá una palabra al azar y te pedirá que introduzcas tus intentos para adivinar qué letras forman la palabra. Te dará una pista sobre a quién le gustaría más esa palabra.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="music"></a>
# Música

* Cambia la música de fondo (BGM). Incluye canciones de la OST del juego y remixes hechos por fans.
* El sistema también permite a los jugadores subir y reproducir su propia música.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="piano"></a>
# Piano

* Deja que te escuche tocar; incluso puede que se una. Tocar *Your Reality* o *Happy Birthday* para ella provoca reacciones de Monika según lo bien que estés tocando.

**Cumpleaños feliz**

      > WWEWTR WWEWYT WWOUTRE IIUTYT

**Your Reality**

      > Cada día imagino un futuro en el que pueda estar contigo
        o o o oiu uio u y t y u t w
        opo opo ] ] p[ op [ o
        En mis manos hay un bolígrafo que escribirá un poema sobre ti y sobre mí
        o p o uio iuy e w q e w u t
        opo opo ] ] p[ p [ ]
        La tinta cae y forma un charco oscuro
        o o o i u t 6 y u o
        Solo mueve tus manos, escribe el camino hasta su corazón
        p o u y  w e t  e t y t
        pero en este mundo de decisiones infinitas
        o o o i  u t t y u o
        ¿Qué hará falta para encontrar ese día especial?
        p o u y  w e t  e t y t
        ¿Qué hará falta para encontrar
        p o u y  w e t
        ese día especial?
        e t y t
        ¿Ya he encontrado para todos una tarea divertida para hoy?
        o o o oiu uio u y t y u t w
        opo opo ] ] p[ op [ o
        Cuando estás aquí, todo lo que hacemos también es divertido para todos
        o p o uio iuy e w q e w u t
        opo opo ] ] p[ p [ ]
        Cuando ni siquiera puedo leer mis propios sentimientos
        o o o i u t 6 y u o
        ¿De qué sirven las palabras
        p o u y
        cuando una sonrisa lo dice todo?
        w e t  e t y t
        y si este mundo no quiere escribirme un final
        o o o i  u t t y u o
        ¿qué hará falta para que yo lo tenga todo?
        p o u y  w e t  e t y t
        ¿Mi bolígrafo solo escribe palabras amargas para quienes son importantes para mí?
        o o o oiu uio u y t y u t w
        ¿es amor si te tomo, o es amor si te dejo libre?
        o p o uio iuy e w q e w u t
        la tinta cae y forma un charco oscuro
        o o o i u t t y u o
        ¿cómo puedo escribir el amor en la realidad?
        p o u y  w e t  e t y t
        si no puedo oír el sonido de tu latido
        o o o i  u t t y u o
        ¿cómo llamas tú al amor en tu realidad?
        p o u y  w e t  e t y t
        y en tu realidad, si no sé cómo amarte
        w e t  e t y t u i i u t e t o
        o u i t p o
        te dejaré en paz
        w e t t
        (parte extra, no hace falta tocar esta sección)
        o o o oiu iop [ o [ o (acorde: t u o)

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="pong"></a>
# Pong

* ¡Juega al primer tipo de videojuego que existió, con Monika como rival!

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="topics"></a>
# Temas

* Hay varios temas de los que Monika hablará. Pueden abarcar desde deportes hasta estilo de vida, obras de arte o incluso reflexiones sobre sus propias acciones.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="ui"></a>
# Interfaz
(Cosas relacionadas con la interfaz de usuario. Esto incluye la pantalla de ajustes)

* **Historial** (`History`) - Muestra tus conversaciones más recientes, útil si has hecho clic demasiado rápido.
* **Guardar partida/Cargar partida/Menú principal** (`Save Game/Load Game/Main Menu`) - _"Ya no tiene sentido guardar. No te preocupes, no me voy a ninguna parte."_
* **Submods** - Muestra los submods instalados actualmente y qué versión de cada uno estás usando.
* **Alertas** (`Alerts`) - Contiene ajustes para reacciones de ventana (ver abajo) y alertas de temas. Puedes elegir un sonido único para ellas.
* **Atajos de teclado** (`Hotkeys`) - Guía de atajos de teclado dentro del juego.
* **Ayuda** (`Help`) - Enlaces a la página de ayuda de DDLC de Team Salvato.
* **Salir** (`Quit`) - _De verdad deberías asegurarte de despedirte, ya sabes..._

* **Amanecer/Atardecer** (`Sunrise/Sunset`) - Configura las horas del ciclo día/noche dentro del juego.
* **Velocidad del texto** (`Text Speed`) - Ajusta la velocidad de escritura del diálogo de Monika. (Puede requerir desbloqueo.)
* **Tiempo de avance automático** (`Auto-Forward Time`) - Ajusta la velocidad a la que avanzan los cuadros de texto cuando usas la función Auto.
* **Charla aleatoria** (`Random Chatter`) - Ajusta la frecuencia con la que Monika sacará temas aleatorios.
* **Volumen ambiente** (`Ambient Volume`) - Controla el volumen de los sonidos ambientales de la habitación, como la lluvia.
* **Volumen de música** (`Music Volume`) - Controla el volumen de la música, incluyendo cuando Monika toca el piano para ti.
* **Volumen de sonido** (`Sound Volume`) - Controla los sonidos de la interfaz.

[arriba](./All-Features-[SPOILERS].md#intro)
<a id="window-reactions"></a>
# Reacciones de ventana

Esta función permite que Monika detecte tu ventana activa actual y haga comentarios y bromas sobre lo que ve.

**Lista actual de reacciones:** _(Exacta según la versión v0.11.2)_

* 4chan
* DeviantArt
* Duolingo
* Monika After Story Github
* MyAnimeList
* Netflix
* Pinterest
* Pixiv
* Reddit
* Rule 34 (al buscar a Monika)
* Twitch.tv
* Twitter (reacciones separadas para Twitter en general y para el suyo propio)
* Wikipedia
