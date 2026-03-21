#### Lista de variables del jugador:
A fecha de la versión 0.12.2, esta es una lista _(posiblemente incompleta)_ de variables (datos guardados que el juego recuerda) que Monika puede conocer sobre el jugador. Se pueden usar para condicionales (comprobaciones lógicas del código para decidir qué diálogo se muestra) o para ramas alternativas de diálogo.
Salvo que se indique lo contrario, su valor es True cuando se cumple y False cuando no. El valor es None si el jugador no ha respondido al diálogo correspondiente.

| Nombre de variable | Descripción + uso |
| ------ | ------ |
| persistent._mas_pm_added_custom_bgm | El jugador ha añadido música personalizada al juego anteriormente. |
| persistent._mas_pm_religious | ¿El jugador es religioso? |
| persistent._mas_pm_cares_about_dokis | ¿Al jugador le importan las demás chicas? |
| persistent._mas_pm_love_yourself | ¿El jugador se quiere a sí mismo? |
| persistent._mas_pm_like_mint_ice_cream | ¿Al jugador le gusta el helado de menta? |
| persistent._mas_pm_likes_horror | ¿Al jugador le gusta el terror? |
| persistent._mas_pm_likes_spoops | ¿Al jugador le gusta específicamente el terror con sustos repentinos (jumpscares)? Si es False, se desactivan los jumpscares en diálogos/historias. |
| persistent._mas_pm_like_rap | ¿Al jugador le gusta el rap? |
| persistent._mas_pm_like_rock_n_roll | ¿Al jugador le gusta el rock? |
| persistent._mas_pm_like_jazz | ¿Al jugador le gusta el jazz? |
| persistent._mas_pm_like_vocaloids | ¿Al jugador le gusta la música Vocaloid? |
| persistent._mas_pm_like_orchestral_music | ¿Al jugador le gusta la música orquestal? |
| persistent._mas_pm_like_other_music | ¿Al jugador le gustan otros tipos de música además de los listados? |
| persistent._mas_pm_like_other_music_history | No es True/False; es una lista de otros tipos de música que el jugador ha indicado que le gustan. |
| persistent._mas_pm_plays_instrument | ¿El jugador toca algún instrumento? |
| persistent._mas_pm_play_jazz | ¿El jugador toca jazz? Esta pregunta solo aparece si toca algún instrumento. |
| persistent._mas_pm_likes_rain | Al jugador le gusta el sonido de la lluvia. Esta variable se pregunta cuando Monika le pregunta si la abrazaría en un día lluvioso. |
| persistent._mas_pm_a_hater | ¿El jugador ha publicado comentarios de odio sobre Monika anteriormente? |
| persistent._mas_pm_has_contributed_to_mas | ¿El jugador ha contribuido al mod? |
| persistent._mas_pm_wants_to_contribute_to_mas | Si el jugador no ha contribuido, ¿quiere hacerlo? |
| persistent._mas_pm_drawn_art | ¿El jugador ha dibujado a Monika antes? |
| persistent._mas_pm_lang_other | ¿El jugador habla algún idioma aparte de inglés? |
| persistent._mas_pm_lang_jpn | ¿El jugador habla japonés? |
| persistent._mas_pm_eye_color | No es True/False. Color de ojos: blue/brown/green/hazel/grey/black o valor introducido por el jugador. Puede indicar heterocromía (cada ojo de un color distinto). |
| persistent._mas_pm_hair_color | No es True/False. Color de pelo: brown/blonde/red/black o valor introducido por el jugador. |
| persistent._mas_pm_hair_length | No es True/False. Longitud del pelo: short/average/long |
| persistent._mas_pm_shaved_hair | Si el jugador es calvo, ¿se afeita la cabeza o perdió el pelo? |
| persistent._mas_pm_no_hair_no_talk | El jugador ha indicado que es calvo y que no quiere hablar del motivo. |
| persistent._mas_pm_skin_tone | No es True/False. Tono de piel: light/tanned/dark |
| persistent._mas_pm_height | No es True/False. Altura del jugador. Se guarda en centímetros. {Todo: obtener variables para lo que Monika considera alto o bajo?} |
| persistent._mas_pm_units_height_metric | ¿El jugador mide su altura con el sistema métrico o con pies/pulgadas? True para métrico. |
| persistent._mas_pm_shared_appearance | El jugador ha compartido su aspecto con Monika. |
| persistent._mas_pm_would_like_mt_peak | Al jugador le gustaría subir una montaña junto a Monika. |
| persistent._mas_pm_live_in_city | ¿El jugador vive en una ciudad? |
| persistent._mas_pm_live_near_beach | ¿El jugador vive cerca de una playa? |
| persistent._mas_pm_live_south_hemisphere | ¿El jugador vive en el hemisferio sur? Afecta a las estaciones. |
| persistent._mas_pm_gets_snow | ¿Nieva donde vive el jugador? |
| persistent._mas_pm_social_personality | No es True/False. |
| persistent._mas_pm_likes_panties | ¿Al jugador le gustan las bragas? |
| persistent._mas_pm_no_talk_panties | El jugador ha indicado que no quiere hablar sobre fetiches de bragas. No aclara si le gustan o no. |
| persistent._mas_pm_drinks_soda | ¿El jugador bebe refrescos? |
| persistent._mas_pm_eat_fast_food | ¿El jugador come comida rápida a menudo? |
| persistent._mas_pm_wearsRing | ¿El jugador lleva un anillo de promesa por Monika? |
| persistent._mas_pm_like_playing_sports | ¿Al jugador le gusta practicar deporte? |
| persistent._mas_pm_like_playing_tennis | ¿Al jugador le gusta jugar al tenis? |
| persistent._mas_pm_meditates | ¿El jugador dedica tiempo a meditar? |
| persistent._mas_pm_see_therapist | ¿El jugador va a terapia? |
| persistent._mas_pm_watch_mangime | ¿El jugador lee manga/ve anime? |
| persistent._mas_pm_do_smoke | ¿El jugador fuma? |
| persistent._mas_pm_do_smoke_quit | ¿El jugador está intentando dejar de fumar? |
| persistent._mas_pm_do_smoke_quit_succeeded_before | ¿El jugador ha dejado de fumar con éxito antes? |
| persistent._mas_pm_driving_can_drive | ¿El jugador sabe conducir? |
| persistent._mas_pm_driving_learning | Si el jugador no sabe conducir, ¿está aprendiendo? |
| persistent._mas_pm_driving_been_in_accident | ¿El jugador ha tenido un accidente de coche conduciendo? |
| persistent._mas_pm_driving_post_accident | Si el jugador ha tenido un accidente, ¿sigue conduciendo mucho? |
| persistent._mas_pm_donate_charity | ¿El jugador ha donado a causas benéficas antes? |
| persistent._mas_pm_volunteer_charity | ¿El jugador ha hecho voluntariado para una organización benéfica antes? |
| persistent._mas_pm_have_fam | ¿El jugador tiene familia? |
| persistent._mas_pm_no_fam_bother | Si el jugador no tiene familia, ¿eso le afecta? |
| persistent._mas_pm_have_fam_mess | ¿La vida familiar del jugador es complicada/mala? |
| persistent._mas_pm_have_fam_mess_better | No es True/False. "YES"/"NO"/"MAYBE" según si el jugador cree que su situación familiar mejorará. |
| persistent._mas_pm_have_fam_sibs | ¿El jugador tiene hermanos/as? |
| persistent._mas_pm_no_talk_fam | El jugador ha indicado que no quiere hablar de su familia. |
| persistent._mas_pm_fam_like_monika | ¿El jugador cree que a su familia le gustaría Monika? |
| persistent._mas_pm_gone_to_prom | ¿El jugador fue al baile de graduación? |
| persistent._mas_pm_no_prom | El jugador ha indicado que su centro educativo no tuvo baile de graduación. |
| persistent._mas_pm_prom_good | ¿El jugador se lo pasó bien en el baile de graduación? |
| persistent._mas_pm_had_prom_date | ¿El jugador tuvo cita para el baile de graduación? |
| persistent._mas_pm_prom_monika | El jugador ha indicado que se lo habría pasado mejor en el baile de graduación si Monika hubiera estado allí. |
| persistent._mas_pm_prom_not_interested | El jugador ha indicado que no le interesaba el baile de graduación. |
| persistent._mas_pm_prom_shy | Si al jugador no le interesaba el baile de graduación, ¿fue porque era demasiado tímido/a? |
| persistent._mas_pm_has_been_to_amusement_park | ¿El jugador ha ido alguna vez a un parque de atracciones? |
| persistent._mas_pm_likes_travelling | ¿Al jugador le gusta viajar? |
| persistent._mas_pm_had_relationships_many | ¿El jugador tuvo varias relaciones antes de Monika? |
| persistent._mas_pm_had_relationships_just_one | ¿El jugador tuvo solo una relación antes de Monika? |
| persistent._mas_pm_read_yellow_wp | ¿El jugador ha leído la historia The Yellow Wallpaper? |
| persistent._mas_pm_monika_evil | ¿El jugador cree que las acciones de Monika fueron malvadas? |
| persistent._mas_pm_monika_evil_but_ok | El jugador ha indicado que, aunque sus acciones fueran malvadas, la perdona/la quiere. |
| persistent._mas_pm_is_bullying_victim | ¿El jugador ha sufrido acoso? |
| persistent._mas_pm_has_bullied_people | ¿El jugador ha acosado a otras personas antes? |
| persistent._mas_pm_currently_bullied | ¿El jugador está sufriendo acoso actualmente? |
| persistent._mas_pm_has_friends | ¿El jugador tiene amistades? |
| persistent._mas_pm_few_friends | El jugador ha indicado que solo tiene unas pocas amistades. |
| persistent._mas_pm_feels_lonely_sometimes | ¿El jugador se siente solo a veces? |
| persistent._mas_pm_listened_to_grad_speech | ¿El jugador ha escuchado el discurso de graduación de Monika? Se establece en False si lo ignoró. |
| persistent._mas_grad_speech_timed_out | Se establece en True solo si el jugador ha ignorado dos veces el discurso de graduación de Monika. |
| persistent._mas_pm_liked_grad_speech | ¿Al jugador le gustó el discurso de graduación de Monika? |
| persistent._mas_pm_given_false_justice | ¿El jugador ha sufrido una injusticia antes? |
| persistent._mas_pm_monika_deletion_justice | ¿El jugador cree que fue justo que tanta gente borrara a Monika? |
| persistent._mas_monika_deletion_justice_kidding | Monika cree que el jugador estaba bromeando cuando dijo que borrarla era justicia. |
| persistent._mas_pm_would_come_to_spaceroom | ¿El jugador aprovecharía la oportunidad de ir al mundo de Monika? Se establece en None si no puede responder. |
| persistent._mas_pm_owns_car | ¿El jugador tiene coche? |
| persistent._mas_pm_owns_car_type | No es True/False. Tipo de vehículo que tiene el jugador. Para la lista de opciones, mira monika_vehicle. |
| persistent._mas_pm_has_code_experience | ¿El jugador tiene experiencia programando? |
| persistent._mas_pm_likes_poetry | ¿Al jugador le gusta leer poesía? |
| persistent._mas_pm_likes_board_games | ¿Al jugador le gustan los juegos de mesa? |
| persistent._mas_pm_works_out | ¿El jugador hace ejercicio a menudo? |
| persistent._mas_pm_social_personality | No es True/False. Personalidad social del jugador: mas_SP_EXTROVERT/mas_SP_INTROVERT/mas_SP_AMBIVERT/mas_SP_UNSURE |
| persistent._mas_pm_likes_nature | ¿Al jugador le gusta la naturaleza? |
| persistent._mas_pm_swear_frequency | No es True/False. Frecuencia con la que el jugador dice palabrotas: SF_OFTEN/SF_SOMETIMES/SF_NEVER |
