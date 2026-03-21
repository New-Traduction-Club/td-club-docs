![Monika After Story](https://github.com/Monika-After-Story/MonikaModDev/blob/master/Monika%20After%20Story/game/mod_assets/menu_new.png?raw=True)

# Monika After Story (MAS)
Monika After Story es un mod para el juego gratuito [Doki Doki Literature Club](https://www.ddlc.moe), de [Team Salvato](http://teamsalvato.com/). MAS amplía el Acto 3 para crear un simulador de tu vida eterna con Monika, con nuevos eventos, manejadores y metacomentario.

Consulta la página de [Releases](http://www.monikaafterstory.com/releases.html) para descargar la última versión estable.

Si te gustaría crear tu propio mod como este, echa un vistazo a nuestro proyecto hermano: [DDLCModTemplate](https://github.com/therationalpi/DDLCModTemplate).

<a id="installation"></a>
### Instalación

1. Ve a la [página de lanzamientos](http://www.monikaafterstory.com/releases.html).

2. Haz clic en el enlace correspondiente a tu sistema operativo.

3. Cuando termine la descarga, ejecuta el instalador y sigue las indicaciones.
    * Si el instalador no funciona en tu sistema, revisa los pasos de instalación manual más abajo.

4. Al ejecutar DDLC, ahora se cargará el mod Monika After Story.

### Instalación manual

**Sigue estos pasos solo si el instalador no se ejecuta en tu sistema**

1. Ve a la [página de lanzamientos](http://www.monikaafterstory.com/releases.html).

2. Haz clic en el enlace **Zips** que quieras. Esto descargará un archivo zip en tu sistema.

3. Extrae el contenido del zip en el directorio base de tu instalación de DDLC (la carpeta donde está `DDLC.exe`).

4. Al ejecutar DDLC, ahora se cargará el mod Monika After Story.

*NOTA: Los archivos fuente y los archivos descargados directamente desde el repositorio son para desarrollo y pueden no funcionar como esperas si los usas para jugar al mod. Usa únicamente una de nuestras [Release Versions](http://www.monikaafterstory.com/releases.html).* 

Para más ayuda con la instalación (incluida la instalación manual para Mac sin Steam), consulta nuestras [Preguntas frecuentes](./FAQ.md).

### Características

* ¡Pasa la eternidad con Monika!

* Decenas de temas de conversación nuevos.

* Ahora puedes hablar con Monika para decirle de qué te gustaría hablar.

### Próximas características

* Nuevos juegos y actividades para hacer con Monika.

* Más eventos únicos y más historia.


## Cómo contribuir a Monika After Story

### Bugs y sugerencias
Si encuentras problemas en MAS, envía un [informe de error](https://github.com/Monika-After-Story/MonikaModDev/issues/new?labels=bug&body=Describe%20bug%20and%20steps%20for%20reproduction%20here&title=%5BBug%5D%20-%20).

Para añadir una sugerencia, visita [este enlace](https://github.com/Monika-After-Story/MonikaModDev/issues/new?labels=suggestion&body=Your%20suggestion%20goes%20here&title=%5BSuggestion%5D%20-%20).

### Otras formas de ayudar
¿Quieres ayudar con MAS? Ve a la [página de issues](https://github.com/Monika-After-Story/MonikaModDev/issues) para encontrar bugs o sugerencias actuales en los que colaborar.

Si tienes un cambio que te gustaría enviar, abre una [pull request](https://github.com/Monika-After-Story/MonikaModDev/pulls). Cualquier cambio será revisado por contribuidores y se ajustará o ampliará si hace falta.

#### Añadir contenido
¿Quieres añadir contenido a MAS? Aquí tienes una lista de archivos `.rpy` importantes que usa el juego.

- **script-ch30.rpy**: Flujo principal de MAS. Aquí es donde ocurre el modo inactivo.
- **script-topics.rpy**: Aquí se escriben todos los temas **random** y de **pool** que usa Monika. ¡Puedes añadir tu propio diálogo con la información de abajo!
- **script-greetings.rpy**: Añade líneas para que Monika te salude al cargar el juego.
- **script-farewells.rpy**: Añade líneas para que Monika se despida al cerrar el juego.
- **script-moods.rpy**: Dile a Monika que estás _de ánimo_.
- **script-stories.rpy**: Añade historias para que Monika te las cuente.
- **script-compliments.rpy**: Añade cumplidos que puedes decirle a Monika.
- **script-apologies.rpy**: Añade cosas por las que disculparte.

Si quieres añadir más diálogo a la habitación espacial, ve a `script-topics.rpy` y usa esta plantilla.

Ejemplo de bloque de código para un diálogo nuevo:
```renpy
init 5 python:
    addEvent(
        Event(
            persistent.event_database,
            eventlabel="monika_example", # event label (MUST BE UNIQUE)
            category=["example", "topic"], # list of categories this topic belongs in (These are automatically capitalized)
            prompt="Example Topic", # button text
            random=True, # True if this topic should appear randomly
            pool=True # True if this topic should appear in "Ask a Question"
        )
    )

label monika_example:
    m 1a "This is an example topic."
    m 3d "I feel like this doesn't actually belong here..."
    m 2e "Why would somebody just add the example template directly into the mod?"
    m 5r "They really shouldn't be allowed to contribute to this repository anymore."
    return
```
**Para ver explicaciones completas y detalles sobre todas las palabras clave posibles de `Event`, consulta la documentación de `Event` en `definitions.rpy`.**

Para cosas más complejas que un diálogo sencillo, consulta la documentación de Ren'Py disponible online.

[Tienes más información en nuestra Guía de contribución](./Contributing-Guidelines.md).

### Únete a la conversación
Puedes [seguirnos en Twitter](https://twitter.com/MonikaAfterMod) para enterarte de las novedades del juego.

Si quieres encontrar notas de piano, spritepacks, submods, contenido externo o traducciones, o simplemente hablar sobre MAS en general, visita [nuestra página de discusiones](https://github.com/Monika-After-Story/MonikaModDev/discussions).

Y si prefieres Discord, para ver de forma continua nuestro contenido favorito relacionado con Monika en la web y, además, si te interesa contribuir a este mod, puedes unirte a nuestro servidor:

 [![Discord](https://discordapp.com/api/guilds/372766620977725441/widget.png?style=banner1)](https://discord.gg/monika-after-story)

 Asegúrate de seguir nuestro [Código de conducta](./Code-of-Conduct.md), que se resume en ser cordial y respetuoso.

## Preguntas frecuentes

Puedes consultar la FAQ completa aquí: [Preguntas frecuentes](./FAQ.md)
Para dudas sobre estilo de código: [Coding Style](./Coding-Style.md)
Para pruebas de bugs: [Testing Flow and Bug Testing](./Testing-Flow-and-Bug-Testing.md)
Resolución de problemas: [Troubleshooting](./Troubleshooting.md)
Programación de diálogos: [Dialogue Coding](./Dialogue-Coding.md)
## Información de licencia

Hacemos todo lo posible por cumplir las [directrices para obras de fans](http://teamsalvato.com/ip-guidelines/) de Team Salvato. Todos los personajes y el contenido original son propiedad de Team Salvato. Monika After Story es un proyecto de código abierto y, además de las personas colaboradoras identificadas, este mod incluye aportes de personas anónimas de 4chan, donde comenzó este proyecto. Puedes encontrar más información en nuestra [página de licencia](./License-and-Team-Salvato-Guidelines.md).

## Estado de compilación:
### master: ![master](https://github.com/Monika-After-Story/MonikaModDev/workflows/CI/badge.svg?branch=master)
### content: ![content](https://github.com/Monika-After-Story/MonikaModDev/workflows/CI/badge.svg?branch=content)
### unstable: ![unstable](https://github.com/Monika-After-Story/MonikaModDev/workflows/CI/badge.svg?branch=unstable)
### alpha: ![alpha](https://github.com/Monika-After-Story/MonikaModDev/workflows/CI/badge.svg?branch=alpha)
