# Fortines

Juego de cartas de batalla coleccionable ambientado en la Argentina de las Invasiones Inglesas, la Independencia y la guerra con el Brasil. Es una app de un solo archivo HTML/JS (`www/index.html`) envuelta en Capacitor 8 para Android.

## Cómo sale el APK y el AAB

Cada vez que subís cambios a `main`, GitHub Actions compila solo (pestaña **Actions** → "Compilar Android"). Al terminar, en **Releases** aparece una versión de prueba con dos archivos:

- `fortines-prueba-vX.apk`: para instalar directo en el teléfono (APK de depuración).
- `fortines-vX.aab`: para subir a Google Play Console (firmado con tu clave de subida).

También quedan como artefactos en cada ejecución de Actions. Podés lanzar una compilación a mano con **Run workflow**.

El número de versión (`versionCode`) sube solo con cada compilación, así Play nunca rechaza un AAB por versión repetida.

## Secretos necesarios (una sola vez)

En el repo: **Settings → Secrets and variables → Actions → New repository secret**.

| Secreto | Qué va |
| --- | --- |
| `ANDROID_KEYSTORE_BASE64` | El archivo `.jks` convertido a base64 |
| `ANDROID_KEYSTORE_PASSWORD` | Contraseña del keystore |
| `ANDROID_KEY_ALIAS` | Alias de la clave (`fortines`) |
| `ANDROID_KEY_PASSWORD` | Contraseña de la clave |

Sin estos secretos el APK de prueba sale igual, pero el AAB queda sin firmar.

**Guardá el `.jks` y las contraseñas fuera del repo.** Nunca se suben a Git (están en `.gitignore`).

## Actualizar el juego

1. Reemplazá `www/index.html` por la versión nueva.
2. Hacé commit y push a `main`.
3. Esperá unos minutos y bajá el APK nuevo desde Releases.

Las fuentes van incluidas en `www/fonts`, así que el juego funciona sin internet.

## Ícono y pantalla de inicio

Los originales están en `assets/`. Si los cambiás, regenerá los de Android con:

```
npm run icons
```

## Datos de la app

- ID de la app: `com.fortines.juego` (se puede cambiar hasta la primera subida a Play; después queda fijo para siempre).
- Android mínimo: 7.0 (API 24). Apunta a Android 16 (API 36).
- Orientación: vertical.
