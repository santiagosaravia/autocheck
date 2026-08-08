# AutoCheck — Plataforma de Inspección Vehicular (prototipo)

Prototipo funcional de la plataforma de inspección vehicular guiada. Es un
único archivo (`index.html`) que corre en cualquier navegador, sin backend ni
instalación. Sirve para mostrarle el flujo real a inversores, concesionarias
o para que vos mismo lo pruebes en el celular como si fueras el inspector.

## Qué incluye este prototipo

- Formulario de datos del vehículo (patente, marca, modelo, cliente, inspector).
- Checklist guiado de 38 pasos, agrupados en 5 áreas — Exterior (24, incluye
  las 8 mediciones de espesor de pintura con micrómetro/pintómetro), Chasis
  (7, número de VIN + 6 fotos estructurales: largueros, torres de suspensión,
  piso y travesaño trasero), Motor (3, incluye escaneo OBD opcional),
  Interior (3) y Documentación (1).
- Diagrama circular que indica el ángulo de cámara a usar en cada paso
  exterior, como usan las aseguradoras brasileñas — y, además, una
  **ilustración de referencia** (un diagrama simple, no una foto real) en
  **todos** los 38 pasos, mostrando qué encuadre se espera: el ángulo del
  auto, un neumático de cerca, el micrómetro apoyado sobre el panel, la
  chapa del chasis, el tablero, el cinturón, la cédula, etc. Los pasos del
  lado derecho del auto reutilizan la misma ilustración del lado izquierdo
  pero reflejada, para no duplicar arte.
- Se puede avanzar y volver libremente entre pasos aunque falte la foto —
  pero no se puede **generar el informe final** hasta que todas las fotos
  obligatorias estén cargadas (el escaneo OBD es el único ítem opcional).
  La pantalla de resumen muestra qué falta y permite saltar directo a
  completarlo.
- Marcado de observaciones por ítem, con nota.
- Pantalla de resumen con veredicto (Aprobado / Aprobado con observaciones /
  Rechazado), sugerido automáticamente según la cantidad de observaciones.
- Botón para borrar una inspección (desde el historial o desde el informe
  final), protegido con un código de seguridad de 4 dígitos.
- Informe final imprimible / exportable a PDF (botón "Imprimir" usa el
  diálogo nativo del navegador → "Guardar como PDF"). La versión impresa
  usa una grilla compacta agrupada por Exterior/Interior/Chasis/Motor/
  Documentación para aprovechar bien las hojas sin achicar demasiado las
  fotos — en las pruebas, una inspección completa de 38 fotos ocupa
  alrededor de 4 carillas A4, y hasta 5 si hay muchas observaciones
  marcadas (las notas de observación ocupan más espacio, así que es
  esperable que sumen alguna carilla extra). Ninguna foto se corta entre
  una página y la siguiente.
- Historial de inspecciones guardado en el propio dispositivo con
  **IndexedDB** (no localStorage), para poder guardar muchas más fotos sin
  chocar con límites de espacio. **Importante:** esto sigue siendo solo
  para la demo. No hay servidor ni base de datos central — cada
  dispositivo/navegador tiene su propio historial, y se borra si se limpia
  el almacenamiento del navegador (en Configuración del navegador, no con
  un simple refresh de la página — eso sí persiste).

## Qué falta para ser un producto real

Este archivo es el punto de partida visual y de flujo, no la versión
productiva. Para pasar a producción vas a necesitar (podés retomarlo
cuando quieras, o pedirme ayuda con cada parte):

- Backend real con base de datos (para que el historial no viva solo en
  el celular del inspector, y vos como dueño puedas ver todas las
  inspecciones desde un panel).
- Autenticación de inspectores (login).
- Envío del informe por email/WhatsApp al cliente.
- Generación de PDF del lado del servidor (más prolijo que el "Imprimir"
  del navegador).
- Panel de administración para vos: ver todas las inspecciones, filtrar
  por ciudad/cliente/veredicto, exportar reportes agregados.

## Cómo probarlo ahora mismo, sin subir nada a ningún lado

1. Guardá el archivo `index.html` en cualquier carpeta de tu computadora.
2. Hacé doble clic para abrirlo — se abre en tu navegador y ya funciona.
3. También podés mandarte el archivo a tu celular (por WhatsApp o mail) y
   abrirlo ahí para probar el flujo de cámara real.

## Cómo publicarlo en internet con GitHub Pages (gratis, en unos minutos)

Esto te da un link público (ej: `https://tuusuario.github.io/autocheck/`)
que podés mandarle a cualquiera para que lo pruebe desde su propio
celular, sin instalar nada.

### Opción A — Sin usar la terminal (más simple)

1. Entrá a [github.com](https://github.com) y creá una cuenta si no tenés.
2. Hacé clic en **New repository** (botón verde arriba a la derecha).
3. Ponele de nombre `autocheck` (o el que prefieras), dejalo en **Public**,
   y hacé clic en **Create repository**.
4. Dentro del repositorio recién creado, hacé clic en **uploading an
   existing file** (o el botón **Add file → Upload files**).
5. Arrastrá el archivo `index.html` a la ventana y hacé clic en
   **Commit changes**.
6. Andá a la pestaña **Settings** del repositorio → en el menú de la
   izquierda, **Pages**.
7. En **Branch**, elegí `main` y la carpeta `/ (root)`, y guardá.
8. Esperá uno o dos minutos. GitHub te va a mostrar un link tipo
   `https://tuusuario.github.io/autocheck/index.html` — ese es tu sitio
   de prueba, ya publicado.

### Opción B — Con terminal (git)

```bash
# Dentro de la carpeta donde está index.html
git init
git add index.html README.md
git commit -m "Prototipo inicial AutoCheck"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/autocheck.git
git push -u origin main
```

Después andá a **Settings → Pages** en el repositorio en GitHub y activá
Pages sobre la rama `main`, igual que en el paso 6-8 de la Opción A.

## Notas técnicas

- No usa frameworks ni build tools: HTML, CSS y JavaScript puro en un
  solo archivo. Cualquier desarrollador puede tomarlo y extenderlo sin
  curva de aprendizaje.
- Las fotos se comprimen automáticamente en el navegador antes de
  guardarse (para no llenar el almacenamiento local).
- Tipografías: Oswald (títulos), Inter (texto), IBM Plex Mono (datos
  técnicos como VIN, kilometraje, coordenadas) — cargadas desde Google
  Fonts.
- Los 23 pasos del checklist están definidos en un array al principio del
  `<script>` (`const STEPS = [...]`). Para agregar, quitar o reordenar
  pasos, se edita ahí — no hace falta tocar el resto del código.
