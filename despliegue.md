# Despliegue de PokeDex en Azure Static Web Apps

Este documento describe el procedimiento de despliegue consignado para la aplicación PokeDex.

- **URL pública:** https://wonderful-dune-0d08c9e1e.1.azurestaticapps.net
- **Repositorio:** https://github.com/CAROLYYY0220/pokedex
- **Suscripción:** Azure for Students
- **Servicio:** Azure Static Web Apps
- **Plan:** Free

## 1. Crear el repositorio en GitHub

1. Abrir https://github.com/new.
2. Crear un repositorio llamado `pokedex`.
3. Seleccionar la visibilidad deseada. El repositorio documentado es público.
4. Si ya se creó el repositorio y contiene el proyecto, no es necesario repetir este paso.

## 2. Subir el código fuente

La documentación original indica que el código se preparó como repositorio propio y se subió a la rama `main`.

Ejemplo de comandos de Git para un repositorio nuevo (ajusta la ruta local y verifica el origen antes de ejecutarlos):

```powershell
git init
git add .
git commit -m "Código inicial de PokeDex"
git branch -M main
git remote add origin https://github.com/CAROLYYY0220/pokedex.git
git push -u origin main
```

Si Git no tiene configurado el autor de los commits, establece tu nombre y correo:

```powershell
git config --global user.name "TU_NOMBRE"
git config --global user.email "TU_CORREO"
```

No elimines la carpeta `.git` ni el historial de un repositorio existente sin confirmar que realmente deseas reinicializarlo.

## 3. Crear la aplicación estática en Azure

1. Entrar en https://portal.azure.com.
2. Buscar **Static Web Apps** y seleccionar **Crear**.
3. Configurar los datos básicos:
   - Suscripción: `Azure for Students`.
   - Grupo de recursos: `pokedex` (según la configuración documentada).
   - Nombre: `pokedex`.
   - Plan: `Free`.
   - Región: seleccionar una permitida por la suscripción.
4. En la sección de implementación, elegir GitHub y autorizar el acceso.
5. Seleccionar la organización `CAROLYYY0220`, el repositorio `pokedex` y la rama `main`.
6. Configurar la compilación con los valores indicados en la siguiente sección.
7. Revisar y crear el recurso.

### Error de región

Si aparece `RequestDisallowedByAzure`, la región seleccionada puede no estar permitida por la política de la suscripción. Selecciona otra región permitida que aparezca disponible en el portal y vuelve a validar.

## 4. Configuración de compilación

| Campo | Valor documentado |
|---|---|
| Preset | Angular |
| Ubicación de la aplicación | `/` |
| Ubicación de la API | Vacía |
| Ubicación de salida | `dist/pokedex-angular` |

El flujo de GitHub Actions utiliza los siguientes valores:

```yaml
app_location: "/"
api_location: ""
output_location: "dist/pokedex-angular"
```

## 5. GitHub Actions

Al conectar el repositorio con Azure Static Web Apps, Azure configura un flujo de GitHub Actions y almacena el secreto de despliegue en el repositorio.

Para verificar el proceso:

1. Abrir el repositorio en GitHub.
2. Entrar en la pestaña **Actions**.
3. Revisar la ejecución de **Azure Static Web Apps CI/CD**.
4. Confirmar que el flujo finalice correctamente.

La documentación original indica que se eliminó un flujo antiguo de Azure App Service (`main_pokedex-carol.yml`) porque fallaba al requerir secretos que no estaban configurados. Antes de borrar flujos en otro despliegue, verifica que ya no se utilicen.

## 6. Verificar el sitio

Abrir la aplicación publicada:

https://wonderful-dune-0d08c9e1e.1.azurestaticapps.net

También se documentó la comprobación de encabezados HTTP con PowerShell:

```powershell
curl.exe -I https://wonderful-dune-0d08c9e1e.1.azurestaticapps.net
```

La prueba funcional descrita consistió en recargar la página con `Ctrl+F5`, revisar la consola del navegador y confirmar que la lista y las imágenes de Pokémon cargaran correctamente.

## 7. Referencias

- [Repositorio en GitHub](https://github.com/CAROLYYY0220/pokedex)
- [Portal de Azure](https://portal.azure.com)
- [Azure for Students](https://azure.microsoft.com/free/students)
- [SecurityHeaders](https://securityheaders.com)
