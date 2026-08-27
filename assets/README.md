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

Se cargan por `fetch` + `decodeAudioData` y se reproducen sobre el bus maestro
del motor. **Cada efecto conserva su versión sintetizada como respaldo**: si un
archivo falta o no se puede decodificar, suena el efecto por Web Audio y el
juego sigue funcionando igual.

| Archivo | Para qué se usa | Función |
|---|---|---|
| `OVEN-DRA_2_GEN-HDF18120.mp3` | Puerta al cerrarse/abrirse (varía entre 4 muestras) | `sndDoor()` |
| `OVEN-DRA_1_GEN-HDF18119.mp3` | Puerta (variante) | `sndDoor()` |
| `OVEN-DRAWE_GEN-HDF18122.mp3` | Puerta (variante) | `sndDoor() |
| `OVEN-DRA_7_GEN-HDF18121.mp3` | Puerta (variante) | `sndDoor() |
| `DOOR_POUNDING_ME_D0291401.mp3` | Golpes contra la puerta cerrada | `sndDoorBang()` |
| `knock2.mp3` | Llaman a la puerta: un animatrónico ha llegado | `sndKnock()` |
| `error.mp3` | Acción denegada / puerta atascada | `sndDoorJam()` |
| `CAMERA_VIDEO_LOA_60105303.mp3` | Subir el monitor | `sndCamUp(true)` |
| `put-down.mp3` | Bajar el monitor | `sndCamUp(false)` |
| `blip3.mp3` | Blip al cambiar de cámara | `sndCamSwitch()` |
| `garble1.mp3` | Interferencia al cambiar de sala | `sndCamGlitch()` |
| `garble2.mp3` | Interferencia al cambiar de sala | `sndCamGlitch()` |
| `garble3.mp3` | Interferencia al cambiar de sala | `sndCamGlitch()` |
| `static.mp3` | Estática del monitor, en bucle mientras está subido | `startCamStatic()` |
| `static2.mp3` | Interferencia fuerte (alguien se mueve mientras miras) | `sndCamGlitch(true)` |
| `Vocals_Breaths_S_35972006.mp3` | Respiración en la puerta | `sndBreath()` |
| `Vocals_Breaths_S_35972008.mp3` | Respiración en la puerta | `sndBreath()` |
| `Vocals_Breaths_S_35972012.mp3` | Respiración en la puerta | `sndBreath()` |
| `Vocals_Breaths_S_35972014.mp3` | Respiración en la puerta | `sndBreath()` |
| `run.mp3` | Carrera de IShowSpeed por el pasillo | `sndFoxyRun()` |
| `running-fast3.mp3` | Carrera de IShowSpeed por el pasillo | `sndFoxyRun()` |
| `deep-steps.mp3` | Pasos por el pasillo | `sndFootsteps()` |
| `XSCREAM.mp3` | Jumpscare | `sndJumpscare()` |
| `XSCREAM2.mp3` | Jumpscare (variante) | `sndJumpscare(true)` |
| `robotvoice.mp3` | «¡LET'S EAT!» durante el apagón | `sndRobotVoice()` |
| `whispering2.mp3` | Susurro: alucinación sonora | `maybeHallucinationSfx()` |
| `Laugh_Giggle_Girl_1.mp3` | Risa de niña: alucinación sonora | `maybeHallucinationSfx()` |
| `Laugh_Giggle_Girl_1d.mp3` | Risa de niña: alucinación sonora | `maybeHallucinationSfx()` |
| `Laugh_Giggle_Girl_2d.mp3` | Risa de niña: alucinación sonora | `maybeHallucinationSfx()` |
| `Laugh_Giggle_Girl_8d.mp3` | Risa de niña: alucinación sonora | `maybeHallucinationSfx()` |
| `windowscare.mp3` | Aparición de Golden Skibidi | `sndScareFlash()` |
| `ambience2.mp3` | Ambiente de la oficina (30 s), en bucle | `startAmbienceBed()` |
| `Buzz_Fan_Florescent2.mp3` | Zumbido del ventilador, en bucle | `startFanHum()` |
| `BallastHumMedium2.mp3` | Zumbido del fluorescente al encender la luz | `sndLight()` |
| `EerieAmbienceLargeSca_MV005.mp3` | Ambiente tenso cuando queda poca energía | `startAmbience()` |
| `powerdown.mp3` | Se va la luz | `sndPowerDown()` |
| `chimes-2.mp3` | Campanadas de las 6 AM | `sndSixAM()` |
| `darkness-music.mp3` | Marcha del Toreador durante el apagón | `sndFreddyTune()` |
| `pirate-song2.mp3` | Música del Pirate Cove la primera vez que abres la CAM 5 | `sndPirateCove()` |
| `circus.mp3` | Música de fiesta en la intro del periódico | `sndPartyCrowd()` |
| `CROWD_SMALL_CHIL_EC049202.mp3` | Ambiente de público en la intro del periódico | `sndPartyCrowd()` |
| `COMPUTER_DIGITAL_L2076505.mp3` | Pantalla «12:00 AM» al empezar la noche | `sndNightStart()` |
| `MiniDV_Tape_Eject_1.mp3` | La cinta sale: fin de la llamada del encargado | `startPhoneCall()` |
| `music_box.mp3` | Caja de música de Golden Skibidi (se recorta a 6,2 s) | `maybeGoldenSkibidi()` |

Sin asignar (en el pack, pero no he podido identificar su uso en el FNAF 1;
quedan disponibles por si el equipo les encuentra sitio):

- `ColdPresc-B.mp3`
- `SFXBible_12478.mp3`

Las ganancias de cada muestra están en la tabla `SFX_VOL` del HTML, en un solo
sitio, para poder afinarlas sin tocar el resto del código.

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
