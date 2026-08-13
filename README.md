Exit code: 0
Wall time: 0.8 seconds
Output:
# AutoCheck

Prototipo móvil autocontenido para inspecciones vehiculares. Usa perfiles de inspección configurables, IndexedDB para inspecciones y evidencias, autosave, captura de cámara, GPS opcional, hallazgos, veredicto e informe imprimible.

## Publicar en GitHub Pages

1. Creá un repositorio nuevo en GitHub.
2. Elegí **Add file → Upload files** y subí `index.html` y `README.md`.
3. En **Settings → Pages**, seleccioná **Deploy from a branch**, rama `main` y carpeta `/ (root)`.
4. Guardá. GitHub mostrará la URL pública luego de la publicación.

Abrí siempre la URL HTTPS de GitHub Pages: la cámara, GPS e IndexedDB dependen de un contexto seguro. También puede abrirse localmente, pero algunos navegadores restringen cámara/GPS en `file://`.

## iPhone + Safari

1. Guardá ambos archivos en **Archivos**.
2. Abrí GitHub en Safari, iniciá sesión y creá el repositorio.
3. Usá **Upload files** para seleccionar los dos archivos desde Archivos. Si no aparece la opción, activá **Solicitar sitio web de escritorio** desde `aA`.
4. Activá Pages como se indica arriba y abrí la URL HTTPS.
5. En Compartir elegí **Añadir a pantalla de inicio** para usarlo como app.

Al iniciar una inspección Safari solicitará GPS; rechazarlo no bloquea el flujo. Al tocar **CAPTURAR FOTO** se abre la cámara con preferencia por la trasera (`capture="environment"`). iOS decide finalmente qué cámara ofrece, por limitaciones del navegador. No hay selector de galería, archivos, arrastre ni upload: la evidencia se ingresa sólo mediante ese control de captura.

Los datos y fotos optimizadas se almacenan en IndexedDB del navegador. Si se borra el historial/datos del sitio, se eliminan; exportá o imprimí los informes importantes. IndexedDB permite continuar offline después de que el archivo esté cargado, aunque la fuente remota puede no estar disponible sin red; el diseño usa fuentes de respaldo del sistema. Para máxima disponibilidad offline, descargá/autoalojá las fuentes o eliminá la regla `@import`.

## Pruebas realizadas

- EXPECTED: perfiles Simple, Precompra, Completa, Vistoria, Siniestro, Flota y Personalizada generan checklists diferentes desde datos JavaScript.
- EXPECTED: requisitos obligatorios bloquean finalizar y el resumen muestra cada pendiente.
- EXPECTED: fotos se comprimen a JPEG (máximo aproximado 1200 px) y se guardan con timestamp, punto e información GPS disponible.
- EXPECTED: hallazgos graves/críticos producen `RECHAZADO`; otros hallazgos producen `APROBADO CON OBSERVACIONES`.
- NOT TESTED: cámara, GPS, IndexedDB, impresión A4 y recuperación deben validarse en el navegador/dispositivo de destino, ya que este entorno no dispone de dichos permisos/interfaz.

El código de borrado `1310` es una barrera básica del prototipo, no autenticación real. Las firmas y QR quedan preparados conceptualmente en el informe y no constituyen certificación digital.


