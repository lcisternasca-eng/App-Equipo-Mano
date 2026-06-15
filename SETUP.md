# Configuración Google Cloud — Tabla Quirúrgica Unidad de Mano

Sigue estos pasos para activar la autenticación y la conexión con Google Sheets.
Tiempo estimado: 15 minutos.

---

## Paso 1 — Crear un proyecto en Google Cloud

1. Ve a https://console.cloud.google.com
2. Inicia sesión con **l.cisternas.ca@gmail.com**
3. En la barra superior, haz clic en el selector de proyectos → **"Nuevo proyecto"**
4. Nombre del proyecto: `tabla-quirurgica-mano`
5. Haz clic en **Crear**

---

## Paso 2 — Activar la API de Google Sheets

1. En el menú lateral: **APIs y servicios → Biblioteca**
2. Busca `Google Sheets API`
3. Haz clic en el resultado → **Habilitar**

---

## Paso 3 — Configurar la pantalla de consentimiento OAuth

1. En el menú lateral: **APIs y servicios → Pantalla de consentimiento de OAuth**
2. Tipo de usuario: selecciona **Externo** → Crear
3. Rellena los campos obligatorios:
   - Nombre de la app: `Tabla Quirúrgica Mano`
   - Correo de asistencia: `l.cisternas.ca@gmail.com`
   - Correo del desarrollador: `l.cisternas.ca@gmail.com`
4. Haz clic en **Guardar y continuar** (en las pantallas de permisos y prueba también)
5. En la pantalla **"Usuarios de prueba"**, haz clic en **+ Añadir usuarios**
   - Añade los correos de todos los miembros del equipo que usarán la app
6. Haz clic en **Guardar y continuar** hasta terminar

---

## Paso 4 — Crear el Client ID de OAuth

1. En el menú lateral: **APIs y servicios → Credenciales**
2. Haz clic en **+ Crear credenciales → ID de cliente de OAuth**
3. Tipo de aplicación: **Aplicación web**
4. Nombre: `Tabla Quirúrgica App`
5. En **"Orígenes JavaScript autorizados"**, añade:
   - `http://localhost` (para pruebas locales)
   - La URL donde desplegarás la app (ej: `https://tu-app.vercel.app`)
6. Haz clic en **Crear**
7. Se abrirá un diálogo con tu **Client ID** — cópialo (se ve así: `123456789-abcdef.apps.googleusercontent.com`)

---

## Paso 5 — Pegar el Client ID en la app

Abre el archivo `index.html` con cualquier editor de texto.
Busca esta línea cerca del inicio del script:

```javascript
clientId: '',
```

Cámbiala por:

```javascript
clientId: 'TU_CLIENT_ID_AQUI',
```

Guarda el archivo.

---

## Paso 6 — Verificar permisos en las hojas de Google Sheets

Las dos hojas deben ser accesibles por la cuenta que iniciará sesión.

- **Lista de espera:** https://docs.google.com/spreadsheets/d/1V48vqYerSrQ2IC6hikePzMoCAASBZfzR3n_i9OvWjgI
- **Tabla quirúrgica:** https://docs.google.com/spreadsheets/d/1DBjeYGeLSSRG68CljiswtZoo_f5oG6wSTFoVaLbfqYE

Asegúrate de que la cuenta `l.cisternas.ca@gmail.com` tiene acceso de **editor** en ambas.

---

## Paso 7 — Preparar las hojas (estructura de columnas)

La app espera esta estructura. Si tus hojas ya tienen encabezados, asegúrate de que coincidan.

### Hoja DIFERIDOS (lista de espera) — pestaña "DIFERIDOS"
| A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|
| Nombre | RUT | Diagnóstico | Lateralidad | FechaLesión | FechaIngreso | Teléfono | Observaciones |

### Hoja tabla quirúrgica — pestaña "Junio 2026"
| A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Turno | Nombre | RUT | Edad | Diagnóstico | CX | Lateralidad | Cirujanos | Anestesia | Código | Insumos | Biopsia | Comentario | Fecha | Pabellón | Estado |

La fila 1 es de encabezados. Los datos empiezan en la fila 2.

---

## Paso 8 — Desplegar la app (para acceso del equipo)

### Opción A — Vercel (recomendado, gratis)
1. Crea una cuenta en https://vercel.com con tu Gmail
2. Haz clic en **"Add New Project"**
3. Elige **"Upload"** y sube la carpeta `tabla-quirurgica`
4. Copia la URL que te entrega (ej: `https://tabla-mano.vercel.app`)
5. Vuelve al Paso 4 y añade esa URL en los "Orígenes autorizados"

### Opción B — Abrir localmente (solo para pruebas)
Abre el archivo `index.html` directamente en Chrome. Funciona para una sola persona sin servidor.

---

## Notas adicionales

- **Radiografías:** se guardan en el navegador local (localStorage). No se sincronizan entre computadores en esta versión. En la próxima versión se pueden subir a Google Drive.
- **Múltiples usuarios:** cada miembro del equipo debe abrir la app e iniciar sesión con su cuenta Google (que debe estar en la lista de usuarios de prueba del Paso 3).
- **Nuevo mes:** cuando cambie el mes, crea una nueva pestaña en la hoja quirúrgica (ej: "Julio 2026") y actualiza el nombre en la app desde Configuración.

---

¿Dudas? Consulta la documentación de Google Cloud: https://developers.google.com/identity/oauth2/web/guides/overview
