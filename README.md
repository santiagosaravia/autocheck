# AutoCheck — Plataforma de Inspección Vehicular (prototipo)

Prototipo funcional de la plataforma de inspección vehicular guiada. Es un
único archivo (`index.html`) que corre en cualquier navegador, sin backend ni
instalación. Sirve para mostrarle el flujo real a inversores, concesionarias
o para que vos mismo lo pruebes en el celular como si fueras el inspector.

## Qué incluye este prototipo

- Formulario de datos del vehículo (patente, marca, modelo, cliente, inspector).
- Checklist guiado de 23 pasos (idéntico al listado que armamos: exterior,
  identificación/VIN, neumáticos, mecánica, interior, documentación).
- Diagrama circular que indica el ángulo de foto a tomar en cada paso,
  como usan las aseguradoras brasileñas.
- No se puede avanzar al siguiente paso sin completar la foto (y el dato
  de texto/número si corresponde).
- Marcado de observaciones por ítem, con nota.
- Pantalla de resumen con veredicto (Aprobado / Aprobado con observaciones /
  Rechazado), sugerido automáticamente según la cantidad de observaciones.
- Informe final imprimible / exportable a PDF (botón "Imprimir" usa el
  diálogo nativo del navegador → "Guardar como PDF").
- Historial de inspecciones guardado en el propio dispositivo (localStorage).
  **Importante:** esto es solo para la demo. No hay servidor ni base de
  datos central — cada dispositivo/navegador tiene su propio historial, y
  se borra si se limpia la caché del navegador.

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
