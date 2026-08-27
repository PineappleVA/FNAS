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

**Regla que sigue el motor: una muestra nunca dura más que el evento que la
dispara.** El glitch visual de una cámara dura 280–620 ms, así que los `garble`
(2–3 s) se recortan a 0,55 s; el golpe en la puerta anima 380 ms + 1100 ms de
retirada, así que `DOOR_POUNDING` (3,37 s) se recorta a 1,40 s. Los recortes y
los *cooldowns* están en la tabla `SFX` del HTML, en un solo sitio.

Para comprobar de oído que cada sonido está donde debe: **[`audio-test.html`](../audio-test.html)**
lista los 46 archivos con el evento que los dispara y su recorte.

### En el juego (34)

| Archivo | Suena cuando | Duración | Se reproduce |
|---|---|---|---|
| `Buzz_Fan_Florescent2.mp3` | zumbido del ventilador (bucle) | 4.86 s | en bucle |
| `CAMERA_VIDEO_LOA_60105303.mp3` | subir el monitor | 2.59 s | solo los primeros **.7 s** |
| `CROWD_SMALL_CHIL_EC049202.mp3` | publico en la intro | 1.75 s | completo |
| `DOOR_POUNDING_ME_D0291401.mp3` | golpes contra la puerta cerrada | 3.37 s | solo los primeros **1.4 s** |
| `EerieAmbienceLargeSca_MV005.mp3` | ambiente tenso con poca energía | 57.47 s | completo |
| `Laugh_Giggle_Girl_1.mp3` | risa (alucinación) | 1.12 s | solo los primeros **2 s** |
| `Laugh_Giggle_Girl_1d.mp3` | risa (alucinación) | 2.82 s | solo los primeros **2 s** |
| `Laugh_Giggle_Girl_2d.mp3` | risa (alucinación) | 4.05 s | solo los primeros **2 s** |
| `Laugh_Giggle_Girl_8d.mp3` | risa (alucinación) | 2.85 s | solo los primeros **2 s** |
| `MiniDV_Tape_Eject_1.mp3` | fin de la llamada | 8.36 s | solo los primeros **1.5 s** |
| `Vocals_Breaths_S_35972006.mp3` | respiracion en la puerta | 1.65 s | completo |
| `Vocals_Breaths_S_35972008.mp3` | respiracion en la puerta | 3.03 s | completo |
| `Vocals_Breaths_S_35972012.mp3` | respiracion en la puerta | 1.36 s | completo |
| `Vocals_Breaths_S_35972014.mp3` | respiracion en la puerta | 1.88 s | completo |
| `XSCREAM.mp3` | jumpscare | 2.66 s | completo |
| `ambience2.mp3` | ambiente de la oficina (bucle) | 30.04 s | en bucle |
| `blip3.mp3` | cambiar de cámara | 0.16 s | completo |
| `chimes-2.mp3` | campanas de las 6 AM | 8.65 s | completo |
| `circus.mp3` | música de fiesta en la intro | 11.10 s | solo los primeros **6.2 s** |
| `darkness-music.mp3` | marcha del Toreador durante el apagón | 62.41 s | completo |
| `deep-steps.mp3` | pasos por el pasillo | 7.89 s | solo los primeros **.9 s** |
| `error.mp3` | accion denegada | 0.21 s | completo |
| `garble1.mp3` | interferencia al cambiar de sala | 2.09 s | solo los primeros **.55 s** |
| `garble2.mp3` | interferencia al cambiar de sala | 3.00 s | solo los primeros **.55 s** |
| `garble3.mp3` | interferencia al cambiar de sala | 2.14 s | solo los primeros **.55 s** |
| `knock2.mp3` | un animatrónico llega a la puerta | 1.72 s | completo |
| `pirate-song2.mp3` | música del Pirate Cove | 4.88 s | completo |
| `powerdown.mp3` | se va la luz | 9.34 s | completo |
| `put-down.mp3` | bajar el monitor | 0.44 s | completo |
| `run.mp3` | carrera de IShowSpeed | 1.33 s | completo |
| `running-fast3.mp3` | carrera de IShowSpeed | 1.18 s | completo |
| `static.mp3` | estática del monitor (bucle) | 5.46 s | en bucle |
| `static2.mp3` | estática del monitor (bucle, alternativa) | 16.88 s | en bucle |
| `whispering2.mp3` | susurro (alucinación) | 7.58 s | solo los primeros **2.2 s** |

### Sin asignar (12)

Están en la carpeta y se pueden escuchar en la página de pruebas, pero no se
disparan en el juego. Asignarlos es una línea en la tabla `SFX`.

| Archivo | Por qué no está asignado |
|---|---|
| `BallastHumMedium2.mp3` | zumbido de 4,36 s; la luz se pulsa constantemente y lo saturaba |
| `COMPUTER_DIGITAL_L2076505.mp3` | uso sin identificar |
| `ColdPresc-B.mp3` | 1:55 sin uso identificado |
| `OVEN-DRAWE_GEN-HDF18122.mp3` | idem |
| `OVEN-DRA_1_GEN-HDF18119.mp3` | candidatas a puerta, pero duran 2,6-5,2 s para una pulsacion de ~200 ms y no esta confirmado que sean la puerta del FNAF 1 |
| `OVEN-DRA_2_GEN-HDF18120.mp3` | idem |
| `OVEN-DRA_7_GEN-HDF18121.mp3` | idem |
| `SFXBible_12478.mp3` | uso sin identificar |
| `XSCREAM2.mp3` | segundo grito; de reserva |
| `music_box.mp3` | pista de 3:53; cualquier recorte seria arbitrario |
| `robotvoice.mp3` | peleaba con el Toreador durante el apagon |
| `windowscare.mp3` | uso en el FNAF 1 sin identificar |

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
