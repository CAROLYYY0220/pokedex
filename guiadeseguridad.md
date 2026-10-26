# Configuración de seguridad

Este documento reúne la configuración de seguridad descrita para PokeDex en Azure Static Web Apps.

## 1. Archivo de configuración

El archivo `staticwebapp.config.json` debe ubicarse en la raíz del proyecto, junto a `package.json`, según la guía original.

Configuración documentada:

```json
{
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": [
      "/assets/*",
      "*.{css,js,gif,png,jpg,ico,woff,woff2,ttf,eot,otf,json}"
    ]
  },
  "globalHeaders": {
    "Content-Security-Policy": "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:; connect-src 'self' https://beta.pokeapi.co https://graphql.pokeapi.co https://pokeapi.co; object-src 'none'; base-uri 'self'; form-action 'self'; frame-ancestors 'none'",
    "X-Frame-Options": "DENY",
    "Permissions-Policy": "geolocation=(), camera=(), microphone=(), payment=()",
    "Referrer-Policy": "strict-origin-when-cross-origin",
    "X-Content-Type-Options": "nosniff"
  }
}
```

## 2. Función de los encabezados

| Encabezado | Función descrita |
|---|---|
| `Content-Security-Policy` | Restringe los orígenes de los que se pueden cargar recursos y los destinos de conexión. |
| `X-Frame-Options: DENY` | Impide que la aplicación se muestre dentro de un `iframe` en otra página. |
| `Permissions-Policy` | Desactiva el acceso a ubicación, cámara, micrófono y pagos. |
| `Referrer-Policy` | Controla la información de referencia enviada al navegar a otros sitios. |
| `X-Content-Type-Options: nosniff` | Evita que el navegador intente adivinar el tipo MIME de un recurso. |
| `Strict-Transport-Security` | La guía original indica que Azure lo agrega por defecto para exigir HTTPS. Debe confirmarse en la respuesta real del servidor. |

## 3. Comprobar los encabezados

Ejecuta en PowerShell:

```powershell
curl.exe -I https://wonderful-dune-0d08c9e1e.1.azurestaticapps.net
```

Revisa que la respuesta contenga los encabezados esperados.

## 4. Escaneo de SecurityHeaders

1. Abrir https://securityheaders.com.
2. Introducir la URL pública de la aplicación.
3. Ejecutar el análisis.
4. Guardar una captura de pantalla con la fecha y el resultado para usarla como evidencia.

La documentación original registra una calificación C antes de agregar `staticwebapp.config.json` y A+ después. Ese resultado corresponde al registro del proyecto y no constituye una medición actualizada.

## 5. Prueba funcional

La guía original indica que se recargó la aplicación con `Ctrl+F5`, se revisó la consola del navegador (F12) y se comprobó que la lista e imágenes de Pokémon cargaran sin errores de Content Security Policy.

Para una entrega, agrega capturas propias que evidencien estas comprobaciones.
