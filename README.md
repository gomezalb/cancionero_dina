# Cancionero

Cancionero digital con panel de administración integrado. Basado en [cancionero original](https://github.com/gomezalb/cancionero).

## Configuración inicial (una sola vez)

### 1. Crear el repositorio en GitHub

1. Creá un nuevo repositorio público en GitHub llamado `cancionero_dina`
2. Subí todos estos archivos al repositorio
3. En **Settings → Pages**, activá GitHub Pages desde la rama `main`

### 2. Crear el token de GitHub

1. Entrá a [github.com/settings/tokens](https://github.com/settings/tokens)
2. Hacé clic en **"Fine-grained tokens" → "Generate new token"**
3. Configurá:
   - **Token name:** `cancionero-dina-admin`
   - **Expiration:** 1 year (podés renovarlo cada año)
   - **Repository access:** Solo `cancionero_dina`
   - **Permissions → Contents:** `Read and write`
4. Hacé clic en **Generate token** y copiá el token (empieza con `github_pat_...`)

### 3. Configurar el token y contraseña en el código

Abrí `index.html` y buscá esta sección cerca del final del archivo:

```javascript
const GH_CONFIG = {
  owner:  "GITHUB_USUARIO",     // ← reemplazar con tu usuario de GitHub
  repo:   "cancionero_dina",
  file:   "canciones.json",
  branch: "main",
  token:  "GITHUB_TOKEN",       // ← reemplazar con el token que generaste
  password: "ADMIN_PASSWORD"    // ← elegí una contraseña para el admin
};
```

Reemplazá los tres valores y volvé a subir el archivo.

## Uso del panel de administración

1. Entrá al cancionero en la URL de GitHub Pages
2. Tocá la pestaña **Editar**
3. Desde ahí podés:
   - **Buscar y editar** acordes/tonalidad de cualquier canción
   - **Agregar canciones nuevas** con la letra
4. Cuando terminés los cambios, tocá **"☁ Publicar cambios"**
5. Ingresá la contraseña de administración
6. En aproximadamente **1 minuto** los cambios son visibles para todos

## Estructura del proyecto

- `index.html` — toda la aplicación
- `canciones.json` — base de datos de canciones
- `setlist.json` — lista fijada para reuniones (opcional)
- `sw.js` — service worker para uso offline
- `manifest.json` — configuración PWA

## Lista fijada (setlist.json)

Para fijar una lista para una reunión, editá `setlist.json`:

```json
{
  "name": "Reunión del domingo",
  "expira": "2026-12-31",
  "songs": [
    "Título canción 1",
    "Título canción 2"
  ]
}
```

Cuando pasa la fecha de `expira`, la lista fijada deja de mostrarse automáticamente.
Para no tener lista fijada, dejá el archivo como `{}`.
