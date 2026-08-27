# Balance y diseño — FNAF Skibidi v3.0 *(build de producción)*

Documento del estado **actual** del juego. Refleja el código tal y como está ahora mismo;
no es un historial de cambios.

---

## 1. Reglas de muerte

**Con el monitor levantado nadie te mata.** Como en FNAF, el animatrónico que llega a tu puerta se
queda esperando y su temporizador de muerte no corre mientras miras las cámaras. El jumpscare solo
puede ocurrir con el monitor **bajado**.

**Pero esconderse no es una estrategia.** Si aguantas el monitor arriba con alguien esperando en una
puerta abierta, el juego **te lo baja a la fuerza**. Unos instantes antes la señal se degrada con un
glitch y un pitido, como aviso, y al arrancártelo la pantalla da un tirón seco.

| Dificultad | N1 | N2 | N3 | N4 | N5 | N6 |
|---|---|---|---|---|---|---|
| Normal | 5,0 s | 4,8 s | 4,6 s | 4,4 s | 4,2 s | 4,0 s |
| Medio | 4,0 s | 3,8 s | 3,7 s | 3,5 s | 3,4 s | 3,2 s |
| Difícil | 3,2 s | 3,1 s | 2,9 s | 2,8 s | 2,7 s | 2,6 s |

*Tiempo que puedes campear antes de que te bajen el monitor.*

Una vez abajo, el margen para cerrar la puerta antes de morir (**grace period**):

| Dificultad | N1 | N2 | N3 | N4 | N5 | N6 |
|---|---|---|---|---|---|---|
| Normal | 6609 ms | 6319 | 6005 | 5797 | 5532 | 5266 |
| Medio | 5575 ms | 5366 | 5224 | 4927 | 4719 | 4504 |
| Difícil | 4510 ms | 4307 | 4143 | 3903 | 3787 | 3581 |

**IShowSpeed tiene su propio margen**, más corto porque ataca sin aviso pero ya no instantáneo:
2300 / 2800 / 3400 ms de base por `[1, 1, .96, .92, .88, .84, .80]` — en N6 son 1840 / 2240 / 2720 ms.
Cada tramo de su sprint (3→4→11→puerta) dura 1250 / 1450 / 1700 ms, así que da tiempo a verlo llegar
por las cámaras.

Se amplió respecto al ajuste anterior — antes Difícil N6 daba 2122 ms, ahora 3550 ms — y la caída
por noche es más suave (`×0,80` en N6 en vez de `×0,64`), así que incluso la última noche deja tiempo
real de reacción. Speed pasó de 700 ms a **1500 ms** de margen.

**La puerta cerrada protege siempre**, sin excepciones (verificado 300/300).

### Puertas y luces: para qué sirve cada una

Las dos cosas tienen funciones distintas y no intercambiables:

- **La luz solo REVELA.** Enciéndela y ves quién está esperando en tu puerta, iluminado y con su
  sombra proyectada en la pared. La luz **nunca** lo espanta: antes se iba por su cuenta un 35 % de
  las veces, lo que convertía el botón de luz en una ruleta y hacía que cerrar la puerta fuera
  opcional.
- **Cerrar la puerta AHUYENTA.** Es la única forma de quitártelo de encima. Golpea la chapa, se
  sacude la puerta y a los 1,1 s se retira al pasillo anterior.

Si **abres antes de que se complete la retirada**, sigue ahí esperando: no basta con dar un toque al
botón. Y sin luz encendida el animatrónico no es invisible — se intuye su **silueta en penumbra**, así
que sabes que hay algo pero no quién. No hay ojos rojos ni ningún otro indicador: solo la sombra.

### Las dos puertas, y su ventanilla
La ventanilla está **recortada en la propia chapa** de cada puerta (no es un adorno superpuesto): se
mueve, se escala y desaparece con ella. Con la puerta cerrada enciendes la luz y **ves quién hay
fuera** por el hueco. Ya no estás ciego tras cerrar.

