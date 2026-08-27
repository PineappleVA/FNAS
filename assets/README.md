# `assets/` — recursos multimedia

> ⚠️ **Esta carpeta NO está cubierta por la licencia del código.**
> El `LICENSE` (MIT) de la raíz se aplica solo al HTML/CSS/JS del proyecto.
> Nada de lo que hay aquí puede redistribuirse bajo esa licencia: no somos sus
> titulares y no tenemos derecho a cederlo. Detalles en [`../NOTICE`](../NOTICE).

Contenido servido junto a las páginas: los tres builds lo cargan con rutas
relativas (`assets/...`), ya no va incrustado en base64 dentro del HTML.

## Procedencia

| Archivo | Contenido | Procedencia / licencia |
|---|---|---|
| `fonts/creepster-400.woff2` | tipografía Creepster | © 2011 Font Diner, Inc · **SIL OFL 1.1** → [`fonts/OFL.txt`](fonts/OFL.txt) |
| `fonts/vt323-400-latin.woff2`<br>`fonts/vt323-400-latin-ext.woff2` | tipografía VT323 (subconjuntos latin y latin-ext) | © 2011 The VT323 Project Authors · **SIL OFL 1.1** → [`fonts/OFL.txt`](fonts/OFL.txt) |
| `img/splash-logo.png` | logo del splash («Pineapple presenta») | Equipo Pineapple · obra propia |
| `img/newspaper-intro.png` | periódico «Skibiry Herald» de la intro | Scott Cawthon · obra mixeada |
| `audio/title-theme.m4a` | música de la pantalla de título | Scott Cawthon · obra propia |
| `audio/click.mp3` | clic de interfaz | Equipo Pineapple · obra propia |
| `audio/phone/night1-4.mp3` | llamadas de teléfono de cada noche (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| `audio/phone-unreleased/night1-4.mp3` | llamadas de teléfono de la compilación Unreleased | Equipo Pineapple · obra propia |
| `audio/fnaf1/*.mp3` (46) | efectos y música del **FNAF 1** integrados en el motor | recursos de audio de **Five Nights at Freddy's** → **Scott Cawthon** · ⛔ no redistribuir |

**Regla general:** mientras una fila no esté confirmada como obra propia, el
archivo se trata como recurso de terceros y queda **excluido** de la licencia
del código. Las filas marcadas con ⚠️ son las que el equipo debe revisar y
completar; si un recurso resulta ser propio, basta con cambiar su fila.

Los binarios idénticos entre builds se guardan una sola vez y se comparten:
el logo, el periódico, la música del título y el clic son los mismos ficheros
para las tres versiones.

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
para poder rastrear la procedencia; los que empiezan por `sin-usar-` están en la
carpeta pero no se disparan en el juego.

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

### En el juego (42)

| Archivo | Suena cuando | Duración | Se reproduce | Nombre original |
|---|---|---|---|---|
| `accion-denegada.mp3` | acción denegada | 0.21 s | completo | `error.mp3` |
| `ambiente-apagon.mp3` | ambiente del apagón, desde que se va la luz hasta el susto o las 6 AM | 30.04 s | en bucle | `ambience2.mp3` |
| `ambiente-oficina.mp3` | ambiente principal de la oficina, toda la noche | 115.51 s | en bucle | `ColdPresc-B.mp3` |
| `amenaza-cerca.mp3` | amenaza cerca: **30 %** con un animatrónico en el pasillo, **50 %** con dos, **75 %** con tres, **100 %** si Freddy está en la oficina | 57.47 s | en bucle, volumen según la amenaza | `EerieAmbienceLargeSca_MV005.mp3` |
| `bajar-monitor.mp3` | bajar el monitor | 0.44 s | completo | `put-down.mp3` |
| `cambiar-camara.mp3` | cambiar de cámara | 0.16 s | completo | `blip3.mp3` |
| `campanas-6am.mp3` | campanas de las 6 AM | 8.65 s | completo | `chimes-2.mp3` |
| `carrera-pasillo-1.mp3` | carrera de IShowSpeed | 1.33 s | completo | `run.mp3` |
| `carrera-pasillo-2.mp3` | carrera de IShowSpeed | 1.18 s | completo | `running-fast3.mp3` |
| `estatica-del-monitor-larga.mp3` | estática del monitor (bucle, alternativa) | 16.88 s | en bucle | `static2.mp3` |
| `estatica-del-monitor.mp3` | estática del monitor (bucle) | 5.46 s | en bucle | `static.mp3` |
| `fin-de-la-llamada.mp3` | la cinta sale al terminar la llamada | 8.36 s | solo los primeros **1.5 s** | `MiniDV_Tape_Eject_1.mp3` |
| `golpes-en-la-puerta.mp3` | golpes contra la puerta cerrada | 3.37 s | solo los primeros **1.4 s** | `DOOR_POUNDING_ME_D0291401.mp3` |
| `grito-golden-freddy.mp3` | jumpscare de Golden Freddy (el grito **lento**, no el normal) | 7.97 s | completo | `XSCREAM2.mp3` |
| `interferencia-camara-1.mp3` | interferencia al cambiar de sala | 2.09 s | solo los primeros **.55 s** | `garble1.mp3` |
| `interferencia-camara-2.mp3` | interferencia al cambiar de sala | 3.00 s | solo los primeros **.55 s** | `garble2.mp3` |
| `interferencia-camara-3.mp3` | interferencia al cambiar de sala | 2.14 s | solo los primeros **.55 s** | `garble3.mp3` |
| `jumpscare.mp3` | jumpscare | 2.66 s | completo | `XSCREAM.mp3` |
| `llaman-a-la-puerta.mp3` | un animatrónico llega a la puerta | 1.72 s | completo | `knock2.mp3` |
| `marcha-toreador-apagon.mp3` | Freddy toca la Marcha del Toreador al irse la luz | 233.42 s | completo | `music_box.mp3` |
| `musica-pirate-cove.mp3` | Pirate Cove la primera vez que abres la CAM 5 | 4.88 s | completo | `pirate-song2.mp3` |
| `organo-de-circo.mp3` | órgano de circo, ocasionalmente durante la noche | 6.20 s | completo | `circus.mp3` |
| `pasos-pasillo.mp3` | pasos por el pasillo | 7.89 s | solo los primeros **.9 s** | `deep-steps.mp3` |
| `publico-de-la-intro.mp3` | público en la intro del periódico | 1.75 s | completo | `CROWD_SMALL_CHIL_EC049202.mp3` |
| `respiracion-en-la-puerta-1.mp3` | respiración en la puerta | 1.65 s | completo | `Vocals_Breaths_S_35972006.mp3` |
| `respiracion-en-la-puerta-2.mp3` | respiración en la puerta | 3.03 s | completo | `Vocals_Breaths_S_35972008.mp3` |
| `respiracion-en-la-puerta-3.mp3` | respiración en la puerta | 1.36 s | completo | `Vocals_Breaths_S_35972012.mp3` |
| `respiracion-en-la-puerta-4.mp3` | respiración en la puerta | 1.88 s | completo | `Vocals_Breaths_S_35972014.mp3` |
| `risa-alucinacion-1.mp3` | risa (alucinación) | 1.12 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_1.mp3` |
| `risa-alucinacion-2.mp3` | risa lenta de Freddy al moverse, y alucinación | 2.82 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_1d.mp3` |
| `risa-alucinacion-3.mp3` | risa lenta de Freddy al moverse, y alucinación | 4.05 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_2d.mp3` |
| `risa-alucinacion-4.mp3` | risa lenta de Freddy al moverse, y alucinación | 2.85 s | solo los primeros **2 s** | `Laugh_Giggle_Girl_8d.mp3` |
| `ruidos-cocina-1.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 3.89 s | completo | `OVEN-DRA_1_GEN-HDF18119.mp3` |
| `ruidos-cocina-2.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 2.56 s | completo | `OVEN-DRA_2_GEN-HDF18120.mp3` |
| `ruidos-cocina-3.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 5.17 s | completo | `OVEN-DRA_7_GEN-HDF18121.mp3` |
| `ruidos-cocina-4.mp3` | Chica moviéndose por la cocina (CAM 6, que no tiene imagen) | 2.69 s | completo | `OVEN-DRAWE_GEN-HDF18122.mp3` |
| `se-va-la-luz.mp3` | se va la luz | 9.34 s | completo | `powerdown.mp3` |
| `subir-monitor.mp3` | subir el monitor | 2.59 s | solo los primeros **.7 s** | `CAMERA_VIDEO_LOA_60105303.mp3` |
| `susurro-alucinacion.mp3` | susurro (alucinación) | 7.58 s | solo los primeros **2.2 s** | `whispering2.mp3` |
| `voz-robotica-pasillo.mp3` | Bonnie o Chica en las esquinas de los pasillos, **solo desde la 4.ª noche** | 7.55 s | completo | `robotvoice.mp3` |
| `zumbido-luces-pasillo.mp3` | luces de los pasillos encendidas | 4.36 s | en bucle | `BallastHumMedium2.mp3` |
| `zumbido-ventilador.mp3` | zumbido del ventilador (bucle) | 4.86 s | en bucle | `Buzz_Fan_Florescent2.mp3` |

### Sin asignar (4)

| Archivo | Nombre original | Por qué no está asignado |
|---|---|---|
| `sin-usar-golpe-corto.mp3` | `SFXBible_12478.mp3` | la wiki describe unos «golpes que pueden ser escuchados cada cierto tiempo», pero no da el archivo: identificarlo por el nombre sería una conjetura |
| `sin-usar-secuencia-digital.mp3` | `COMPUTER_DIGITAL_L2076505.mp3` | uso sin identificar |
| `sin-usar-susto-ventana.mp3` | `windowscare.mp3` | su página de la wiki redirige a *Grimm Foxy* (Help Wanted): no es un sonido del FNAF 1 |
| `tema-menu-fnaf1.mp3` | `darkness-music.mp3` | es el **tema del menú** original (*Urban Darkness Part 08*, Bjørn Lynne) según [la wiki](https://freddy-fazbears-pizza.fandom.com/wiki/Soundtrack_(FNaF1)); el juego usa su propio tema de título |

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
