# `assets/` — recursos multimedia

> ⚠️ **Esta carpeta NO está cubierta por la licencia del código.**
> El `LICENSE` (MIT) de la raíz se aplica solo al HTML/CSS/JS del proyecto.
> Nada de lo que hay aquí puede redistribuirse bajo esa licencia: no somos sus
> titulares y no tenemos derecho a cederlo. Detalles en [`../NOTICE`](../NOTICE).

Contenido servido junto a las páginas: los tres builds lo cargan con rutas
relativas (`assets/...`), ya no va incrustado en base64 dentro del HTML.

## Inventario completo

Los **63 ficheros** de `assets/`, uno por uno, con su función y su procedencia. Los 46 mp3 de
FNAF 1 se detallan en la sección siguiente, con el evento que los dispara y su nivel de
verificación.

| # | Archivo | Función | Procedencia / licencia |
|---|---|---|---|
| 1 | `README.md` | este documento: procedencia, atribución y excepción de licencia | Equipo Pineapple · obra propia |
| 2 | `fonts/OFL.txt` | texto de la licencia SIL OFL 1.1 que cubre las dos tipografías | SIL Open Font License 1.1 |
| 3 | `fonts/creepster-400.woff2` | tipografía de los títulos y del logotipo en pantalla | © 2011 Font Diner, Inc · **SIL OFL 1.1** |
| 4 | `fonts/vt323-400-latin.woff2` | tipografía de terminal: HUD, reloj y etiquetas de cámara (subconjunto latin) | © 2011 The VT323 Project Authors · **SIL OFL 1.1** |
| 5 | `fonts/vt323-400-latin-ext.woff2` | la misma tipografía, subconjunto latin-ext para acentos y eñes | © 2011 The VT323 Project Authors · **SIL OFL 1.1** |
| 6 | `img/splash-logo.png` | logo del splash «Pineapple presenta» al arrancar | Equipo Pineapple · obra propia |
| 7 | `img/newspaper-intro.png` | periódico «Skibiry Herald» de la intro de cada noche | Scott Cawthon · obra mixeada |
| 8 | `audio/title-theme.m4a` | música de la pantalla de título y del menú | Scott Cawthon · obra propia |
| 9 | `audio/click.mp3` | clic de interfaz en botones y menús | Equipo Pineapple · obra propia |
| 10 | `audio/phone/night1.mp3` | llamada del encargado de la noche 1 (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| 11 | `audio/phone/night2.mp3` | llamada del encargado de la noche 2 (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| 12 | `audio/phone/night3.mp3` | llamada del encargado de la noche 3 (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| 13 | `audio/phone/night4.mp3` | llamada del encargado de la noche 4 (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| 14 | `audio/phone-unreleased/night1.mp3` | llamada del encargado de la noche 1 (compilación Unreleased) | Equipo Pineapple · obra propia |
| 15 | `audio/phone-unreleased/night2.mp3` | llamada del encargado de la noche 2 (compilación Unreleased) | Equipo Pineapple · obra propia |
| 16 | `audio/phone-unreleased/night3.mp3` | llamada del encargado de la noche 3 (compilación Unreleased) | Equipo Pineapple · obra propia |
| 17 | `audio/phone-unreleased/night4.mp3` | llamada del encargado de la noche 4 (compilación Unreleased) | Equipo Pineapple · obra propia |
| 18–63 | `audio/fnaf1/*.mp3` (46) | efectos y música del **FNAF 1**, uno por uno en la sección siguiente | recursos de audio de **Five Nights at Freddy's** → **Scott Cawthon** · ⛔ no redistribuir |

**Regla general:** mientras un fichero no esté confirmado como obra propia, se trata como recurso
de terceros y queda **excluido** de la licencia del código. Si uno resulta ser propio, basta con
cambiar su fila.

Los binarios idénticos entre builds se guardan una sola vez y se comparten: el logo, el periódico,
la música del título y el clic son los mismos ficheros para las tres versiones.

## Audio de FNAF 1 — `audio/fnaf1/`

46 efectos en MP3 procedentes del pack *Sound Effects* de **Five Nights at
Freddys** en [The Sounds Resource](https://sounds.spriters-resource.com/pc_computer/fivenightsatfreddys/asset/398089/)
(asset 398089, subido por `MilesTheCreator`), convertidos de WAV a MP3.
Pertenecen al juego original de **Scott Cawthon**: están aquí como recurso de un
fangame gratuito y sin ánimo de lucro, **excluidos de la licencia** y no
redistribuibles, igual que el resto de esta carpeta.

**Los archivos están renombrados según el uso que tienen en el juego**
(`golpes-en-la-puerta.mp3`, `jumpscare.mp3`, `campanas-6am.mp3`…), no con el
nombre del pack. La última columna de cada tabla conserva el nombre original
para poder rastrear la procedencia. De los 46, **45 se disparan en el juego**; el
único que no lo hace es `tema-menu-fnaf1.mp3`, que es el tema del menú original.

**Regla que sigue el motor: una muestra nunca dura más que el evento que la
dispara.** El glitch visual de una cámara dura 280–620 ms, así que
`interferencia-camara-*` (2–3 s) se recorta a 0,55 s; el golpe en la puerta anima
380 ms + 1100 ms de retirada, así que `golpes-en-la-puerta` (3,37 s) se recorta a
1,40 s. Los recortes y los *cooldowns* están en la tabla `SFX` del HTML, en un
solo sitio.

### Audio posicional

Los sonidos que ocurren en un sitio del local se colocan ahí con un `PannerNode`
HRTF: el oyente está sentado en la oficina mirando al frente, las puertas quedan
a izquierda y derecha a medio metro, los pasillos se alejan hacia el fondo y las
salas se reparten alrededor. Así la puerta izquierda suena a la izquierda,
IShowSpeed corre por el pasillo oeste y el escenario queda al fondo, con
atenuación por distancia.

Cada cámara tiene su punto (`CAM_POS`): los pasillos oeste (2A/2B/2C) caen a la
izquierda y los este (4A/4B/4C) a la derecha, como en el mapa del juego. La
música y el ambiente del local **no** se panean, porque no vienen de un sitio.
`SFX_3D=false` lo degrada a paneo estéreo, y si el navegador no tiene
`PannerNode` la caída es automática.

Cuatro sonidos que ocurren en una sala concreta se anclan a su cámara, de modo que
pueden sonar en cualquier momento y se oyen venir de donde toca:

| Sonido | Se coloca en |
|---|---|
| `musica-pirate-cove.mp3` | Pirate Cove (CAM 5) |
| `organo-de-circo.mp3` | CAM 1B |
| `voz-robotica-pasillo.mp3` | esquina del pasillo: CAM 2B a la izquierda, 4B a la derecha |
| `ruidos-cocina-*.mp3` | la cocina (CAM 6, que no tiene imagen) |

### Mezcla

Los deslizadores mandan sobre lo que corresponde: **Música** controla la música
del menú *y* la del juego (Toreador, Pirate Cove, fiesta y campanas de las 6 AM,
marcadas con `music:1` en la tabla `SFX`); **Efectos** controla el resto;
**Maestro** los dos. Antes el deslizador de Música solo afectaba al menú y la
música del menú llevaba un 0,42 fijo que se saltaba el ajuste.

La llamada del encargado suena por un `<audio>` aparte, fuera del bus maestro,
así que mientras habla el ambiente y la estática se atenúan a un tercio y
vuelven a su nivel al cortar.

Para comprobar de oído que cada sonido está donde debe: **[`audio-test.html`](../audio-test.html)**.

### De dónde salen

Dos páginas de la Five Nights at Freddy's Wiki son la fuente de las identidades:

- [**Archivos de sonido (FNaF)**](https://freddy-fazbears-pizza.fandom.com/es/wiki/Archivos_de_sonido_(FNaF)) — la lista completa de efectos del FNAF 1,
  agrupados por uso: animatrónicos, movimiento, música de ambiente, monitor, puertas y
  luces, cocina, gemidos y llamadas.
- [**Soundtrack (FNaF1)**](https://freddy-fazbears-pizza.fandom.com/wiki/Soundtrack_(FNaF1)) — las pistas musicales, con título real, autor y el
  momento exacto en que suenan.

Lo que se corrigió con ellas:

- `music_box.ogg` **es** la Marcha del Toreador (Bizet, muestra *1905 Regina Music Box*
  de Sound Ideas) y suena al irse la luz o con Freddy en la Cocina.
- `Darkness music.ogg` no es el Toreador: es el **tema del menú** de Steam (*Urban
  Darkness Part 08*, Bjørn Lynne).
- `ColdPresc B.ogg` es el ambiente principal de la noche y `Ambience2.ogg` el del
  **apagón**; estaban intercambiados.
- `EerieAmbienceLargeSca MV005.ogg` es la «música de ambiente 2», la que suena **cuando
  un animatrónico está cerca**, con la escalera de volumen 30/50/75/100 %.
- `Circus.ogg` suena al azar **cuando uno de los animatrónicos está activo**, no en la
  intro del periódico.
- `OVEN-DRA*` no eran candidatas a puerta: son los cuatro **ruidos de Chica en la
  cocina** (`OVEN-DRAWE` = *oven drawer*).
- `robotvoice` es la **voz robótica** de las esquinas de los pasillos desde la 4.ª noche.
- `XSCREAM2` es el grito **lento** del jumpscare de Golden Freddy, distinto del normal.
- `BallastHumMedium2` es el zumbido de las **luces de los pasillos**.
- Las interferencias de cámara (`garble1-3`) ya estaban bien: la wiki las atribuye a los
  animatrónicos moviéndose, y el juego las dispara desde `camMoveGlitch()`.

Dos identidades son **inferencia**, no dato de la wiki, y están marcadas como tales: que
`Laugh_Giggle_Girl_1d/2d/8d` sean las risas lentas de Freddy al moverse (coincide con la
distinción *lento*/*normal* de la wiki) y que `CAMERA_VIDEO_LOA_60105303` sea el monitor
al subirlo. La wiki confirma que existe un sonido real de puertas (`Puertas de la
Office.ogg`), pero **no está en el pack subido**, así que la puerta sigue sintetizada.

### Nivel de verificación

Cada fila de las dos tablas anteriores lleva marcado de dónde sale su identidad:

| Marca | Significado |
|---|---|
| ✅ | La wiki describe **este** sonido y su uso; el archivo encaja por nombre y función |
| 🔶 | La wiki describe el uso, pero **qué archivo concreto** es, es deducción mía |
| ⚠ | **Hay que verificarlo**: o la descripción de la wiki no encaja con el uso que le damos, o no hay entrada en la wiki |
| — | Uso propio de este fangame; la wiki no lista ese sonido |

Tras la verificación a oído ya **no queda ninguna fila marcada ⚠ ni 🔶**: las 45 están
confirmadas. Las marcas se conservan en la leyenda por si se añade material nuevo.

### En el juego (45)

| Archivo | Suena cuando | Duración | Se reproduce | Nombre original | Verificación |
|---|---|---|---|---|---|
| `accion-denegada.mp3` | acción denegada | 0.42 s | completo | `error.mp3` | — · uso propio del fangame (puerta atascada); la wiki no lista ese sonido |
| `accion-puerta.mp3` | abrir o cerrar una puerta de la oficina | 2.35 s | solo los primeros **0.6 s** | `SFXBible_12478.mp3` | ✅ · «accion de cerrar/abrir las puertas» |
| `ambiente-apagon.mp3` | ambiente del apagón, desde que se va la luz hasta el susto o las 6 AM | 60.08 s | en bucle | `ambience2.mp3` | ✅ · *Ambience2* = ambiente del apagón |
| `ambiente-oficina.mp3` | ambiente principal de la oficina, toda la noche | 115.51 s | en bucle | `ColdPresc-B.mp3` | ✅ · *Cold Presence B* = ambiente principal de la noche |
| `amenaza-cerca.mp3` | amenaza cerca: **30 %** con un animatrónico en el pasillo, **50 %** con dos, **75 %** con tres, **100 %** si Freddy está en la oficina | 114.91 s | en bucle, volumen según la amenaza | `EerieAmbienceLargeSca_MV005.mp3` | ✅ · *Giant Hollow Tube Sector*, con la escalera 30/50/75/100 % |
| `bajar-monitor.mp3` | bajar el monitor | 0.89 s | completo | `put-down.mp3` | ✅ · «subir/bajar el monitor»  |
| `cambiar-camara.mp3` | cambiar de cámara | 0.29 s | completo | `blip3.mp3` | ✅ · «cambiar de cámara» |
| `campanas-6am.mp3` | campanas de las 6 AM | 17.29 s | completo | `chimes-2.mp3` | ✅ · «campanas al finalizar una noche» |
| `carrera-pasillo-1.mp3` | carrera de IShowSpeed | 2.66 s | completo | `run.mp3` | ✅ · «carrera de IShowSpeed» |
| `carrera-pasillo-2.mp3` | carrera de IShowSpeed | 2.32 s | completo | `running-fast3.mp3` | ✅ · idem |
| `estatica-del-monitor-larga.mp3` | estática del monitor (bucle, alternativa) | 33.72 s | en bucle | `static2.mp3` | ✅ · «estatica que se reproduce en el menu principal que va disminuyendo» |
| `estatica-del-monitor.mp3` | estática del monitor (bucle) | 10.92 s | en bucle | `static.mp3` | ✅ · «estatica que suena justo despues del jumpscare» |
| `fin-de-la-llamada.mp3` | la cinta sale al terminar la llamada | 16.72 s | solo los primeros **1.5 s** | `MiniDV_Tape_Eject_1.mp3` |✅ · «estatica que se reproduce en cada camara» |
| `glitch-noche-6.mp3` | glitch digital aleatorio, **solo en la noche 6** | 8.10 s | solo los primeros **0.8 s** | `COMPUTER_DIGITAL_L2076505.mp3` | ✅ · glitch aleatorio en la noche 6 |
| `golpes-en-la-puerta.mp3` | golpes contra la puerta cerrada | 6.74 s | solo los primeros **1.4 s** | `DOOR_POUNDING_ME_D0291401.mp3` | ✅ · «Foxy golpeando la puerta izquierda de la oficina» |
| `grito-golden-freddy.mp3` | jumpscare de Golden Freddy (el grito **lento**, no el normal) | 15.93 s | completo | `XSCREAM2.mp3` | ✅ · «Jumpscare de Golden Freddy» |
| `interferencia-camara-1.mp3` | interferencia cuando se mueve un animatronico | 4.15 s | solo los primeros **.55 s** | `garble1.mp3` | ✅ · «señal de las cámaras interrumpida», 3 variantes |
| `interferencia-camara-2.mp3` | interferencia cuando se mueve un animatronico | 5.98 s | solo los primeros **.55 s** | `garble2.mp3` | ✅ · idem |
| `interferencia-camara-3.mp3` | interferencia cuando se mueve un animatronico | 4.26 s | solo los primeros **.55 s** | `garble3.mp3` | ✅ · idem |
| `jumpscare.mp3` | jumpscare | 5.33 s | completo | `XSCREAM.mp3` | ✅ · «sonido del jumpscare de los animatrónicos» |
| `llaman-a-la-puerta.mp3` | un animatrónico llega a la puerta | 3.42 s | completo | `knock2.mp3` | ✅ · «Foxy golpeando la puerta izquierda de la oficina» |
| `marcha-toreador-apagon.mp3` | Freddy toca la Marcha del Toreador al irse la luz | 233.42 s | completo | `music_box.mp3` | ✅ · *Toreador March* (Bizet, muestra 1905 Regina Music Box) |
| `musica-pirate-cove.mp3` | Pirate Cove la primera vez que abres la CAM 5 | 9.74 s | completo | `pirate-song2.mp3` | ✅ · «Foxy cantando» en Pirate Cove (el juego debe jugar en donde esta la camara para poder poner el sonido en cualquier momento y que se escuche en 3D) |
| `organo-de-circo.mp3` | órgano de circo, ocasionalmente durante la noche | 22.20 s | completo | `circus.mp3` | ✅ · «música de circo al azar cuando un animatrónico está activo» (el juego debe jugar en donde esta la camara para poder poner el sonido en cualquier momento y que se escuche en 3D, se posiciona en la camara 1B) |
| `pasos-pasillo.mp3` | pasos por el pasillo | 7.89 s | solo los primeros **.9 s** | `deep-steps.mp3` | ✅ · «pasos de Bonnie y Chica» |
| `publico-de-la-intro.mp3` | público en la intro del periódico | 3.47 s | completo | `CROWD_SMALL_CHIL_EC049202.mp3` | ✅ · «niños gritando al finalizar una noche» |
| `respiracion-en-la-puerta-1.mp3` | respiración en la puerta | 3.27 s | completo | `Vocals_Breaths_S_35972006.mp3` | ✅ · *gemidos* al entrar en la oficina con el monitor subido |
| `respiracion-en-la-puerta-2.mp3` | respiración en la puerta | 6.06 s | completo | `Vocals_Breaths_S_35972008.mp3` | ✅ · idem |
| `respiracion-en-la-puerta-3.mp3` | respiración en la puerta | 2.72 s | completo | `Vocals_Breaths_S_35972012.mp3` | ✅ · idem |
| `respiracion-en-la-puerta-4.mp3` | respiración en la puerta | 3.76 s | completo | `Vocals_Breaths_S_35972014.mp3` | ✅ · idem |
| `risa-alucinacion-1.mp3` | risa (alucinación) | 2.25 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_1.mp3` | ✅ · sonido aleatorio de ambiente |
| `risa-alucinacion-2.mp3` | risa lenta de Freddy al moverse, y alucinación | 5.62 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_1d.mp3` | ✅ · risa de Freddy al moverse |
| `risa-alucinacion-3.mp3` | risa lenta de Freddy al moverse, y alucinación | 8.07 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_2d.mp3` | ✅ · idem |
| `risa-alucinacion-4.mp3` | risa lenta de Freddy al moverse, y alucinación | 5.67 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_8d.mp3` | ✅ · idem |
| `ruidos-cocina-1.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 7.76 s | completo | `OVEN-DRA_1_GEN-HDF18119.mp3` | ✅ · «ruidos de Chica en la Kitchen», 4 variantes (el juego debe jugar en donde esta la camara para poder poner el sonido en cualquier momento y que se escuche en 3D) |
| `ruidos-cocina-2.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 5.09 s | completo | `OVEN-DRA_2_GEN-HDF18120.mp3` | ✅ · idem |
| `ruidos-cocina-3.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 10.34 s | completo | `OVEN-DRA_7_GEN-HDF18121.mp3` | ✅ · idem |
| `ruidos-cocina-4.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 5.36 s | completo | `OVEN-DRAWE_GEN-HDF18122.mp3` | ✅ · idem |
| `se-va-la-luz.mp3` | se va la luz | 18.91 s | completo | `powerdown.mp3` | ✅ · «cuando se corta la energía del establecimiento» |
| `subir-monitor.mp3` | subir el monitor | 5.15 s | solo los primeros **.7 s** | `CAMERA_VIDEO_LOA_60105303.mp3` | ✅ · «levantando el monitor» |
| `susto-puerta-iluminada.mp3` | enciendes la luz del pasillo y hay un animatrónico en esa puerta | 4.31 s | solo los primeros **1.2 s** | `windowscare.mp3` | ✅ · cuando aparece un animatronico en tu puerta iluminandolo |
| `susurro-alucinacion.mp3` | susurro (alucinación) | 15.12 s | solo los primeros **2.2 s** | `whispering2.mp3` | ✅ · sonido aleatorio de ambiente cuando un animatronico esta cerca |
| `voz-robotica-pasillo.mp3` | Bonnie o Chica en las esquinas de los pasillos, **solo desde la 4.ª noche** | 15.10 s | completo | `robotvoice.mp3` | ✅ · «voz robótica» de las esquinas desde la 4.ª noche (el juego debe jugar en donde esta la camara para poder poner el sonido en cualquier momento y que se escuche en 3D, se posiciona en la camara 2B y 4B) |
| `zumbido-luces-pasillo.mp3` | luces de los pasillos encendidas | 8.72 s | en bucle | `BallastHumMedium2.mp3` | ✅ · «sonido de las luces de los pasillos» |
| `zumbido-ventilador.mp3` | zumbido del ventilador (bucle) | 9.69 s | en bucle | `Buzz_Fan_Florescent2.mp3` | ✅ · «sonidos provocados por el ventilador y la luz» |

### Sin asignar (1)

| Archivo | Nombre original | Por qué no está asignado | Verificación |
|---|---|---|---|
| `tema-menu-fnaf1.mp3` | `darkness-music.mp3` | es el **tema del menú** original (*Urban Darkness Part 08*, Bjørn Lynne) según [la wiki](https://freddy-fazbears-pizza.fandom.com/wiki/Soundtrack_(FNaF1)); el juego usa su propio tema de título | ✅ · *Urban Darkness Part 08* = tema del menú de Steam |

Si un mp3 falta o no se puede decodificar, cada efecto cae en su versión
sintetizada (`synthXxx`) y el juego sigue funcionando igual que antes.

## Atribución obligatoria

- Los recursos de audio e imagen procedentes de *Five Nights at Freddy's*
  pertenecen a **Scott Cawthon**, creador del juego original.
- El universo, los personajes y la marca *Skibidi Toilet* pertenecen a
  **DaFuqBoom**.
- Este proyecto es un **fangame gratuito y sin ánimo de lucro**, no oficial y
  sin afiliación, patrocinio ni respaldo de ninguno de los dos.

## Sin monetización

Ningún recurso de esta carpeta puede usarse en una versión de pago, con
publicidad, con micropagos o con enlaces de donación. Es la condición bajo la
que la comunidad de FNAF puede trabajar con los recursos del juego original.

## Añadir recursos nuevos

1. Comprueba que tienes derecho a usarlos (obra propia, licencia compatible o
   recurso del juego original dentro de un fangame sin ánimo de lucro).
2. Añade la fila correspondiente en la tabla de procedencia de arriba.
3. Si trae su propia licencia (como las tipografías OFL), incluye el texto en
   esta carpeta, igual que `fonts/OFL.txt`.