Y cada puerta es **distinta**, para que el lado izquierdo y el derecho no sean espejos:

| | Izquierda (W-01) | Derecha (E-02) |
|---|---|---|
| Ventanilla | ancha y baja (2,7:1) | estrecha y alta (0,9:1) |
| Vidrio | malla de alambre cuadrada | barrotes verticales gruesos |
| Chapa | gris azulado, bandas anchas | verde grisáceo, bandas finas y juntas |
| Herraje | tirador vertical | barra antipánico horizontal |
| Placa | abajo a la izquierda | arriba a la derecha |

### Respiración en la puerta
Si hay alguien esperando fuera **se le oye respirar por ese lado** (audio panoramizado a izquierda o
derecha) aunque no enciendas la luz. Con la puerta cerrada deja de oírse. Recompensa jugar con sonido.

### Puerta atascada
Machacar el botón de una puerta **atasca el mecanismo 2,6 s** (5 pulsaciones en menos de 4 s), avisado
con el LED en ámbar parpadeante. Corta el exploit de abrir y cerrar en bucle para no gastar batería;
el uso normal nunca lo dispara.

---

## 2. Energía

`powerTick()` — consumo por segundo, multiplicado por dificultad y noche:

- Base: `0,016 %`
- Cada puerta cerrada: `+0,205 %`
- Extra si ambas cerradas: `+0,075 %`
- Cada luz: `+0,09 %`
- Monitor levantado: `+0,085 %`

Multiplicador por dificultad: **Normal 1,08 · Medio 1,38 · Difícil 1,70**
Multiplicador por noche: `×1,00 → ×1,06 → ×1,13 → ×1,21 → ×1,31 → ×1,42`

**Coste total de una noche** (estrategia media: 22 % del tiempo una puerta, 12 % luz, 30 % monitor).
Tabla reproducida a partir del código con desviación 0 en las 18 celdas:
`6 h × base × curvaDeHora[noche] × multDificultad × curvaDeConsumo[noche] × 0,0974 %/s`.

| Dificultad | N1 | N2 | N3 | N4 | N5 | N6 |
|---|---|---|---|---|---|---|
| Normal | 44 % | 46 % | 48 % | 50 % | 53 % | 56 % |
| Medio | 55 % | 57 % | 59 % | 62 % | 66 % | 70 % |
| Difícil | 66 % | 68 % | 71 % | 75 % | 79 % | 84 % |

Curva monótona en ambos ejes y ninguna noche supera el 100 %: siempre se puede ganar gestionando bien,
pero Difícil N6 deja muy poco margen.

**Duración de la noche:** base `66 s/hora` en Difícil, `68 s` en Medio, `70 s` en Normal, por
`[1, 1, 0.98, 0.96, 0.94, 0.92, 0.90]`. Las tres duran casi lo mismo a propósito: si las noches
difíciles fueran más cortas, gastarían menos batería en total y saldrían *más fáciles*.

---

## 3. Animatrónicos

Niveles de IA por noche (máximo 20):

```
Skibidi Toilet   [0, 0,  3,  6, 10, 15, 20]
Cameraman        [0, 4,  8, 12, 16, 19, 20]
TV Woman         [0, 3,  7, 11, 15, 18, 20]
IShowSpeed       [0, 2,  5,  9, 14, 18, 20]
```

`calmFactor` (cuanto mayor, más tranquilos): **Difícil 22 · Medio 25 · Normal 29**.
Probabilidad de moverse por tick, media de los cuatro:

| Dificultad | N1 | N3 | N6 |
|---|---|---|---|
| Normal | 10,3 % | 32,7 % | 68,9 % |
| Medio | 12,0 % | 38,0 % | 80,0 % |
| Difícil | 13,6 % | 43,2 % | 90,9 % |

