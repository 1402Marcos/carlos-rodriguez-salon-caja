# Carlos Rodríguez Salón — Caja

Sistema de control de flujo de efectivo, cierre de caja, catálogo, empleados,
reportes y respaldo para un salón de belleza. Es una aplicación web de un
solo archivo (`index.html`): no requiere servidor, base de datos externa ni
backend. Todos los datos se guardan en el propio navegador del dispositivo
(IndexedDB).

## Estructura del proyecto

```
index.html              La aplicación completa (HTML + CSS + JS)
manifest.json           Metadatos de la PWA (nombre, íconos, colores)
sw.js                   Service Worker (uso offline + instalación)
icons/
  icon-192.png           Ícono 192×192 (Android)
  icon-512.png           Ícono 512×512 (Android, splash screen)
  icon-maskable-512.png  Ícono adaptable 512×512 (Android, forma dinámica)
  apple-touch-icon.png   Ícono 180×180 (iOS, opcional)
  favicon-32.png         Ícono de pestaña (opcional)
```

Los cuatro archivos (`index.html`, `manifest.json`, `sw.js`, `icons/`) deben
publicarse juntos, respetando esta misma estructura de carpetas.

## Publicar en GitHub Pages (gratis, con HTTPS automático)

### 1. Crear la cuenta y el repositorio
1. Crea una cuenta gratuita en [github.com](https://github.com) si no tienes una.
2. Haz clic en **+** (arriba a la derecha) → **New repository**.
3. Nombre sugerido: `salon-caja` (puede ser cualquiera).
4. Marca la opción **Public** (obligatorio para GitHub Pages gratis).
5. Haz clic en **Create repository**.

### 2. Subir los archivos
**Opción A — Sin usar la terminal (recomendado):**
1. En la página del repositorio recién creado, haz clic en **uploading an existing file**
   (o **Add file → Upload files**).
2. Arrastra los archivos `index.html`, `manifest.json`, `sw.js` y la carpeta
   `icons` completa (con sus 5 imágenes adentro).
3. Escribe un mensaje de commit, ej. "Primera versión".
4. Haz clic en **Commit changes**.

**Opción B — Con git (si ya lo usas):**
```bash
git clone https://github.com/TU-USUARIO/salon-caja.git
cd salon-caja
# copia aquí index.html, manifest.json, sw.js y la carpeta icons/
git add .
git commit -m "Primera versión"
git push
```

### 3. Activar GitHub Pages
1. En el repositorio, ve a **Settings** → **Pages** (menú lateral izquierdo).
2. En **Source**, elige **Deploy from a branch**.
3. En **Branch**, elige `main` y la carpeta `/ (root)`.
4. Haz clic en **Save**.
5. Espera 1–3 minutos. GitHub mostrará tu URL pública, con este formato:
   ```
   https://TU-USUARIO.github.io/salon-caja/
   ```

El certificado **HTTPS se activa automáticamente**, sin ninguna configuración
adicional — GitHub lo emite y renueva por ti de forma gratuita, de por vida,
mientras el repositorio exista.

### 4. Instalar como aplicación en Android (Chrome)
1. Abre la URL de tu sitio en **Google Chrome** en el teléfono Android.
2. Chrome mostrará automáticamente un banner **"Instalar app"** o
   **"Agregar a la pantalla de inicio"** (puede tardar unos segundos en
   aparecer). Si no aparece solo, toca el menú de tres puntos (⋮) →
   **"Instalar aplicación"**.
3. Confirma. El ícono aparecerá en la pantalla de inicio del teléfono y se
   abrirá en modo de pantalla completa, sin la barra del navegador — como
   cualquier otra app instalada.

### 5. Verificar que funciona sin internet
1. Con la app ya instalada y abierta al menos una vez con internet activo,
   pon el teléfono en modo avión.
2. Abre la app desde el ícono de la pantalla de inicio: debe seguir
   funcionando con normalidad (el Service Worker guarda una copia local).

## Actualizar la app en el futuro
Cada vez que quieras publicar una nueva versión:
1. Sube el nuevo `index.html` (y `sw.js`/`manifest.json` si cambiaron) al
   mismo repositorio, reemplazando los archivos existentes (arrastrar de
   nuevo con **Add file → Upload files**, o `git add/commit/push`).
2. GitHub Pages actualiza el sitio automáticamente en 1–2 minutos.
3. La próxima vez que alguien abra la app **con internet**, recibirá la
   versión nueva automáticamente. Si la abre sin internet, seguirá viendo
   la última versión que se guardó en su dispositivo, hasta que vuelva a
   tener conexión.

## Importante: qué SÍ y qué NO resuelve este hosting

- ✅ Resuelve: necesitar `file://` y sus problemas de compatibilidad,
  contar con HTTPS, y poder instalarse como app en Android.
- ❌ No resuelve: sincronización de datos en tiempo real entre varios
  teléfonos. Cada dispositivo que visita la URL sigue teniendo su propia
  base de datos local (IndexedDB), independiente de los demás. Alojar el
  archivo en un sitio web no crea automáticamente una base de datos
  compartida — para eso se necesitaría un backend con servidor, lo cual
  está fuera del alcance de este proyecto (ver conversación previa sobre
  este tema).

## Seguridad de los datos
Los datos del negocio nunca salen del dispositivo ni pasan por GitHub —
GitHub solo aloja el código de la aplicación (el archivo `.html` en sí),
no la información de caja, movimientos ni usuarios. Sigue haciendo
respaldos periódicos desde **Más → Respaldo de datos** dentro de la app.
