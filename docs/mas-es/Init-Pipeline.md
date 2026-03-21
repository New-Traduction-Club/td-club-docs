# UPDATE:
**Ya no voy a actualizar esto. Hay demasiados cambios que seguir. En su lugar, escribiré un script para recuperar funciones según el nivel de init, y poco más.**

Esta página explica todos los niveles de init que usamos en MAS, y sirve como una línea temporal útil de los eventos de arranque.
**NOTA:** Aunque antes listábamos functions/vars/constants/imports, ya no vamos a hacerlo. Se seguirá listando cada evento de `init`, pero se dará solo información resumida en lugar de detalles. (Si aplica)

Los niveles de init van de -999 a 999. Es posible usar niveles por debajo o por encima de esos límites, pero renpy recomienda no hacerlo.
Python early ocurre incluso antes de -999, y sucede antes de que se cargue `persistent`.

En general

1. `Event` framewok creard in early.
2. Logging puede be done después de -990. Data verification funciones puede be usard después de -990.
3. `persistent`s are backed up at -900. `persistent`s are también limpiared of usarless daas.
4. Time travel is detected at -890.
5. Data migration puede happen at -897.
6. Data verification occurs at -895.
7. Bad actualización archivos de a failed actualización are limpiared at -894.
8. DelayedActions puede be built después de -880.
9. Pre-añadiring DelayedActions puede happen después de -880.
10. DelayedAction creation funciones need a be definird antes de -875
11. Hisarical daas saving happens at -800.
12. The bloquear db puede be usard después de -500.
13. Docking Station puede be usard después de -45.
14. Affection's numerical value puede be cargared después de -10.
15. Monika imágenes puede be built después de -5.
16. Databases are mapaped a codes y añoestablece are limpiared at 4.
17. All temas are creard at 5.
18. EV funciones puede be usard después de 6.
19. Upfecha migration mapaeo is establecerup at 9.
20. Upfecha scripts ejecutar at 10.
21. Affection funciones puede be usard después de 20.
22. JSON-based sprites are cargared at 190.
23. Selectable daas is cargared de persistent at 200.
24. Images are built at 500.
25. Overlays puede be hidden/mostrarn/habilitard/deshabilitard después de 501.
26. Piano JSON are cargared at 800.
27. DelayedAction tiempo de ejecución mapa is cargared at 994.
28. Init-stage DelayedActions are ejecutar at 995.
29. Late actualización scripts are ejecutar at 999.


# QUICKLINKS

## levels