Intervalo de movimiento: base `1900 / 2900 / 4200 ms` por `[1, 1, .91, .84, .77, .70, .62]`.

**Observar una cámara frena pero no inmoviliza:** 55 % de probabilidad de que el animatrónico se
quede quieto, y solo 30 % en los pasillos de la oficina (CAM 2C / 4C). Congelarlos por completo
convertía el monitor en invulnerabilidad.

### IShowSpeed (Pirate Cove)

Carga por fases hasta lanzarse por el pasillo oeste. **Vigilar la CAM 5 es su contramedida real:**

| Dificultad | Ataques/noche ignorándolo | N6 vigilando el Cove |
|---|---|---|
| Normal | 1,7 (N1) → 16,4 (N6) | un ataque cada ~2441 s |
| Medio | 2,8 → 20,2 | ~1898 s |
| Difícil | 6,8 → 39,6 | ~18 s |

Su carga nunca baja de 5 pasos, vigilar el Cove funciona 14 ticks seguidos antes de que se impaciente,
el boost doble de Difícil exige IA ≥ 14 con 28 % de probabilidad, y su tick base es
`1300 / 1700 / 2200 ms` por `[1, 1, .95, .91, .87, .83, .79]`.

### Golden Skibidi

Aparición rara y opcional desde la Noche 3: se materializa en la oficina en tono dorado. Si te quedas
mirándolo te mata a los ~6 s; si levantas el monitor, se disipa. Probabilidad por comprobación:
**2 % Normal · 3,5 % Medio · 5,5 % Difícil**.

---

## 4. Estrellas y progresión

Las noches se desbloquean **en orden**. La Noche 6 está oculta hasta desbloquearse y se distingue
solo por su color.

| Dificultad | Noches 1-5 | Noche 6 |
|---|---|---|
| Normal | 1★ | 3★ |
| Medio | 2★ | 3★ |
| Difícil | 3★ | 3★ |

Se guarda siempre el mejor resultado obtenido en cada noche.

---

## 5. Presentación

### Oficina
Penumbra azul-verdosa, viñeta que cierra la sala, halo cálido de la lámpara sobre la pared y rejilla
en perspectiva en el suelo. Decoración deliberadamente sobria — reloj, dos luces de techo, rejilla de
ventilación, tablón de notas, un archivador y dos pósters — porque la oficina de FNAF está vacía.
Todos los iconos son formas CSS: la fuente VT323 no tiene emojis y se veían como cuadros vacíos.

### Nada de texto en la oficina
Mientras juegas **no hay ni una palabra en pantalla** aparte del HUD: todo se comunica con iconos y
luces, como en FNAF. Los botones de puerta y luz llevan solo su pictograma, el botón del monitor solo
su icono de pantalla, y el rótulo CERRADA / ABIERTA que había sobre cada marco es ahora una **barra
LED** que se enciende en rojo.

### Puertas y luces
Los botones van en un **panel metálico incrustado en el trozo de pared junto a cada puerta**, con
sombra interior, tornillos en las esquinas y teclas rehundidas. Cada tecla tiene su icono y un **LED**
que se enciende **rojo** al cerrar la puerta y **amarillo** al dar la luz. Las puertas son chapa
industrial con franjas de peligro y raíl superior, y se sacuden cuando alguien choca contra ellas.

### El animatrónico en la puerta
Se apoya en el suelo del pasillo, a escala del hueco, con **sombra de contacto** bajo los pies y
**sombra proyectada** en la pared cuando le da la luz. Al cerrarle la puerta en la cara se sacude y
retrocede hacia el fondo encogiéndose.

### Cámaras
- Barrido de encendido tipo CRT al cambiar de sala
- Deriva lenta del plano (ciclo de 26 s), banda de desincronización vertical y aberración cromática
- Carcasa con bisel, curvatura de cristal y reflejo

