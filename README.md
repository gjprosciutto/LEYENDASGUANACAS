# Noche en el Cantón 🐾

Plataformero 2D en HTML + CSS + JavaScript puro (sin frameworks ni build tools),
basado en leyendas de El Salvador. Corre 100% en el navegador.

## Cómo abrirlo en VS Code

1. Descomprimí la carpeta y abrila en VS Code (`Archivo > Abrir carpeta...`).
2. Instalá la extensión **Live Server** (de Ritwick Dey) si no la tenés.
3. Click derecho sobre `index.html` → **"Open with Live Server"**.
   - Esto es importante: si abrís el `index.html` directo con doble clic (`file://`),
     algunos navegadores bloquean la carga de los archivos `.js` por seguridad (CORS).
     Con Live Server (o cualquier servidor local) no hay problema.

Alternativa sin extensión, desde la terminal integrada de VS Code:

```bash
# Opción con Python (si lo tenés instalado)
python3 -m http.server 5500
# luego abrí http://localhost:5500 en el navegador
```

## Estructura del proyecto

```
noche-en-el-canton-2d/
├── index.html          # Estructura de la página, HUD y pantallas
├── style.css            # Estilo Dark Gothic / Místico
└── js/
    ├── dialogo.js        # Todas las líneas del Cadejo Blanco (lore de cada leyenda)
    ├── niveles.js         # Geometría de cada nivel (piso, plataformas, posiciones)
    └── juego.js           # Motor: física, cámara, IA de enemigos, estados del juego
```

## Controles

- Mover: `←` `→` o `A` `D`
- Saltar: `↑`, `W` o `Espacio`

## Flujo del juego

1. **Tienda** — caminás hasta la tienda de Niña Mayra a completar el mandado.
2. **El bosque (La Siguanaba)** — plataformas, tenés que escapar de ella sin dejar que te alcance.
   Al cruzar el portal aparece una pantalla de carga: "¡Has logrado escapar de la Siguanaba!".
3. **El río (El Cipitío)** — esquivá las piedras que te tira mientras cruzás los tramos de piso.
   Otra pantalla de carga al pasar el portal.
4. **El camino final (El Cadejo Negro)** — huida a contrarreloj; al llegar a cierto punto,
   el Cadejo Blanco se sacrifica peleando contra él para que sigas corriendo. Pantalla de
   carga final antes de llegar a la casa.
5. **La casa** — llegás donde tu mamá. La casa de tu mamá aparece flotando en el aire
   (se mece suavemente y proyecta sombra en el suelo) y termina el juego.

Tenés 3 vidas compartidas entre los niveles con peligro (bosque, río, camino final).
Si las perdés todas, pantalla de Game Over con botón para reintentar desde el inicio.

## Estilo visual

- **Pixel art estilo N64**: todo el canvas se dibuja normal y, al final de cada frame,
  se reduce de tamaño y se vuelve a agrandar sin suavizado (función `aplicarPixelArt()`
  en `js/juego.js`). Eso "cuadricula" la imagen como en una consola de baja resolución.
  Para más o menos pixelado, cambiá la constante `ESCALA_PIXEL_ART` (más alto = más chunky).
- **La Siguanaba** es una mujer con cabeza de caballo, sin más adornos ni misterio de rostro.
- **Pantallas de portal**: en vez de una transición instantánea, cada portal muestra una
  pantalla de carga estilo videojuego (barra de progreso + mensaje) antes de continuar.
  Los mensajes y la duración se controlan en `MENSAJES_CARGA` y `DURACION_CARGA`.
- **Pantalla de inicio**: botón grande y "chunky" al estilo Geometry Dash (rebote, bisel
  3D con sombra escalonada), sobre un fondo retro 80s con sol, grid en perspectiva y
  formas geométricas flotantes.

## Ideas para seguir editando

- Cambiá las velocidades (`velocidadBase`) o el número de vidas en `js/niveles.js` y `js/juego.js`.
- Agregá más líneas de diálogo en `js/dialogo.js`.
- Los personajes están dibujados con formas de `canvas` (sin imágenes) para que el proyecto
  funcione sin assets externos — podés reemplazar las funciones `dibujar...()` en `js/juego.js`
  por `drawImage()` si querés usar sprites/arte propio.
- Si más adelante querés guardar puntajes o tiempos de partida en un servidor, ahí sí
  tendría sentido meter un backend en **PHP** (o Node) con una base de datos — pero el
  juego en sí, al ser todo lógica de cliente (canvas + teclado), no lo necesita.
