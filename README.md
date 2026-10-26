# PokeDex en Azure Static Web Apps

Aplicación **PokeDex** (Angular 14) desplegada en la nube pública de **Microsoft Azure** usando el servicio **Azure Static Web Apps**, para la compañía Pueblo Paleta Inc.

- **URL pública:** https://wonderful-dune-0d08c9e1e.1.azurestaticapps.net
- **Repositorio:** https://github.com/CAROLYYY0220/pokedex
- **Nube usada:** Azure for Students
- **Calificación en securityheaders.com:** **A+**

El paso a paso del despliegue está en [Despliegue.md](Despliegue.md).

---

## Tutorial: cómo se creó la cuenta en la nube (Azure for Students)

Azure for Students es la opción de Microsoft para estudiantes. Requiere una **cuenta de correo institucional** y no pide tarjeta de crédito.

### Paso 1. Entrar a la página de Azure for Students

1. Abrir en el navegador: https://azure.microsoft.com/free/students
2. Pulsar **Activate now** (Activar ahora).

### Paso 2. Iniciar sesión con la cuenta institucional

1. Escribir el correo institucional de la universidad y pulsar **Siguiente**.
2. Ingresar la contraseña de esa cuenta.
3. Aceptar los permisos que pida Microsoft.

### Paso 3. Verificar que se es estudiante

1. Completar el formulario con los datos personales (país, nombre y apellido).
2. Aceptar los términos y condiciones.
3. Verificar el teléfono con el código que llega por mensaje de texto, si lo pide.
4. Si la universidad lo requiere, confirmar el correo institucional con el enlace que llega a la bandeja.

### Paso 4. Entrar al portal de Azure

1. Abrir https://portal.azure.com e iniciar sesión con la misma cuenta.
2. Verificar que en **Suscripciones** aparezca **Azure for Students**.

### Paso 5. Configuración inicial

1. **Crear un grupo de recursos:** buscar *Grupos de recursos* > **Crear**, con el nombre `pokedex`.
2. **Región:** Azure for Students solo permite crear recursos en algunas regiones (directiva *Allowed resource deployment regions*). Con la región equivocada aparece el error `RequestDisallowedByAzure`. Se resolvió probando otra región de las que ofrece Static Web Apps (Central US, East US 2, West US 2, West Europe y East Asia) hasta que la validación pasó sin error.
3. **Costos:** la app usa el plan **Free** de Static Web Apps, por lo que no consume el crédito de la suscripción.

### Paso 6. Crear el recurso Static Web App

El detalle de la creación del recurso, la conexión con GitHub y la configuración de la compilación está en [Despliegue.md](Despliegue.md).

---

## Problemas encontrados

| Problema | Causa | Solución |
|---|---|---|
| `RequestDisallowedByAzure` al crear el recurso | La región elegida no está permitida en la suscripción de estudiante | Cambiar el campo **Región** por otra de las permitidas |
| El flujo antiguo de GitHub Actions fallaba con `client-id and tenant-id` | Era un flujo de App Service y el repositorio nuevo no tiene esos secretos | Eliminar el archivo `main_pokedex-carol.yml` |

---

## Tecnologías

- Angular 14
- Apollo Client / GraphQL (consume PokéAPI)
- GitHub Actions
- Azure Static Web Apps