### Mapa
Planta real del local en vez de una lista de botones: los **pasillos son canales verdes** que conectan
las salas, el conducto de servicio va discontinuo, la **oficina está marcada en azul** al sur con sus
**dos puertas en rojo**, y un barrido de radar recorre el plano. Las dos cámaras de puerta (2C y 4C)
llevan borde rojo por ser las que avisan del peligro inmediato, y las salas solo con audio se ven
apagadas y con borde discontinuo. El mapa **no revela dónde están los animatrónicos**: hay que mirar.

Las 12 salas se montan con un sistema común de perspectiva: techo con vigas, pared del fondo, paredes
laterales en fuga y suelo con rejilla proyectada. Cada una tiene decorado propio (tarima y telón,
mesas en profundidad, estanterías con cabezas, cabinas, puerta iluminada al fondo...). Los
animatrónicos tienen carril propio y profundidades distintas para no taparse, se apoyan en el suelo
real y llevan sombra de contacto. Su tamaño es proporcional al feed, así que la escena se ve igual en
1024×768 que en 1920×1080.

### Animación del monitor
Al **subir**, el panel se despliega desde abajo con sobreexposición. Al **bajar**, la imagen cae y
colapsa en una línea horizontal brillante, como un CRT apagándose. Si te lo arrancan por campear, se
añade un tirón seco. Todo respeta el ajuste "Parpadeo de luces".

### Llamadas
Contestador de cinta: carretes girando, medidor VU que reacciona, piloto REC parpadeante y botón
SALTAR discreto.

### Pantalla de muerte
Fondo negro, el animatrónico que te mató ocupando la pantalla en penumbra con respiración lenta y una
brasa roja detrás. Solo la palabra GAME OVER, en rojo apagado — **sin subtítulo ni frase
explicativa**. Los botones aparecen a los 2 segundos.

---

## 6. Opciones

7 ajustes: llamadas de teléfono, ambiente de la oficina, filtro CRT, estática de cámara, parpadeo de
luces, sacudida de pantalla e intensidad de jumpscares. Más dificultad, volúmenes y la pantalla de
Versión con changelog (1.0, 2.0, 3.0) y barra fija que indica qué versión estás leyendo.

---

## 7. Verificación

### Playtest con bot (noches completas, tiempo real, sin acelerar)

| Dificultad | Resultado Noche 6 | Batería final |
|---|---|---|
| Normal | **victoria 6 AM** | 31 % |
| Medio | **victoria 6 AM** | 13 % |
| Difícil | muerte a las 5 AM por agotamiento | 0 % |

La curva es la buscada: Normal y Medio se superan jugando bien, y Difícil N6 se pierde por quedarse
sin batería en la última hora, no por un fallo de reacción.

### Batería de regresión, **0 errores JS y 0 errores de consola**:

- Monitor arriba con enemigo en la puerta: **0/4** muertes
- La luz nunca ahuyenta: **0** huidas en 120 encendidos
- Cerrar la puerta ahuyenta a los **4/4** animatrónicos
- Abrir antes de tiempo: el animatrónico sigue en la puerta
- Sin texto visible en la oficina (7 controles comprobados)
- Mapa: 12 nodos sin solapes ni desbordes
- Animatrónico del pasillo encajado con margen en 4 resoluciones
- **0** nodos de ojos rojos en el DOM
- Cristal visible con la puerta cerrada, oculto con la puerta abierta
- Puerta: se atasca a las 5 pulsaciones rápidas, el uso normal no
- Ventanilla contenida dentro de su puerta en 4 resoluciones
- Las dos puertas con chapa, rejilla y proporciones distintas
- Puerta cerrada bloquea **400/400** · la luz nunca ahuyenta **80/80**
- **48/48** comprobaciones de que el panel del mapa no tapa a ningún animatrónico
- Apagón: corta puertas, luces y monitor, y aparece Skibidi dorado con su melodía
- Pantalla de victoria, opciones con pantalla de versión y créditos sin botón *Volver*
- Estrellas correctas al ganar en las 3 dificultades (1★/2★/3★, N6 siempre 3★)
- **10** partidas encadenadas sin fugas de timers; nodos DOM estables (532 → 532)
- Sin desbordes de layout en 1920×1080, 1366×768, 1280×800 y 1024×768
- Anti-camping: baja el monitor a los 3,5 s / 2,7 s / 2,1 s según dificultad
- Monitor abajo con puerta abierta: mata correctamente
- Puerta cerrada: **0/300** filtraciones
- IShowSpeed con puerta cerrada: **0/300** muertes
- **72/72** cámaras (12 × 6 noches) renderizan escena
- **48/48** cámaras sin desbordes ni solapes (12 × 4 resoluciones)
- Animaciones de subida y bajada del monitor: correctas
- Estrellas correctas en las tres dificultades
- Pantalla de muerte con los 4 asesinos: retrato correcto, sin texto residual
- 6 partidas encadenadas: **0** timers colgando