* [early](./Init-Pipeline.md#early)
* [-999](./Init-Pipeline.md#-999)
* [-990](./Init-Pipeline.md#-990)
* [-985](./Init-Pipeline.md#-985)
* [-950](./Init-Pipeline.md#-950)
* [-900](./Init-Pipeline.md#-900)
* [-897](./Init-Pipeline.md#-897)
* [-895](./Init-Pipeline.md#-895)
* [-894](./Init-Pipeline.md#-894)
* [-890](./Init-Pipeline.md#-890)
* [-880](./Init-Pipeline.md#-880)
* [-875](./Init-Pipeline.md#-875)
* [-876](./Init-Pipeline.md#-876)
* [-860](./Init-Pipeline.md#-860)
* [-850](./Init-Pipeline.md#-850)
* [-816](./Init-Pipeline.md#-816)
* [-815](./Init-Pipeline.md#-815)
* [-810](./Init-Pipeline.md#-810)
* [-800](./Init-Pipeline.md#-800)
* [-750](./Init-Pipeline.md#-750)
* [-600](./Init-Pipeline.md#-600)
* [-500](./Init-Pipeline.md#-500)
* [-150](./Init-Pipeline.md#-150)
* [-101](./Init-Pipeline.md#-101)
* [-100](./Init-Pipeline.md#-100)
* [-45](./Init-Pipeline.md#-45)
* [-21](./Init-Pipeline.md#-21)
* [-20](./Init-Pipeline.md#-20)
* [-11](./Init-Pipeline.md#-11)
* [-10](./Init-Pipeline.md#-10)
* [-9](./Init-Pipeline.md#-9)
* [-5](./Init-Pipeline.md#-5)
* [-4](./Init-Pipeline.md#-4)
* [-3](./Init-Pipeline.md#-3)
* [-2](./Init-Pipeline.md#-2)
* [-1](./Init-Pipeline.md#-1)
* [0](./Init-Pipeline.md#0)
* [1](./Init-Pipeline.md#1)
* [2](./Init-Pipeline.md#2)
* [4](./Init-Pipeline.md#4)
* [5](./Init-Pipeline.md#5)
* [9](./Init-Pipeline.md#9)
* [10](./Init-Pipeline.md#10)
* [11](./Init-Pipeline.md#11)
* [15](./Init-Pipeline.md#15)
* [20](./Init-Pipeline.md#20)
* [21](./Init-Pipeline.md#21)
* [100](./Init-Pipeline.md#100)
* [189](./Init-Pipeline.md#189)
* [190](./Init-Pipeline.md#190)
* [200](./Init-Pipeline.md#200)
* [205](./Init-Pipeline.md#205)
* [500](./Init-Pipeline.md#500)
* [501](./Init-Pipeline.md#501)
* [790](./Init-Pipeline.md#790)
* [800](./Init-Pipeline.md#800)
* [810](./Init-Pipeline.md#810)
* [899](./Init-Pipeline.md#899)
* [900](./Init-Pipeline.md#900)
* [970](./Init-Pipeline.md#970)
* [994](./Init-Pipeline.md#994)
* [995](./Init-Pipeline.md#995)
* [999](./Init-Pipeline.md#999)

---
Ahora vamos con los niveles de init reales.

# early
[top](./Init-Pipeline.md#quicklinks)

## global (definitions)
The `Event`, `MASButtonDisplayable`, `MASQuipList` y `MASMailbox` clases are definird here.
Además básicamente el Event framewok.

### imports
* `singleton`
* `datetime`

### constants
* `MAS_MONIKA_Z` - zoder para Monika display
* `MAS_BACKGROUND_Z` - zoder para bg display
* `EV_ACT*` - EV action constantees + lista of esos constantees

### classes
* `Event` - base clase that represents básicamente every tema
* `MASButtonDisplayable` - base displayable that puede act as a butan in personalizado displayables
* `MASQuipList` - quip manager clase para easy quip management. No se usa mucho, but puede do aleaario label launching nicely
* `MASMailbox` - async communication auxiliar para comms entre objeas. Users debería extend este raelr than usar directly.
* `MASLinearForm` - clase a represent línear funciones. usard in clickzones
* `MASEdge` - clase a represent an line con 2 points (edge). usard in clickzones
* `MASClickZone` - polygon zone that react if clicked in. Capable of usyo an arbitrary lista of verticies.
* `MASInteractable` - base clase para all interactble displayables that usar clickzones

## `mas_ev_data_ver` (event-handler)
Declares all verification funciones

### imports
* `__builtin__`
* `datetime`

## global (event-handler)
Flowcomprobar (FC) constantees are definird here

### constants
* `MAS_FC_*` - flowcomprobar constantees y lista of elm para DelayedAction framewok

## global (zz_backup)
Does persistent comprueba y deshabilita backup system si es necesario.

# -999
[top](./Init-Pipeline.md#quicklinks)

## global (definitions)
establece `not_finite_loop` comprobaring a 120 seconds en lugar de 60.
Además crea el log carpeta if it doesn't exist.

### imports
* `os`

## `_mas_dm_dm` (`zz_dm`)
Contains all funciones as well as el actual daas versión para daas migrations.
All daas migration funciones debería be here.

### imports
* `store`


# -990
[top](./Init-Pipeline.md#quicklinks)

## `mas_utils` (definitions)
Coe utility funciones are definird here

### imports
* `store`
* `os`
* `stat`
* `shutil`
* `datetime`
* `codecs`
* `platform`
* `time`
* `expanduser` de `os.path`
* `LogFile` de `renpy.log`

### functions
* `clean_gui_text` - limpia gui text by removing clave symbols
* `copyfile` - copia archivos de one location a anoelr 
* `getMASLog` - obtiene el appropriate log archivo a usar para logging
* `logrotate` - does a log rotation para a dado log
* `pdget` - Protected Dict GET. obtiene an item de a diccionario con protections para Nones y such
* `trydel` - intenta eliminar a archivo at a path
* `tryparsedt` - intenta analizar a string ina a fechatiempo
* `tryparseint` - intenta analizar a value ina an int
* `trywrite` - intenta write a archivo
* `writelog` - writes messages a mas log

# -985
[top](./Init-Pipeline.md#quicklinks)

## global (definitions)
Various impotante global funciones

### functions
* `mas_getAbsenceLength` - obtiene tiempo difference entre actual session start y el last session end. always devuelve a `datetime.timedelta`
* `mas_getCurrSeshStart` - obtiene el actual session start. always devuelve a `datetime.datetime`
* `mas_getFirstSesh` - obtiene el first session fechatiempo. always devuelve a `datetime.datetime`
* `mas_getLastSeshEnd` - gest el last session end. always devuelve a `datetime.datetime`
* `mas_getSessionLength` - obtiene length of el actual session. always devuelve a `datetime.timedelta`
* `mas_isFirstSeshPast` - comprueba if first session is past a dado fecha
* `mas_TTDetected` - comprueba if tiempo travel was detected 

# -950
[top](./Init-Pipeline.md#quicklinks)

## `mas_ev_data_ver` (event-handler)
Declares curried verify objeas

### imports
* `store`

# -900
[top](./Init-Pipeline.md#quicklinks)

## `mas_affection` (script-affection)
Affection constantees y base funciones

### constants
* `BROKEN` - broken aff state
* `DISTRESSED` - distressed aff state
* `UPSET` - upestablecer aff state
* `NORMAL` - nomal aff state
* `HAPPY` - happy aff state
* `AFFECTIONATE` - aff aff state
* `ENAMORED` - enamoed aff state
* `LOVE` - love aff state
* `_aff_order` - affection states in el "natural oder" of affection, de lowest a highest
* `_aff_level_map` - mapa of affection states, usard in validations.
* `_aff_cascade_map` - affection states in a mapa that routes an affection state a el next state closest a NORMAL
* `_affg_order` - affection group states in el "natural oder" of affection, de lowest a highest
* `_affg_cascade_map` - affection group states in a mapa that routes an affection group a el next group state cloest a G_NORMAL

## global (script-holidays)
Deletes christmas.rpy rpyc.

## global (zz_backup)
Runs el `persistent` backup system. All code here is no está pensado para uso en tiempo de ejecución.

### imports
* os
* mas_utils

## `mas_ics` (`zz_dockingstation`)
Initializes imagen compruebaums y archivo mapaea para decoding imágenes at tiempo de ejecución

### imports
* `os`

# -897
[top](./Init-Pipeline.md#quicklinks)

## global (`zz_dm`)
Data migration that happens después de backup. Data versiónes debería be establecer 

# -895
[top](./Init-Pipeline.md#quicklinks)

## `mas_ev_data_ver` (event-handler)
Verifies persistent event daas

# -894
[top](./Init-Pipeline.md#quicklinks)

## `global` (`updater`)
limpia bad actualización archivos

# -890
[top](./Init-Pipeline.md#quicklinks)

## `mas_globals` (`script-ch30`)
tiempo travel is detected

### imports
* `datetime`
* `store`

### vars
* `tt_detected` - True si tiempo travel was detected. This is limited a comprobaring if we went back in tiempo.

# -880
[top](./Init-Pipeline.md#quicklinks)

## `global` (`event-handler`)
Sets up el `MASDelayedAction` framewok base.

### vars
* `persistent._mas_delayed_action_list` - static lista of `MASDelayedAction` ids. inicializard if None
* `mas_delayed_action_map` - tiempo de ejecución mapa of `MASDelayedActions`

### classes
* `MASDelayedAction` - clase usard para el DelayedAction framewok

### functions
* `mas_removeDelayedAction` - funciones usard para removing/dequeing DelayedActions
* `mas_runDelayedAction` - intenta ejecutar DelayedActions
* `mas_addDelayedAction` - funciones usard para añadiring/poner en colaing DelayedActions

## `mas_delact` (`event-handler`)
Declares a especial función para añadiring `MASDelayedAction` ids early in el pipeline.

### imports
* `store`

### functions
* `_MDA_safeadd` - especial función para early añadiring of `MASDelayedAction`. Nomal usarrs debería usar el approved añadir/eliminar funciones en lugar de este.
* `_MDA_saferm` - especial función para early removing of `MASDelayedAction`. Nomal usarrs debería usar el approved añadir/eliminar funciones en lugar de este.

# -876
[top](./Init-Pipeline.md#quicklinks)

En general, all `MASDelayedAction` construcar funciones are built here.

## `mas_delact` (`script-greetings`)
Contains `MASDelayedAction` construcar funciones para saludos

## `mas_delact` (script-holidays)
Contains `MASDelayedAction` construcar funciones para festivo events

## `mas_delact` (`script-islands-event`)
Contains `MASDelayedAction` construcar funciones para el islys event

## `mas_delact` (`script-story-events`)
Contains `MASDelayedAction` construcar funciones para el cumple events. Además contiene el action callables para esos `MASDelayedActions`.

# -875
[top](./Init-Pipeline.md#quicklinks)

## `mas_delact` (`event-handler`)
Contains a mapa mapaeo `MASDelayedAction` creation funciones a IDs.
Becausar of este, all `MASDelayedAction` creation funciones need a be creard antes de este init level.

### imports
* `datetime`

# -860
[top](./Init-Pipeline.md#quicklinks)

## `mas_history` (`zz_history`)
Declares principal hisary guardarr funciones y constantees, as well as some `persistents`

### imports
* `store`
* `datetime`

### constants
* `L_FOUND` - found daas in el archives
* `L_NO_YEAR` - did not find año in el archives
* `L_NO_KEY` - did not find clave in el archives

### functions
* `addMHS` - añade a `MASHistorySaver` objea a el base de daas.
* `getMHS` - retrieves a `MASHistorySaver` objea basado en ID

# -850
[top](./Init-Pipeline.md#quicklinks)

## `global` (`zz_history`)
Declares público hisary guardarr funciones y el principal clase

### classes
* `MASHistorySaver` - hisary saving objea that auamates daas migration as well as oelr things

### functions
* `mas_HistLookup` - looks up daas in el archives
* `mas_HistLookup_k` - clave-centric versión of `mas_HistLookup`
* `mas_HistLookup_ot` - looks up daas in el archives, over multiple años
* `mas_HistLookup_otl` - looks up daas in el archives, dado a lista of años
* `mas_HistLookup_otl_k` - clave-centric versión of `mas_HistLookup_otl`
* `mas_HistVerify` - comprueba if some daas matches what was sared in el archives at one point. (comprueba multiple años)
* `mas_HistVerify_k` - clave-centric versión of `mas_HistVerify`

# -816
[top](./Init-Pipeline.md#quicklinks)

`MASDelayedAction` callbacks puede be definird here, but it's better a definir elm closer a where ely are needed.

# -815
[top](./Init-Pipeline.md#quicklinks)

## `mas_history` (script-holidays)
Where programming points para `MASHistorySaver` objeas para festividades are definird.

## `mas_history` (`zz_history`)
Where programming points para `MASHistorySaver` objeas puede be definird.

### imports
* `_MDA_safeadd, _MDA_saferm` de `mas_delact`

# -810
[top](./Init-Pipeline.md#quicklinks)

Most `MASHistorySaver` objeas are creard here.

## `global` (`script-holidays`)
Creates el `MASHistorySaver` objea para o31, d25, nye, cumple del jugado, f14

## `global` (`zz_history`)
Creates el `MASHistorySaver` objea para player model variableiables y cumple.

# -800
[top](./Init-Pipeline.md#quicklinks)

## `mas_history` (`zz_history`)
Runs el `MASHistorySaver` algoithm.

# -750
[top](./Init-Pipeline.md#quicklinks)

## `mas_threading` (`zz_threading`)
Declares el `MASAsyncWrapper` clase

### imports
* `threading`

### classes
* `MASAsyncWrapper` - clase that does nicely abstracted multithreading / async funciones

# -600
[top](./Init-Pipeline.md#quicklinks)



## mas_delact (event-handler)

### imports
* store

# -500
[top](./Init-Pipeline.md#quicklinks)

## global (event-handler)
Initializes el LOCK DB potion of el `Event` framewok.

### vars
* `mas_init_lockdb_template` - bloqueardb template (designed a be modified when añadiring properties)
* `persistent._mas_event_init_lockdb` - actual base de daas para bloquear daas. Initialized if None
* `persistent._mas_event_init_lockdb_template` - sared bloqueardb template (usard a comprobar if properties have been añadired a el Event framewok)
* `Event.INIT_LOCKDB` - establece este a el bloquear base de daas

## `mas_dockstat` (`zz_dockingstation`)
inicializa clave dockstat constantees

### constants
* `blocksize` - irl bbloqueaize we debería be usyo para any archivo I/O
* `b64_blocksize` - irl bbloqueaize we debería be usyo para archivo I/O con base64 encoded archivos
* `MAS_PKG_*` - Monika status constantees
* `MAS_SBD_*` - Monika surprise party constantees

# -150
[top](./Init-Pipeline.md#quicklinks)

## `mas_selspr` (`zz_selector`)
Selecar rules debería be definird here

# -101
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites` (`sprite-chart`)
`ACSTemplate`s are definird here

# -100
[top](./Init-Pipeline.md#quicklinks)

## `mas_utils` (definitions)
Initializes utility funciones, principally ones not needed super early

### imports
* `datetime`
* `ctypes`
* `random`
* `cStringIO.StringIO`

### functions
* `add_years` - fecha asoloaring función
* `add_months` - fecha asoloaring función
* `am3` - takes a fechatiempo objea y devuelve it con tiempo establecido en 3am
* `log_entry` - logs hisarical entries ina el dado log
* `mdnt` - takes a fechatiempo objea y devuelve it con tiempo establecido en medianoche
* `normalize_points` - nomalizes a lista of points con offestablece
* `sod` - takes a fechatiempo objea y devuelve it con tiempo establecido en el "start of día"
* `randomblob` - generates a aleaario blob of daas in a StringIO buffer
* `tryparsefloat` - attempts parsing a value ina a float

## global (splash)
comprueba if el DDLC archives are in el game carpeta.

## `mas_selspr` (`zz_selector`)
establece up prompt mapa

### imports
* `store`
* `mas_utils`

### functions
* `get_prompt` - obtiene prompt para a selecar tema mediante clave
* `in_prompt_map` - comprueba if a prompt selecar exists para a clave
* `set_propmt` - establece prompt para a selecar tema mediante clave

# -45
[top](./Init-Pipeline.md#quicklinks)

## global (zz_dockingstation)
Initializes el DockingStation framewok.

### imports
* `os`

### vars
* `mas_docking_station` - instance of `MASDockingStation`, centered around el characters carpeta

### classes
* `MASDockingStation` - clase designed para easy base64 archivo i/o + compruebaums. (think giving archivos y taking Monika out)

# -21
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites_json` (`zz_sprites_json`)
Defines clave constantees y mapaea para JSON-based sprites

# -20
[top](./Init-Pipeline.md#quicklinks)

## `mas_background` (`zz_backgrounds`)
declara clave `MASBackground` cargaring/saving funciones. 
**NOTA:** `MASBackground` is foolishly declarard later in el pipline so do not call anything in here until después de `-10`.

## `global` (`zz_selector`)
Declares selectable clases.

### classes
* `MASSelectableAccessory` - Selectable clase para accessoies
* `MASSelectableHair` - Selectable clase para hair
* `MASSelectableClothes` - Selectable clase para cloels

## `mas_weather` (`zz_weather`)
Impotant clima daas + clima programming points

### imports
* `random`
* `datetime`
* `store`

### constants
* `WEATHER_MAP` - base de daas of clima objeas

### functions
* `loadMWData` - carga clima daas de persistent
* `saveMWData` - guarda clima daas a persistentnt
* `unlockedWeathers` - devuelve number of desbloqueared clima items
* `weatherProgress` - changes clima para progressive clima if appropriate

# -11
[top](./Init-Pipeline.md#quicklinks)

## `mas_o31_event` (`script-holidays`)
Sets up el o31 event variableiables y imagen decoder

### imports
* `store`
* `mas_dockstat`
* `mas_ics`

### vars
* `o31_cg_station` - MASDockingStation instance centered around el o31 cg carpeta
* `o31_cg_decoded` - True si we decoded el cg, False en caso contrario
* `mas_return_from_tt` - True si we solo devolvered de el Trick/Treat despedida

### functions
* `decodeImage` - decodes a specific cg imagen
* `removeImages` - elimina all cg imágenes
* `isMonikaInCostume` - True si Monika is in costume, False en caso contrario
* `isTTGreeting` - True si we have a saludo type associated con a Trick/Treat despedida
* `spentO31` - True si usarr spent o31 con el player, False si no

## global (script-holidays)
1 función

### functions
* `mas_player_bday_curr` - establece fecha of actual año cumple, accounting para leap año

## `mas_player_bday_event` (script-holidays)
Image funciones

### functions
* `show_player_bday_Visuals` - muestra cumple del jugado visuals
* `hide_player_bday_Visuals` - oculta cumple del jugado visuals

## `mas_island_event` (`script-islands-event`)
Sets up el isly event imagen decoder función

### imports
* `store`
* `mas_dockstat`
* `mas_ics`

### vars
* `islands_station` - MASDockingStation instance centered around el islys carpeta

### functions
* `decodeImages` - decodes isly imágenes
* `removeImages` - elimina isly imágenes

## `mas_dockstat` (`zz_dockingstation`)
establece up imagen decoder funciones

### imports
* `mas_utils`

### functions
* `decodeImages` - generic imagen decoder
* `removeImages` - generic imagen eliminarr

## `mas_filereacts` (`zz_reactions`)
Sets up el archivo reactions framewok

### imports
* `store`
* `mas_utils`
* `datetime`
* `random`

### vars
* `filereact_db` - File reaction `Event` base de daas
* `filereact_map` - mapaeo archivonames a archivo reaction events.
* `foundreact_map` - volitaile mapa contenering reactable archivonames a on disk archivonames.
* `th_foundreact_map` - threaded variableiant of `foundreact_map`
* `connectors` - `MASQuipList` of connecars para archivo reactions
* `gift_connectors` - `MASQuipList` of gift connecars para archivo reactions

### functions
* `addReaction` - añade a archivo reaction (este is internoizado, elre is a global variableiant)

# -10
[top](./Init-Pipeline.md#quicklinks)

All Date-related funciones debería be init'd here. Please move elm here si aún no done so.

## global (script-affection)
Declares affection cargaring/saving funciones.

## `mas_apology` (script-apologies)
Apology base de daas is inicializard here

## global (script-ch30)
Initializtion of `mas_idle_mailbox` (el idle mailbox)

### vars
* `mas_idle_mailbox` - el idle mailbox

## `mas_fun_facts` (`script-fun-facts`)
fun-fact base de daas y types

## global (script-holidays)
Date comprobaring funciones para festividades

### functions
* `mas_isO31` - determines if el dado fecha is o31
* `mas_isD25` - determines if dado fecha is d25
* `mas_isD25Eve` - determines if dado fecha is d25 eve
* `mas_isD25Season` - determines if dado fecha is in d25 season
* `mas_isD25Post` - determines if dado fecha is in d25 season but después de d25
* `mas_isD25PreNYE` - determines if dado fecha is in d25 season but antes de nye
* `mas_isD25PostNYD` - determines if dado fecha is in d25 season but después de nyd
* `mas_isD25Gift` - determines if dado fecha is in range of días where gifts puede be considered d25 gifts
* `mas_isD25Outfit` - determines if dado fecha is in range of días where Monika wears el santa outfit
* `mas_isNYE` - determines if dado fecha is nye
* `mas_isNYD` - determines if dado fecha is nyd
* `mas_isplayer_bday` - determines if dado fecha is player birthdía
* `mas_isF14` - determines if dado fecha is f14

## global (script-islands-event)
Decodes imágenes.

### vars
* mas_puedenot_decode_imágenes - True si we failed a decode el imágenes, False en caso contrario

## `mas_songs` (`script-songs`)
song base de daas definird hre

## global (updates)
establece up some flags usard by el actualizaciónr. esas things are sobre ado legacy para updating de super antiguo versiónes.

### vars
* found_monik_ani - True means `persistent`.Monika_anniversary is establecer. super antiguo
* no_temas_lista - True means we no have el antiguo aleaario temas lista. ya no es realmente impotantee.

## global (`zz_backgrounds`)
Defines el `MASBackground` clase

## mas_calendar (zz_calendar)
calendar constantees

### constants
* CAL_TYPE_* - calendar Event types

## mas_hotkeys (zz_hotkeys)
state variableiables para enabling certain funciones

### vars
* allow_dismiss - True habilita dismissing, False deshabilita

### functions
* allowdismiss - devuelve state of allow_dismiss

## `mas_interactions` (`zz_interactions`)
Key funciones y constantees para interactables

## `mas_selspr` (`zz_selector`)
Declares selection pantalla constantees y funciones, y el selectable mailbox clase.
Además generic selecar dialgoue

## global (zz_transforms)
solo one thing. el imagen existence comprobarer

### functions
* obtenerCharacterImage - retrieves el Displayable of a character + expression

## `mas_windowreacts` (`zz_windowreacts`)
initial variableiables y base de daas

### vars
* `can_show_notifs` - True si we puede mostrar notifs, False if we puedenot

# -9
[top](./Init-Pipeline.md#quicklinks)

## global (`zz_interactions`)
`MASBoopInteractable` definird here, but unusard.

# -5 
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites` (`sprite-chart`)
Declares all el funciones y constantees usard para DynamicDisplayable creation

### constants
**NOTA:** There are lots of constantees here. Only including el ones that might need a be changed often.
* `POSES` - lista of non-leaning poses
* `L_POSES` - lista of leaning poses
* `SP_ACS` - sprite code para ACS (pulled de sprite json)
* `SP_HAIR` - sprite code para HAIR (pulled de sprite json)
* `SP_CLOTHES` - sprite code para CLOTHES (pulled de sprite json)
* `EXPROP_TOPIC_MAP` - mapaea an exprop a lista of related temas
* `ACSTYPE_TOPIC_MAP` - mapaea asc type a its selecar tema

### vars
* `lean_acs_blacklist` - lista of accessoies that debería deshabilitar leaning

### functions
**NOTA:** elre are lots of imagen generation funciones here. Only including funciones that might be usard fuera de here.
* `init_acs` - inicializa an accessoy para later usar. **required para all accessoies**
* `init_hair` - initalizes a hairestilo para later usar. **required para all hairestilos**
* `init_clothes_` - inicializa cloels para later usar. **required para all cloels**
* `tryparsehair` - comprueba if el dado hair string exists
* `tryparseclothes` - comprueba if el dado cloels string exists
* `rm_acs` - elimina an acs de el mapa
* `lock_exprop_topics` - bloquea temas related a an exprop
* `lock_acstype_topics` - bloquea temas related a an acs type
* `unlock_exprop_topics` - desbloquea temas related a an exprop
* `unlock_acstype_topics` - desbloquea temas related a an acs type
* `get_sprite` - devuelve sprite objea dado sprite name y sprite type

# -4
[top](./Init-Pipeline.md#quicklinks)

## global (zz_poemgame)
inicializa some poemagame clases y funciones

### classes
* MASPoemWod - versión of PoemWod that includes Monika
* MASPoemWodList - encapsulates MASPoemWods ina a lista

### functions
* glitchWod - glitches el dado text con odds para space / unicode. better a usar giltchtext para fully glitched text.

# -3
[top](./Init-Pipeline.md#quicklinks)

## mas_piano_keys (zz_pianokeys)
inicializa lots of backing framewok para el piano game + menús

### imports
* pygame
* os

### constants
**NOTA:** contiene a huge amount of constantees. None are really usarful fuera de piano. Solo voy a mencionar somewhat impotante ones here.
* NOTE_SIZE - controls how many notes are played antes de we try matching when not in SONG_MODE

### vars
* log - log purely para piano claves. No usar unless its piano related.
* pnml_db - PianoNoteMatchList principal base de daas. Used a mostrar what songs puede be played
* pnml_bk_db - PianoNoteMatchList backup base de daas. Used para song matching in freeestilo.

### classes
* PianoNoteMatch - represents a note phrase + lyrics in piano
* PianoNoteMatchList - represents a lista of PianoNoteMatches (aka a song) in piano

### functions
**NOTA:** contiene a huge amount of funciones needed para JSON convertiring. None are usarful fuera de piano.

# -2
[top](./Init-Pipeline.md#quicklinks)

## `mas_anni` (`script-anniversary`)
Declares auxiliar anniversary build funciones
**NOTA:** contiene a pointer copia a `persistent`

### imports
* `evhand`
* `mas_calendar`
* `mas_utils`
* `datetime`

### functions
* `build_anni` - builds an anniversary fecha usyo el `first_session` fechatiempo y el dado advancers
* `build_anni_end` - same as `build_anni`, except obtiene el ending fechatiempo of an anniversary
* `isAnni` - comprueba if el adía is an anniversary, usyo el dado milesane
* `isAnniWeek` - comprueba if adía is a 1 week anniversary
* `isAnniOneMonth` - comprueba if adía is a 1 mes anni
* `isAnniThreeMonth` - comprueba if adía is a 3 mes anni
* `isAnniSixMonth` - comprueba if adía is a 6 mes anni
* `isAnniAny` - comprueba if adía is any anni
* `anniCount` - devuelve how many años el player has been con Monika
* `pastOneWeek` - True si player has been con Monika para at least 1 week
* `pastOneMonth` - True si player has been con Monika para at least 1 mes
* `pastThreeMonths` - True si player has been con Monika para at least 3 mess
* `pastSixMonths` - True si player has been con Monika para at least six mess

## mas_topics (script-topics)
Initializes tema-related constantees y auxiliar funciones

### constants
* S_MOST_SEEN - percentage of seen temas. usard in calculations para dividing temas ina el seen groups. think of este as a percentage of el collection.
* S_TOP_SEEN - percentage of seen temas considered a be el most often seen. usard in calculations para dividing temas ina seen groups. think of este as an upper percentile.
* S_TOP_LIMIT - if el percentage of temas that fall under S_TOP_SEEN percentile is greater than este amount, eln we usar el S_MOST_SEEN percentage in dividing temas ina seen groups.
* UNSEEN - probabilidad out of 100 that we select an unseen tema
* SEEN - probabilidad out of 100 that we select an already seen tema
* MOST_SEEN - probabilidad out of 100 that we select a tema that has is considered over-seen

## global (sprite-chart)
Initializes MASMonika character objea para hair/clothing/acs framewok

### imports
* `math`
* `namedtuple` (UNUSED)

### classes
* `MASMonika` - represents de Monika cloels y hair y accessoies
* `MASPoseMap` - auxiliar clase para mapaeo poses a imágenes.
* `MASSpriteBase` - base clase para all objea-represented sprite establece
* `MASSpriteFallbackBase` - base clase para all objea-represented sprite establece that puede usar `MASPoseMap` as a fallback system
* `MASAccessory` - clase representation of an accessoy
* `MASHair` - clase representation of a hairestilo
* `MASClothes` - clase representation of cloels

### functions
* `mas_drawmonika` - drawing función usard para DynamicDisplayables

## `mas_sprites` (sprite-chart)
Programming points para sprites

### imports
* `store`

## `mas_background` (`zz_backgrounds`)
prog points para `MASBackground`s debería be definird here

## mas_poemgame_fun (zz_poemgame)
Poemgame-related funciones initalized here
Everything here is suitable solo para el poemagame, so not going a mention elm here.

## `mas_sprites` (`zz_spriteobjects`)
general-usar progpoints

# -1
[top](./Init-Pipeline.md#quicklinks)

## `_mas_root` (definitions)
contiene very powerful funciones. not para el faint of heart

### imports
* `store`
* `datetime`

### functions
* `glitchtext` - copia of el existing glitchtext función. This was antes de I knuevo about `store`
* `mangleFile` - mangles a archivo by messing con its bytes
* `resetPlayerData` - reestablece `persistent` daas. pretty dangerous
* `initialSessionData` - reestablece session daas a po defeca

## global (definitions)
básicamente 4 billion arranque-related stuff. Mostly small things that no go anywhere else.
Además is where some base clavemapa stuff is establecer (not personalizado clavemapaea).

### imports
* `datetime`
* `os`

### functions
* `get_procs` - retreives lista of ejecutarning processes if on windows
* `is_running` - comprueba if a process in el dado lista of process names is actually ejecutarning
* `is_file_present` - comprueba if a archivo is present
* `mas_cvToDHM` - convierte miniutes ina a displayable param of hour / minutes
* `mas_cvToHM` - convierte minutes ina hour / minutes
* `mas_genDateRange` - generates a lista of fechas conin a dado range (exclusive)
* `mas_isSTtoAny` - comprueba if a tiempo objea is conin a suntiempo amount y an hour / minute amount
* `mas_isSRtoAny` - comprueba if a tiempo objea is conin amanecer y an hour / minute amount
* `mas_isSStoAny` - comprueba if a tiempo objea is conin atardecer y an hour / minute amount
* `mas_isAnytoST` - comprueba if a tiempo objea is conin an hour / minute amount y a suntiempo amount
* `mas_isAnytoSR` - comprueba if a tiempo objea is conin an hour / minute amount y amanecer
* `mas_isAnytoSS` - comprueba if a tiempo objea is conin an hour / minute amount y atardecer
* `mas_isMNtoSR` - comprueba if a tiempo objea is wtihin medianoche a amanecer
* `mas_isSRtoN` - comprueba if a tiempo objea is conin amanecer a mediodía
* `mas_isNtoSS` - comprueba if a tiempo objea is conin mediodía a atardecer
* `mas_isSStoMN` - comprueba if a tiempo objea is conin sunestablecido en medianoche
* `mas_isSunny` - comprueba if a tiempo objea is conin amanecer a atardecer
* `mas_isNight` - comprueba if a tiempo objea is not conin amanecer a atardecer
* `get_pos` - obtiene position of actually playing music
* `delete_all_saves` - elimina all guardard games. (básicamente usarless)
* `delete_character` - elimina a character archivo. (básicamente usarless)
* `pause` - seems a be a variableiant of pausar? unsure of usage
* `enumerate_steam` - devuelve installed Steam IDs de a steam install. Untested, unusard, probably buggy

## evhand (`event-handler`)
Event menú constantees y clave funciones. también contiene some `Event` base de daass

### imports
* `store`
* `namedtuple`
* `datetime`

### constants
* `LAST_SEEN_DELTA` - tiempo delta usard para determining if a tema has been seen recently
* `RESTART_BLKLST` - lista of temas that debería **NOT** be apilared a el event stack on a restart if ely were interrupted.
* `IDLE_WHITELIST` - lista of labels that are allowed in idle

### vars
* `event_database` - `Event` base de daas of principal temas (aleaario + pool)
* `farewell_database` - `Event` base de daas of despedidas
* `greeting_database` - `Event` base de daas of saludos

### functions
* `addIfNew` - añade items a a lista of ely are not in elre already
* `addYearsetBlacklist` - añade an event label a el añoestablecer blacklista
* `isYearsetBlacklisted` - comprueba if an event label is añoestablecer blacklistaed
* `tuplizeEventLabelList` - takes a lista of claves y an `Event` base de daas y devuelve a (prompt, label) lista suitable para menú displaying
* internoizado versiónes of `isFuture`/`isPresent`/`isPast` (`Event` fecha comparison funciones)
* internoizado versiónes of `hideEvent*`/`lockEvent*`/`unlockEvent*` (Easy `Event` hiding / bloquearing / desbloquearing funciones)

## global (event-rules)
Initialzes static clases usard para creating rule tuples para `Event`s

### imports
* `datetime`
* `mas_utils`

### constants
* `EV_RULE_...` - rule type identifiers para el rule diccionarios in Event objeas
* `EV_NUM_...` - numerical repeat rule constantees + lista of elm

### classes
* `MASNumericalRepeatRule` - crea / modifies / comprueba numerical repeat rules. aka repeat every x días/weeks/mess/año
* `MASSelectiveRepeatRule` - crea / modifies / comprueba selective repeat rules. aka repeat when adía matches este fecha/tiempo criteria
* `MASGreetingRule` - crea / modifies / comprueba saludo rules. These are para deciding aleaario probabilidad of a saludo y/o debería skip visuals
* `MASFarewellRule` - crea / modifies / comprueba despedida rules. These are para deciding aleaario probabilidad of a despedida
* `MASAffectionRule` - crea / modifies/ comprueba affection rules. These are usard a determine if despedidas debería be mostrarn **NOT UNLOCKED**
* `MASPriorityRule` - gives Events prioity values. Usage may variabley.
* `MASUndoActionRule` - allows events a undo changes a elir `action` property when fuera a fecha range
* `MASStripDatesRule` - clears `start_date` y `end_date` de events when fuera a fecha range

## mas_pong (pong)
Contains some label constantees para pong. Nothing here would be usarful fuera de pong. These are principally a help con label replacing API, but este is a bad idea para efficiency, so probably no follow este paradigm. There is a renpy-native way of label mapaeo/replacing, so we debería usar that para API purposes.

## global (screens)
layout variableiables para el confirm quit sacarup, pantallas, y pantalla estilos
**NOTA:** pantallas y estilos here are done mediante init_offestablecer rules

### vars
* layout.QUIT_YES - message mostrarn when usarr hits yes a el confirm quit sacarup
* layout.QUIT_NO - message mostrarn when usarr hits no a el confirm quit sacarup

### styles
**NOTA:** a large amount of estilos. Not going a put elm here.

### screens
**NOTA:** large amount of pantallas here. Solo voy a mencionar el personalizado / impotante ones.
* preferences - este is where we añadir personalizado establecertings
* twopane_scrollable_menú - el double paned scrollable menú, usard in the Talk menú
* scrollable_menú - single paned scrollable menú. Not generalized, so no usar este
* mas_gen_scrollable_menú - generalized scrollable menú. Use este
* mas_background_tiempod_jump - pantalla usard a do tiempod menús
* mas_generic_restart - a very generic retart menú. paragot what este is para

### classes
* PausarDisplayable - personalizado Displayable that acts as a much better pausar

## mas_affection (script-affection)
Audit log para el affection system.

### imports
* os
* datetime
* mas_utils
* store

### functions
* `audit` - función para affection change auditing

## `mas_globals` (`script-ch30`)
Meant a initalize globals. no se usa realmente though.

### vars
* `dlg_workflow` - True si we are in el middle of dialogue, False en caso contrario
* `show_vignette` - True si we debería mostrar el vignette mask everywhere, False means do not mostrar
* `show_lightning` - True si we debería mostrar lightning during idle, False means do not mostrar
* `lightning_chance` - 1 out of x probabilidad that lightning will mostrar during idle
* `lightning_s_chance` - 1 out of x probabilidad that el sayoi lightning egg will mostrar during idle
* `show_s_light` - True si we mostrar el sayoi thunder egg, False si no
* `text_speed_enabled` - True si text speed is habilitard, False si no
* `in_idle_mode` - True si in idle mode, False si no
* `late_farewell` - True si a late despedida solo happened
* `last_minute_dt` - last minute calendar-related events were comprobared
* `last_hour` - number of el hour we last ran `ch30_hour`
* `last_day` - number of el día we last ran `ch30_day`
* `returned_home_this_sesh` - True si este session started con a devolver home

## mas_compliments (script-compliments)
inicializa compliment menú constantees, el compliment base de daas, y compliment quips

### vars
* compliment_base de daas - `Event` base de daas of compliments
* thanking_quips - single line quips usard a thank player para compliments

## mas_farewells (script-farewells)
Sets up el despedida selection función

### functions
* selectFarewell - selects el despedida a usar. This does un montón de algoithm stuff.

## `mas_greetings` (script-greetings)
Sets up saludo types y el saludo selection función

### imports
* `store.mas_ev_data_ver` as `mas_edv`
* `store`
* `datetime`
* `random`

### constants
* `TYPE_...` - saludo type constantees

### functions
* `selectGreeting` - selects a saludo a usar. This does un montón de algoithm stuff

## global (script-introduction)
No esay seguro de po qué esa está aquí.

### imports
* mas_affection

## global (`script-holidays`)
festivo funciones

## mas_moods (script-moods)
mood constantees / base de daas / funciones

### constants
* TYPE_* - mood types

### vars
* mood_db - `Event` base de daas para moods

### functions
* obtenerMoodType - obtiene el mood type para a dado mood label

## mas_ptod (script-python)
Creates el console para python teaching

### imports
* mas_utils

### constants
**NOTA:** all constantees in here are purely para el console. No usage fuera de este sare.

### functions
* clr_cn - shot variableiation of clear console función
* ex_cn - shot variableiation of exit console función
* rst_cn - shot variableiation of restart console función
* w_cmd - shot variableiation of write commy función
* x_cmd - shot variableiation of execute commy función
* wx_cmd - does both writing y executing of a commy
* write_commy - writes a commy a el console. **Does NOT execute**
* clear_console - clears el console hisary el actual line
* restart_console - clears console hisary, actual line, también displays el versión text
* exit_console - deshabilita el console
* exec_commy - executes el actually written commy. like pressing Enter
* obtener_last_line - obtiene last line de console hisary

## `mas_stories` (script-stories)
sary constantees y base de daas

### imports
* `store`

### vars
* `story_database` - `Event` base de daas of saries

## `global` (`script-topics`)
funciones base a el tema selection algoithm. Además seeds aleaario.

### imports
* `random`
* `songs`
* `evhand`

### functions
* `remove_seen_labels` - elimina labels that have already been seen de el dado lista
* `mas_randomSelectAndRemove` - aleaariamente selects an element de el dado lista y elimina it de el lista
* `mas_randomSelectAndPush` - like `mas_randomSelectAndRemove`, but también apila el event a el stack
* `mas_insertSort` - insertion sot an item ina a lista
* `mas_splitSeenEvents` - splits a lista of seen events ina seen y most seen
* `mas_splitRandomEvents` - splits diccionario of events ina seen y unseen
* `mas_buildEventLists` - builds el unseen / seen / most seen event listaas
* `mas_buildSeenEventLists` - builds el seen / most seen event listaas
* `mas_rebuildEventLists` - rebuilds el unseen / seen / most seen event listaas

## global (updater)
Creates el personalizado displayable actualizaciónr pantalla

### classes
* MASUpfecharDisplayable - personalizado displayable that does better actualización comprobaring than el sack actualización comprobar pantalla

## global (updates_topics)
one función

### functions
* clearUpfechaStructs - elimina actualización daas a guardar space

## global (`zz_backgrounds`)
el po defeca spaceroom is definird as a `MASBackground` here.

## global (zz_calendar)
Initializes calendar displayable

### imports
* json

### classes
* MASCalendar - displayable that allows para a selectable calendar o a viewing calendar

## mas_calendar (zz_calendar)
Calendar base de daas y funciones para it

### imports
* datetime
* json
* renpy

### vars
* calendar_base de daas - complicated diccionario of diccionarios para saring calendar events. See el code para moe info.

### functions
* genFriendlyDispDate - crea display friendly fecha/tiempo de a fechatiempo (its a bit moe complicated than that though)
* guardar/cargarCalendarDatabase - saving y cargaring
* añadirEvent* - funciones para añadiring Events a el calendar
* añadirRepeatable* - funciones para añadiring Repeatables a el calendar
* eliminarEvent* - funciones para removing Events de el calendar
* eliminarRepeatable* - funciones para removing Repeatables de el calendar

## global (zz_graphicsmenu)
crea el personalizado graphics menú displayable

### classes
MASGraphicsMenu - personalizado displayable para changing el render

## `mas_hangman` (`zz_hangman`)
inicializa some hangman constantees

### imports
* `store`
* `copy`
* `random`

### constants
* `MONI_WORDS` - lista of Monika's wods
* `EASY_MODE` - constante para easy hangman mode
* `NORM_MODE` - constante para nomal hangman mode
* `HARD_MODE` - constante para hard hangman mode

### vars
* `hm_words` - diccionario of actual selectable wods by difficulty
* `all_hm_words` - diccionario of all hangman wods by difficulty

## hkb_button (zz_hotkey_buttons)
state variableiables para butan enabling

### vars
* talk_habilitard - True habilita talk butan, False deshabilita
* music_habilitard - True habilita music butan, False deshabilita
* play_habilitard - True habilita play butan, False deshabilita
* movie_butans_habilitard - True habilita play butan, False deshabilita (unusard)

## `mas_hotkeys` (`zz_hotkeys`)
state variableiables para hotclave enabling

### vars
* `talk_enabled` - True habilita talk hotclave, False deshabilita
* `music_enabled` - True habilita music hotclave, False deshabilita
* `play_enabled` - True habilita play hotclave, False deshabilita
* `derandom_enabled` - True habilita dealeaarioing, False deshabilita
* `bookmark_enabled` - True habilita bookmarking, False deshabilita
* `mu_stop_enabled` - True habilita music volume lowering / sapping hotclaves, False deshabilita
* `no_window_hiding` - True deshabilita window hiding, False habilita

## songs (zz_music_selector)
establece up music funciones y el music menú

### imports
* os
* mutagen.mp3
* mutagen.oggopus
* mutagen.oggvorbis

### constants
**NOTA:** all song names y archivopaths are constantees here (official songs, not personalizado songs)
* PAGE_LIMIT - number of songs per page

### vars
* actual_track - actually playing song
* selected_track - last selected track
* menú_open - True si el music menú is open, False en caso contrario
* music_choices - contiene el music lista
* music_pages - paginated music lista

### functions
* asoloarVolume - asoloa volume of an audio channel
* obtenerVolume - obtiene volume of an audio channel
* obtenerPlayingMusicName - obtiene el name of el actually playing song
* initMusicChoices - inicializa el music menú
* isInMusicList - comprueba if a song is in the music menú lista

## `global` (`zz_selector`)
Declares displayable para selectables

### imports
* `random`

### classes
* `MASSelectableImageButtonDisplayable` - displayable para an imagen butan that is associated con selectable.

### functions
* `mas_filterUnlockGroup` - desbloquea a selecar para a group if it passes certain criteria

## global (`zz_sprite_objects`)
inicializa `MASAccessory`, `MASHair`, y `MASClothes` objeas

## global (`zz_weather`)
Weaelr objeas are declarard here. We también cargar clima daas.

# 0
[top](./Init-Pipeline.md#quicklinks)

Este se considera el nivel de init por defecto cuando no se indica ningún número.
Además, este nivel de init cubre:
- `default` statements
- `define` statements
- pantallas (unless changed by init offestablecer)
- labels (unless changed by init offestablecer)
- estilos (unless changed by init offestablecer)
- transparams (unless changed by init offestablecer)

## mas_chess (chess)
inicializa chess constantees. None are usarful fuera de here.

## global (definitions)
inicializa a **an** of stuff. No voy a listaarlas aquí since elre's solo ao many

### functions (key ones) 
**NOTE: we debería move esas out of here. init 0 debería be avoided para all funciones.**
* `mas_passedILY`
* `mas_ILY` - establece ILY variableiables
* `mas_shouldKiss` 

## config (definitions)
inicializa some config variableiables

## audio (definitions)
all sack audio is definird here. Rain is añadired a este sare as well.

## mas_suntime (definitions)
suntiempo-related constantees y variableiables are definird here

## times (definitions)
tiempos usard in idle exp calcs

## xp (definitions)
constantees para amount of XP gained para things

## global (event-handler)
inicializa impot `Event` related funciones

### imports
* evhand
* datetime

### functions
* `addEvent` - añade an `Event` objea a an `Event` base de daas. Coe función usard para every `Event` init.
* `mas_hideEvent` - bloquea/dealeaarios/depools/deconditionals an event
* `mas_hideEventLabel` - same as above but para an event label
* `mas_showEvent` - desbloquea/aleaarios/pools an event
* `mas_showEventLabel` - same as above but para an event label
* `mas_lockEvent` - bloquea an event
* `mas_lockEventLabel` - same as above but para an event label
* `mas_unlockEvent` - desbloquea an event
* `mas_unlockEventLabel` - same as bove but para an event label
* global versiónes of isFuture/isPresent/isPast funciones
* `pushEvent` - apilar an Event a el Event stack
* `queueEvent` - pone en cola an Event a el Event stack
* `popEvent` - saca el next Event de el stack.
* `seen_event` - comprueba if an Event has been seen o is actually in el Event stack
* `restartEvent` - apila an interuppted Event back ona el Event stack if its not in el blacklista
* `mas_isRstBlk` - comprueba if el dado label is part of el blacklista
* `mas_cleanJustSeen*` - funciones para limpiaring an Event lista of things that were seen recently
* `mas_unlockPrompt` - intenta desbloquear a Pool Event
* `mas_findEVL` - obtiene index of an eventlabel in el event lista
* `mas_inEVL` - comprueba if an eventlabel is in el event lista
* `mas_rmEVL` - elimina an event label de el event lista
* `mas_rmallEVL` - elimina all occurrences of an event label de event lista

## global (import_ddlc)
1 función lol

### functions
* dumpPersistentToFile - does what it says

## config (options)
clave configuration variableiables

## gui (options)
clave gui variableiables

## build (options)
build establecertings

## preferences (options)
clave preferences

## global (pong)
pong's displayable as well as oelr pong-stuff

### imports
* random
* math

### classes
* PongDisplayable - displayable that ejecuta pong

## global (progression)
clave funciones para xp system

### functions
* grant_xp - give some experience
* obtener_level - devuelve el usarr's actual level

## global (screens)
a couple of funciones

### functions
* RigMousar - aka el mousar movement glitch
* FinishEnterName 
* FileActionMod - muestra that guardar dialogue thing

## mas_layout (screens)
Inits constantees para layout asoloarments, y some auxiliar funciones para elm ao

### imports
* store
* mas_affection

### constants
**NOTA:** este makes a montón de constantees, solo voy a mencionar impotante ones here
* QUIT_MAP - mapaeo of affection levels a what elir QUIT messages debería be

## global (script-affection)
affection state variableiables, el final despedida displayable, surprise text code

### vars
* `mas_curr_affection` - actual affection state
* `mas_curr_affection_group` - actual affection state group

### classes
* MASFinalNoteDisplayable - displayable para el final despedida poema

## global (script-apology)
solo apology related funciones

### functions
* `mas_checkApologies` - comprueba apologies y elimina antiguo ones

## global (script-ch30)
Very wide variableiety of things. Kind of like definitions 2.
Además retrieves actualusarr, comprueba playername variableiables, comprueba para battery sopote, registers el background audio channel.
Solo voy a mencionar some of el stuff here.

### imports
* subprocess
* os
* eliza
* datetime
* battery
* re
* songs
* `hkb_button`
* `mas_globals`

### vars
* `morning_flag` - True si it's actually mañana, False si no. este is moe like a previous state variable.

### functions
* `show_dialogue_box` - jumps a el talk menú
* `pick_game` - jumps a Play menú
* `mas_enable_quitbox` - habilita Monika's quit dialogue warning
* `mas_disable_quitbox` - deshabilita Monika's quit dialogue warning
* `mas_enable_quit` - habilita quitting sin Monika knowing
* `mas_disable_quit` - deshabilita quitting sin Monika knowing
* `mas_drawSpaceroomMasks` - draws el appropriate window masks
* `show_calendar` - muestra el calendar. este is el callback para clicking el calendar butan
* `slow_dismiss` - callback para when Monika talks
* `mas_isMorning` - comprueba if it's actually mañana
* `mas_shouldRain` - comprueba if it debería rain basado en actual affection
* `mas_forceRain` - paraces rain art, sounds, y bloquea rain temas
* `mas_lockHair` - bloquea hair temas
* `mas_resetIdleMode` - reestablece idle mode variableiables
* `mas_enableTextSpeed` - habilita text speed
* `mas_disableTextSpeed` - deshabilita text speed
* `mas_resetTextSpeed` - habilita o deshabilita text speed depending on environment variableiables
* `mas_isTextSpeedEnabled` - devuelve True si text speed is habilitard, False si no
* `mas_isGameUnlocked` - comprueba if dado game is desbloqueared
* `mas_unlockGame` - desbloquea el dado game
* `mas_shouldChangeTime` - comprueba if we debería change a día o noche
* `mas_check_player_derand` - comprueba guardard dealeaario prefs y dealeaarios esos temas

## gmr (script-greetings)
Stuff related a el Listen option in el opendoo saludo

### vars
* eardoo - lista of unseen (o all) Listen options
* `eardoor_all` - lista of all el Listen options

## opendoor (script-greetings)
Stuff related a el opendoo saludo

### constants
* `MAX_DOOR` - I no remember what este is para
* `chance` - 1 out of x probabilidad este saludo will appear

## global (`script-topics`)
bookmark y dealeaario funciones

### functions
* `mas_derandom_topic` - dealeaarios a tema
* `mas_bookmark_topic` - bookmarks a tema
* `mas_hasBookmarks` - comprueba if we have bookmarked temas

## global (shake)
We no usar este

## global (splash)
Splash messages are definird here

## global (sprite-chart)
All of de Monika imágenes are definird here

## `mas_coffee` (sprite-chart)
Coffee-related variableiables are definird here

## `mas_updater` (updater)
inicializa a montón de actualizaciónr related stuff

### constants
* regular - actualización link
* unstable - unstable link
* tiempoout - tiempoout para actualización comprobaring

### vars
* parace - establecido en True a parace an actualización comprobar

### functions
* comprobarUpfecha - comprueba para an actualización usyo Renpy's actualización comprobarer

## global (updates)
funciones related a actualización script migrations

### functions
* eliminarTopicID - unsees a tema if it has been seen
* `mas_eraseTopic` - elimina an Event de its persistent base de daas y bloquear db
* `mas_transferTopic` - transfers an Event's daas y bloquear db daas a anoelr Event
* `mas_transferTopicSeen` - transfers an Event's seen daas a anoelr Event
* asoloarTopicIDs - elimina / transfers an Event's seen status
* actualizaciónTopicIDs - actualizaciones a diccionario of Event's seen statusa
* actualizaciónGameFrom - ejecuta actualización scripts in el proper oder

## updates (updates_topics)
mapaeo system para actualización script migrations

### vars
* `version_updates` - diccionario that mapaea a versión a its next actualización versión
* `topics` - diccionario that mapaea a versión a el tema asoloarments it requires

## global (zz_calendar)
declara some tiempo de ejecución funciones, añade Repeatables a el calendar.

### imports
* mas_calendar

### functions
* `mas_calDropOverlayShield` - habilita input para el calendar superposición
* `mas_calHideOverlay` - oculta el calendar superposición
* `mas_calIsVisible_ovl` - comprueba if el calendar superposición is visible
* `mas_calRaiseOverlayShield` - deshabilita input para el calendar superposición
* `mas_calShowOverlay` - muestra el calendar superposición, si aún no mostraring

## `mas_dockstat` (`zz_dockingstation`)
not base, but still impotante funciones

### imports
* `store`
* `cPickle`

### functions
* `setMoniSize` - does some calculating a figure out el appropriate Monika archivosize

## global (`zz_hotkeys`)
básicamente all el hotclave-related funciones are here. I'm solo listaing el público ones.

### functions
* `mas_HKRaiseShield` - deshabilita el t/m/p hotclaves
* `mas_HKDropShield` - habilita el t/m/p hotclaves
* `mas_HKIsEnabled` - comprueba if el t/m/p hotclaves are habilitard
* `mas_HKCanQuietMusic` - comprueba if we puede lower o sap el music
* `enable_esc` - habilita el game menú / escape clave (mediante `quick_menu`)
* `disable_esc` - deshabilita el game menú / escape clave (mediante `quick_menu`)
* `set_keymaps` - inicializa el clavemapaea

## global (`zz_hotkey_buttons`)
inicializa tiempo de ejecución hotclave butan funciones, as well as muestra el butans

### functions
* `HKBHideButtons` - oculta el butans
* `HKBShowButtons` - muestra el butans
* `mas_HKBRaiseShield` - deshabilita el butans
* `mas_HKBDropShield` - habilita el butans
* `mas_HKBIsEnabled` - comprueba if el butans are habilitard
* `mas_HKBIsVisible` - comprueba if el butans are visible
* `MovieOverlayHideButtons` - oculta movie butans
* `MovieOverlayShowButtons` - muestra movie butans

## global (`zz_music_selector`)
declars music-related funciones

### imports
* songs

### functions
* `dec_musicvol` - decreases music channel volume
* `inc_musicvol` - increases music channel volume
* `mute_music` - mutes music channel
* `play_song` - plays a song ona el music channel
* `mas_startup_song` - starts playing el `persistent`.actual_track
* `select_music` - ejecuta el music selection menú

## `mas_poems` (`zz_poems`)
definir poemaas base de daas

## global (`zz_shields`)
definir shield funciones

### functions
* `mas_DropShield_core` - habilita base interactions
* `mas_RaiseShield_core` - deshabilita base interactions
* `mas_DropShield_dlg` - habilita dialogue-breaking interactions
* `mas_RaiseShield_dlg` - deshabilita dialogue-breaking interactions
* `mas_DropShield_mumu` - habilita music-menú-breaking interactions
* `mas_RaiseShield_mumu` - deshabilita music-menú-breaking interactions
* `mas_DropShield_idle` - habilita idle-breaking interactions
* `mas_RaiseShield_idle` - deshabilita idle-breaking interactions
* `mas_MUMUDropShield` - habilita el music menú
* `mas_MUMURaiseShield` - deshabilita el music menú
* `mas_dlgToIdleShield` - transitions entre dlg y idle mode
* `mas_coreToIdleShield` - transitions entre base y idle mode
* `mas_mumuToIdleShield` - transitions entre music menú y idle mode

## global (`zz_reactions`)
Public versiónes of some clave reaction funciones

### functions
* `addReaction` - añade archivo reactions
* `mas_checkReactions` - comprueba archivo reactions
* `mas_getSpriteObjInfo` - obtiene sprite info de sprite reactions lista
* `mas_finishSpriteObjInfo` - limpiarup actions para sprite reactions

## `global` (`zz_weather`)
funciones para rolling clima probabilidads

### functions
* `shouldRainToday` - comprueba if it debería rain adía

## `global` (`zz_windowreacts`)
comprueba para window reactability

### imports
* `os`
* `sys` - windows solo
* `win32gui` - windows solo
* `win32api` - windows solo
* `balloontip` - nix solo

### vars
* `win_notif_quips` - notification quips para windows
* `other_notif_quips` - notification quips para nix

### functions
* `mas_canCheckActiveWindow` - comprueba if we puede comprobar el active window
* `mas_getActiveWindow` - obtiene el active window name
* `mas_isFocused` - comprueba if MAS is actually focusard
* `mas_isInActiveWindow` - comprueba if clavewods are in el active window name
* `mas_clearNotifs` - clears notifications that we generated
* `mas_checkforWindowReacts` - comprueba if a windowreaction debería occur y pone en cola it
* `mas_resetWindowReacts` - desbloquea window reactions in window react db
* `mas_updateFilterDict` - actualizaciones filter diccionario
* `mas_addBlacklistReact` 
* `mas_removeBlacklistReact`
* `mas_notifsEnabledforGroup` - comprueba si noifications are habilitard para a group
* `mas_unlockFailedWRS` - desbloquea a window react if it failed a be mostrarn
* `mas_tryShowNotificationOSX` - trys a mostrar a notification on mac
* `mas_tryShowNotificationLinux` - trys a mostrar a notification on linux

# 1
[top](./Init-Pipeline.md#quicklinks)

## mas_chess (chess)
huge number of chess constantees, chess dialogue variableiables, as well as chess comprobaring funciones.
Además inicializa el dialogue actions mapa y el chess quiplistaas

### imports
* `os`
* `chess.png`

### vars
* `quit_game` - habilita quitting a chess match

### functions
* `isInProgressGame` - comprueba if a pgn game is valid y in progress

## global (defintions)
Properly establece `persistent.steam`

## mas_randchat (definitions)
Sets up el aleaario chatter funciones y constantees

### functions
* `adjustRandFreq` - asoloa aleaario chatter frequency dado a slider value
* `getRandChatDisp` - convierte aleaario chatter frequency ina a display string

## evhand (event-handler)
Coe action funciones para `Event`'s usage. All of este stuff debería be interno solo.

# 2
[top](./Init-Pipeline.md#quicklinks)

## global (definitions)
Creates coffee related funciones, también variableious oelr funciones

### functions
* `mas_brewCoffee` - starts brewing coffee
* `mas_drinkCoffee` - starts drinking coffee
* `mas_isCoffeeTime` - comprueba if its coffee tiempo
* `mas_resetCoffee` - reestablece coffee variableiables
* `mas_canShowRisque` - comprueba if we puede mostrar risque content
* `mas_getPlayerAge` - obtiene el player age
* `mas_getRPYFiles` - obtiene lista of rpy archivos in el game dir
* `mas_hasRPYFiles` - comprueba if elre are rpy archivos in el game dir
* `mas_is18Over` - comprueba if el player is over 18
* `mas_isFirstSeshDay` - comprueba if dado fecha is el first session fecha
* `mas_pastOneDay` - comprueba if a one día has passed since a dado `datetime.date` o `datetime.datetime`
* `mas_timePastSince` - comprueba if a dado amount of tiempo passed since a dado `datetime.date` o `datetime.datetime`

## global (script-affection)
Creates el final despedida poema

# 4
[top](./Init-Pipeline.md#quicklinks)

## global (definitions)
makes el `mas_randchat` sare globally available

## `global` (`event-handler`)
Maps event base de daass a codes y limpia añoestablecer baclkist

### functions
* `mas_lastSeenInYear` - comprueba if an event label was last seen in a dado año
* `mas_lastSeenLastYear` - comprueba if an event label was last seen last año

## `mas_gtod` (`script-grammar`)
grammar tip auxiliar funciones

### imports
* `datetime`
* `evhand`

### functions
* `has_day_past_tip` - comprueba if a tip has been seen y a día has past

## global (script-holidays)
Poems are definird here

## `global` (`script-islands-event`)
asoloar islys flag if needed

## `mas_ptod` (`script-python`)
declara auxiliar funciones para python tips

### imports
* `datetime`
* `evhand`

### functions
* `has_day_past_tip` - comprueba if a tip has been seen y a día has past
* `has_day_past_tips` - multiple arg versión of above función

## global (updates)
Runs pre-script temas actualización code. Not really usard

## `mas_calendar` (`zz_calendar`)
calendar funciones y season establecerting

### functions
* `addSeasonEvents` - añade seasons a calendar

# 5
[top](./Init-Pipeline.md#quicklinks)

En este nivel de init se crea cada tema. Evita usar este nivel de init para cualquier otra cosa.
También usamos este init para generar las notas de copia de seguridad.

# 6
[top](./Init-Pipeline.md#quicklinks)

## `global` (`event-handler`)
Creates all event base de daas, también clave funciones

### functions
* `mas_getEV` - obtiene an event objea mediante label
* `mas_getEVCL` - solo para calendar usar.
* `mas_hideEVL` - oculta an event, usyo a code a determine base de daas
* `mas_lockEVL` - bloquea an event, usyo a code a determine base de daas
* `mas_showEVL` - muestra an event, usyo a code a determine base de daas
* `mas_stripEVL` - strips conditional y action de an event, también elimina de event lista
* `mas_unlockEVL` - desbloquea an event, usyo a code a determine base de daas`

# 9
[top](./Init-Pipeline.md#quicklinks)

## global (updates_topics)
Runs el label that inicializa el `updates` sare con actualización mapaeo daas.

# 10
[top](./Init-Pipeline.md#quicklinks)

## mas_anni (script-anniversary)
Sets up anniversary base de daas as well as clave anniversary asoloaring funciones

### constants
* `ANNI_LIST` - lista of anniversaries in oder of potential appearance

### vars
* `anni_db` - `Event` base de daas para anniversaries

### functions
* `_month_adjuster` - asoloa mess para a nuevo start fecha
* `_day_adjuster` - asoloar días para a nuevo start fecha
* `add_cal_annis` - añade anniversaries a el calendar
* `clean_cal_annis` - limpia anniversaries de el calendar
* `reset_annis` - reestablece all anniversaries usyo a nuevo start fecha
* `unlock_past_annis` - desbloquea all anniversaries that are past el actual fecha

## global (script-greetings)
This is solo para el Listen option para el saludos. It elimina seen labels y does reestablece si es necesario.

## global (updater)
Declares el background actualización comprobar función

### functions
* `mas_backgroundUpdateCheck` - launches el background actualización comprobar thread

## global (updates)
Runs el versión actualización migration scripts.

## global (`zz_hangman`)
Inits el wodlistaas para hangman

## songs (zz_music_selector)
establece `music_volume` a el actual volume of el music channel

## global (zz_music_selector)
Properly establece el personalizado music direcary, actual track y el available music choices.

## global (`zz_poems`)
definir `MASPoem` clase

## global (`zz_weather`)
Weaelr clase

### classes
* `MASWeather` - clima objea clase

# 11
[top](./Init-Pipeline.md#quicklinks)

## global (script-topics)
Initializes el seen listaas. They are not built until later.

### vars
* `mas_rev_unseen` - lista of unseen `Event`s
* `mas_rev_seen` - lista of seen `Event`s
* `mas_rev_mostseen` - lista of most seen `Event`s

## `mas_poems` (`zz_poems`)
definir clave poema-realted funciones

# 15
[top](./Init-Pipeline.md#quicklinks)

## `mas_affection` (`script-affection`)
Contains all el affection programming points, el logic a ejecutar esos programming points, y wrapper funciones around el base affection state comparaars.
Además inicializa el variableiying talk / play menú quips
**NOTA:** Makes a reference copia of el `persistent`
**NOTA:** Makes a reference copia of el `layout` sare.

### imports
* `store`
* `evhand`
* `mas_layout`

### functions
**NOTA:** Most of esas are programming points. No need a lista elm here
* `runAffPPs` - ejecuta el affection state programming points
* `runAffGPPs` - ejecuta el affection state group programming points

# 20
[top](./Init-Pipeline.md#quicklinks)

## global (script-affection)
Declares all el globally available affection funciones y poemaas

### imports
* `datetime`
* `mas_affection`
* `mas_utils`

### vars
* `mas_apology_reason` - el reason a apologize

### functions
* `mas_FreezeGoodAffExp` - freezes affection gains
* `mas_FreezeBadAffExp` - freezes affection losses
* `mas_FreezeBothAffExp` - freezes affection gains y losses
* `mas_UnfreezeGoodAffExp` - unfreezes affection gains
* `mas_UnfreezeBadAffExp` - unfreezes affection losses
* `mas_UnfreezeBothAffExp` - unfreezes affection gains y losses
* `mas_betweenAff` - comprueba if affection is entre 2 states
* `mas_compareAff` - compare-a función para comparing affection states
* `mas_compareAffG` - compare-a función para comparing affection group states
* `mas_isMoniBroken` - comprueba if actual affection is broken (o lower/higher)
* `mas_isMoniDis` - comprueba if actual affection is distressed (o lower/higher)
* `mas_isMoniUpset` - comprueba if actual affection is upestablecer (o lower/higher)
* `mas_isMoniNormal` - comprueba if actual affection is nomal (o lower/higher)
* `mas_isMoniHappy` - comprueba if actual affection is happy (o lower/higher)
* `mas_isMoniAff` - comprueba if actual affection is affectionate (o lower/higher)
* `mas_isMoniEnamored` - comprueba if actual affection is enamoed (o lower/higher)
* `mas_isMoniLove` - comprueba if actual affection is love (o lower/higher)
* `mas_isMoniGSad` - comprueba if actual affection group is sad (o lower/higher)
* `mas_isMoniGNormal` - comprueba if actual affection group is nomal (o lower/higher)
* `mas_isMoniGHappy` - comprueba if actual affection group is happy (o lower/higher)
* `mas_updateAffectionExp` - establece el affection states a el corect value y ejecuta affection programming points when appropriate
* `mas_gainAffection` - increases affection
* `mas_loseAffection` - decreases affection
* `mas_setAffection` - establece affection a a value
* `mas_checkAffection` - apila an appropriate event basado en affection level
* `mas_setApologyReason` - habilita an apology
* `_mas_getAffection` - obtiene raw affection value
* `_mas_getBadExp` - obtiene bad aff exp establecerting
* `_mas_getGoodExp` - obtiene good aff exp establecerting
* `_mas_getTodayExp` - gest adía aff exp establecerting

# 21
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites_json` (`zz_spritejsons`)
Initializes clave sprite json related constantees

### imports
* `json` 
* `store`
* `mas_utils`

### constants
* `SP_ACS` - sprite type para ACS
* `SP_HAIR` - sprite type para hair
* `SP_CLOTHES` - sprite type para cloels
* `SP_CONSTS` - tuple of all spriet types
* `SP_STR` - sprite type a string name mapaeo (para debug usar)
* `SP_UF_STR` - sprite type usarr friendly string name mapaeo
* `SP_PP` - sprite type a prog point paramat
* `SP_RL` - sprite type a reaction label paramat

### vars
* `giftname_map` - mapaea giftnames a sprite type y name
* `namegift_map` - mapaea sprite type y name a giftname

# 100
[top](./Init-Pipeline.md#quicklinks)

## global (screens)
establece up el appropriate layout variableiables para ui text

## global (zz_calendar)
declars a función para asoloaring el conditional of el start fecha `Event`

### functions
* `mas_chgCalEVul` - literally solo changes conditional para el state fecha `Event`

# 189
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites_json` (`zz_spritejsons`)
json parsing funciones

### imports
* `mas_sprites` as `sms`
* `mas_selspr` as `sml`

# 190
[top](./Init-Pipeline.md#quicklinks)

## `mas_sprites_json` (`zz_spritejsons`)
Checks para JSON sprites y añade elm

# 200
[top](./Init-Pipeline.md#quicklinks)

## `mas_dockstat` (`zz_dockingstation`)
Declares de Monika dockingstation función

### imports
* `store`
* `cStringIO`
* `os`
* `mas_greetings`
* `mas_ics`
* `mas_sprites`
* `evhand`
* `random`
* `datetime`
* `threading`

### functions
* `generateMonika` - generates Monika's nuevo character archivo
* `findMonika` - finds de Monika character archivo
* `init_findMonka` - find Monika, init versión
* `parseMoniData` - analiza Monika character archivo daas ina components
* `selectReturnHomeGreeting` - picks an appropriate saludo if we are devolvering Monika a characters carpeta
* `diffCheckTimes` - devuelve a tiempodelta difference entre last comprobarin/comprobarout tiempos
* `packageCheck` - moe generic package comprobaring función that puede do eielr `signForPackage` y `createPackageSlip`
* `checkinMonika` - comprueba Monika ina el docking station
* `checkoutMonika` - comprueba Monika out of el docking station
* `getCheckTimes` - obtiene a coresponding comprobarin/comprobarout tiempo para a dado compruebaum

## `mas_selspr` (`zz_selector`)
Loads selectable daas.

# 205
[top](./Init-Pipeline.md#quicklinks)

## `mas_dockstat` (`zz_dockingstation`)
Declares async promises.

### imports
* `mas_threading`

### vars
* `monikagen_promise` - `MASAsyncWrapper` objea para generation Monika
* `monikafind_promise` - `MASAsyncWrapper` objea para finding Monika

### functions
* `abortGenPromise` - specifically abots el generation promise in case we aboted it.

# 500
[top](./Init-Pipeline.md#quicklinks)

All imágenes are built at este init level. 

# 501
[top](./Init-Pipeline.md#quicklinks)

## global (zz_overlays)
Declares superposición-related funciones

### functions
* `mas_OVLDropShield` - habilita all superposición pantallas
* `mas_OVLHide` - oculta all superposición pantallas
* `mas_OVLRaiseShield` - deshabilita all superposición pantallas
* `mas_OVLShow` - muestra all superposición pantallas

# 790
[top](./Init-Pipeline.md#quicklinks)

## mas_piano_keys (zz_pianokeys)
Hantiguos el funciones para añadiring JSON songs a piano

### imports
* `json`

### functions
* `addSong` - añade a song a el `PianoNoteMatchList` base de daas
* `addCustomSongs` - analiza el personalizado song carpeta para songs y añade elm a el `PianoNoteMatchList` base de daas
* `addStockSongs` - añade a preestablecer lista of songs a el `PianoNoteMatchList` base de daas

# 800
[top](./Init-Pipeline.md#quicklinks)

## global (`zz_backgrounds`)
background changing funciones

## `mas_piano_keys` (`zz_pianokeys`)
Adds el sack y personalizado songs a el `PianoNoteMatchList` base de daas. Además declara a función para generating el piano song menú.

### functions
* `getSongChoices` - generates a lista of tuples para el piano song selection menú

## global (`zz_reactions`)
Deletes archivos of reactions that failed a be eliminard.

## global (`zz_weather`)
Global clima funciones, as well as establecerting el initial clima

### functions
* `mas_setWeather` - establece el clima sin calling exit programming points
* `mas_changeWeather` - establece el clima calling both entry exit programming points

# 810
[top](./Init-Pipeline.md#quicklinks)

## global (zz_pianokeys)
Creates el piano displayable

### imports
* `mas_piano_keys`

### classes
* `PianoDisplayable` - displayable that ejecuta el piano

### functions
* `pnmlLoadTuples` - carga `PianoNoteMatchList` daas de `persistent` ina coresponding objeas in el `PianoNoteMatchList` base de daas
* `pnmlSaveTuples` - guarda `PianoNoteMatchList` daas ina `persistent` de coresponding objeas in el `PianoNoteMatchList` base de daas

# 899
[top](./Init-Pipeline.md#quicklinks)

## global (chess)
inicializa el chess quiplista

# 900
[top](./Init-Pipeline.md#quicklinks)

En general, aquí se construyen todas las funciones constructoras de DelayedAction.

## global (screens)
Inits el quit messages para layout

# 970
[top](./Init-Pipeline.md#quicklinks)

## global (script-ch30)
Checks para:
* Monika's archivo
* archivo reactions
* cumple stuff
* o31 stuff

### imports
* `mas_filereacts`

# 994
[top](./Init-Pipeline.md#quicklinks)

## mas_delact (event-handler)
Sets up el DelayedAction mapa 

### constants
* `MAP` - Maps DelayedAction IDs a construcar funciones

### functions
* `loadDelayedActionMap` - generates el tiempo de ejecución mapa of DelayedActions de `persistent`
* `saveDelayedActionMap` - guarda el tiempo de ejecución mapa of DelayedActions a `persistent`

# 995
[top](./Init-Pipeline.md#quicklinks)

## global (event-handler)
Runs DelayedActions at el init stage

# 999
[top](./Init-Pipeline.md#quicklinks)

## global (updates)
Runs el late actualización scripts
