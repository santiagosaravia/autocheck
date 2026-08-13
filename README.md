Exit code: 0
Wall time: 0.8 seconds
Output:
# AutoCheck

Prototipo mÃ³vil autocontenido para inspecciones vehiculares. Usa perfiles de inspecciÃ³n configurables, IndexedDB para inspecciones y evidencias, autosave, captura de cÃ¡mara, GPS opcional, hallazgos, veredicto e informe imprimible.

## Publicar en GitHub Pages

1. CreÃ¡ un repositorio nuevo en GitHub.
2. ElegÃ­ **Add file â†’ Upload files** y subÃ­ `index.html` y `README.md`.
3. En **Settings â†’ Pages**, seleccionÃ¡ **Deploy from a branch**, rama `main` y carpeta `/ (root)`.
4. GuardÃ¡. GitHub mostrarÃ¡ la URL pÃºblica luego de la publicaciÃ³n.

AbrÃ­ siempre la URL HTTPS de GitHub Pages: la cÃ¡mara, GPS e IndexedDB dependen de un contexto seguro. TambiÃ©n puede abrirse localmente, pero algunos navegadores restringen cÃ¡mara/GPS en `file://`.

## iPhone + Safari

1. GuardÃ¡ ambos archivos en **Archivos**.
2. AbrÃ­ GitHub en Safari, iniciÃ¡ sesiÃ³n y creÃ¡ el repositorio.
3. UsÃ¡ **Upload files** para seleccionar los dos archivos desde Archivos. Si no aparece la opciÃ³n, activÃ¡ **Solicitar sitio web de escritorio** desde `aA`.
4. ActivÃ¡ Pages como se indica arriba y abrÃ­ la URL HTTPS.
5. En Compartir elegÃ­ **AÃ±adir a pantalla de inicio** para usarlo como app.

Al iniciar una inspecciÃ³n Safari solicitarÃ¡ GPS; rechazarlo no bloquea el flujo. Al tocar **CAPTURAR FOTO** se abre la cÃ¡mara con preferencia por la trasera (`capture="environment"`). iOS decide finalmente quÃ© cÃ¡mara ofrece, por limitaciones del navegador. No hay selector de galerÃ­a, archivos, arrastre ni upload: la evidencia se ingresa sÃ³lo mediante ese control de captura.

Los datos y fotos optimizadas se almacenan en IndexedDB del navegador. Si se borra el historial/datos del sitio, se eliminan; exportÃ¡ o imprimÃ­ los informes importantes. IndexedDB permite continuar offline despuÃ©s de que el archivo estÃ© cargado, aunque la fuente remota puede no estar disponible sin red; el diseÃ±o usa fuentes de respaldo del sistema. Para mÃ¡xima disponibilidad offline, descargÃ¡/autoalojÃ¡ las fuentes o eliminÃ¡ la regla `@import`.

## Pruebas realizadas

- EXPECTED: perfiles Simple, Precompra, Completa, Vistoria, Siniestro, Flota y Personalizada generan checklists diferentes desde datos JavaScript.
- EXPECTED: requisitos obligatorios bloquean finalizar y el resumen muestra cada pendiente.
- EXPECTED: fotos se comprimen a JPEG (mÃ¡ximo aproximado 1200 px) y se guardan con timestamp, punto e informaciÃ³n GPS disponible.
- EXPECTED: hallazgos graves/crÃ­ticos producen `RECHAZADO`; otros hallazgos producen `APROBADO CON OBSERVACIONES`.
- NOT TESTED: cÃ¡mara, GPS, IndexedDB, impresiÃ³n A4 y recuperaciÃ³n deben validarse en el navegador/dispositivo de destino, ya que este entorno no dispone de dichos permisos/interfaz.

El cÃ³digo de borrado `1310` es una barrera bÃ¡sica del prototipo, no autenticaciÃ³n real. Las firmas y QR quedan preparados conceptualmente en el informe y no constituyen certificaciÃ³n digital.