### Multimedia en `assets/` (ya no va incrustada)

El juego **ya no lleva la multimedia en base64 dentro del HTML**. Fuentes, imágenes, música y
llamadas de teléfono viven en la carpeta `assets/` y se sirven junto a la página:

- `assets/fonts/` — `Creepster` y `VT323` (dos subconjuntos) en `.woff2`
- `assets/img/` — logo del splash y periódico de la intro
- `assets/audio/` — música del menú, clic de interfaz y las llamadas de cada noche
  (`phone/` para la v3.0, `phone-unreleased/` para la compilación Unreleased)
- Peticiones a servidores externos durante una sesión completa: **ninguna**. Todo sale del propio
  repositorio; sin `@import`, sin `fonts.googleapis.com` ni `fonts.gstatic.com`.
- **Consecuencia:** el HTML ya **no** es un archivo autónomo. Para jugar hay que servirlo por HTTP
  con la carpeta `assets/` a su lado —GitHub Pages lo hace solo—; abierto con `file://` no carga
  la multimedia.

### Correcciones de esta pasada

- **IShowSpeed mataba saltándose las dos reglas principales.** Al terminar su sprint llamaba a
  `doJumpscare` directamente, sin grace period y **sin comprobar si el monitor estaba levantado**.
  Ahora deja al animatrónico en la puerta y decide el sistema normal, que sí respeta ambas.
- **Clics digitales en todo el audio.** Los osciladores arrancaban y paraban en seco. Se añadió
  envolvente *attack/release* a todos los efectos y arranque/parada suave al zumbido del ventilador.
- **Saturación al solaparse sonidos.** Todo el audio pasa ahora por un bus maestro con compresor,
  así el jumpscare y los efectos simultáneos no distorsionan.
- **Mesas flotando** en el comedor: eran un óvalo sin pata ni sombra. Ahora tienen pata central y
  sombra de contacto.
- **El juego dependía de internet sin que se notara.** La hoja de estilos empezaba con un `@import`
  de Google Fonts: sin conexión, el título y la interfaz perdían su tipografía y caían a una fuente
  del sistema. Las dos fuentes se sirven ahora desde `assets/fonts/`, sin `@import` ni
  dominios de terceros (ver *Multimedia en `assets/`*).
- **Código muerto retirado:** `updateHallEyes` (vacía desde que se quitaron los ojos rojos),
  `stepNear` (nunca conectada) y el `console.log` de arranque de partida.

### Nota de método

Los playtests con el reloj acelerado dan resultados falsos si no se escalan **todos** los relojes por
igual: comprimir la duración de la hora sin comprimir el tick de IShowSpeed lo multiplica
artificialmente, y comprimir además el margen de reacción en la puerta hace que ni un bot perfecto
llegue a tiempo. Las cifras de este documento están medidas de forma determinista sobre el motor real,
sin acelerar.
