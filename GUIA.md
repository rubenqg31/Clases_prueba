# Cómo publicar tu web de clases particulares

Tienes tres archivos:

- `index.html`: la página web.
- `firestore.rules`: las reglas de seguridad de la base de datos.
- `GUIA.md`: esta guía.

La página vive en **GitHub Pages** (gratis) y guarda los datos en **Firebase** (gratis a esta escala, no pide tarjeta).

---

## Paso 0 · Pruébala ya, sin configurar nada

Descarga `index.html` y haz doble clic en él. Se abre en tu navegador en **modo demostración**: todo se guarda solo en ese navegador.

1. Pulsa **Acceso para el profesor** (al pie de la página) y luego **Entrar**.
2. En **Horario y precio**, marca unas horas y guarda.
3. Pulsa **Cerrar sesión**: ahora eres un alumno. Pide una clase.
4. Vuelve a entrar como profesor y acéptala o recházala.
5. Sal otra vez: verás el aviso que le llega al alumno.

---

## Paso 1 · Crea el proyecto en Firebase

1. Entra en <https://console.firebase.google.com> con tu cuenta de Google.
2. Pulsa **Crear un proyecto**, ponle un nombre (por ejemplo `clases-particulares`) y desactiva Google Analytics; no hace falta.

## Paso 2 · Activa los inicios de sesión

1. En el menú izquierdo: **Compilación → Authentication → Comenzar**.
2. En **Método de acceso**, activa estos dos:
   - **Anónimo**, que usan los alumnos sin crear cuenta.
   - **Correo electrónico/contraseña**, que usarás tú.
3. Ve a la pestaña **Usuarios → Agregar usuario**. Pon tu email y una contraseña, que es la que usarás para entrar como profesor.
4. En la lista aparece tu usuario con un **UID** (un código largo). **Cópialo**; lo necesitas en los pasos 4 y 5.

## Paso 3 · Crea la base de datos

1. En el menú: **Compilación → Firestore Database → Crear base de datos**.
2. Ubicación: elige **europe-southwest1 (Madrid)**, o cualquiera de Europa.
3. Elige **Modo de producción**.

## Paso 4 · Pega las reglas de seguridad

1. En Firestore, abre la pestaña **Reglas**.
2. Borra lo que haya y pega todo el contenido de `firestore.rules`.
3. Sustituye `PEGA_AQUI_TU_UID` por tu UID del paso 2. Mantén las comillas.
4. Pulsa **Publicar**.

## Paso 5 · Conecta la página con Firebase

1. Pulsa el engranaje ⚙️ (arriba a la izquierda) y abre **Configuración del proyecto**.
2. Abajo, en **Tus apps**, pulsa el icono **`</>`** (Web). Ponle un nombre y pulsa **Registrar app**. No marques Firebase Hosting.
3. Te mostrará un bloque `const firebaseConfig = { apiKey: ..., authDomain: ..., ... }`.
4. Abre `index.html` con un editor de texto (el Bloc de notas vale). Busca el apartado **CONFIGURACIÓN**, casi al principio del bloque `<script>`:
   - Sustituye los valores `PEGA_AQUI` de `FIREBASE_CONFIG` por los tuyos.
   - Sustituye `PEGA_AQUI_TU_UID` en `UID_PROFESOR` por tu UID.
5. Guarda el archivo.

> Es normal que la `apiKey` quede visible en la página: no es una contraseña. Lo que protege tus datos son las reglas del paso 4.

## Paso 6 · Súbela a GitHub Pages

Tu web ya está en el repositorio `Clases_prueba`, así que no hace falta crear otro.

1. Para guardar tus cambios de `index.html` (el paso 5), ábrelo en GitHub, pulsa el lápiz ✏️, pega tus valores y pulsa **Commit changes**.
2. El repositorio tiene que ser **público**: **Settings → General**, abajo del todo, **Change visibility → Public**.
3. Ve a **Settings → Pages**. En **Branch**, elige `main` y la carpeta `/ (root)`, y pulsa **Save**.
4. En uno o dos minutos tu web estará en:
   `https://rubenqg31.github.io/Clases_prueba/`

## Paso 7 · Autoriza tu dominio en Firebase

En Firebase: **Authentication → Configuración → Dominios autorizados → Agregar dominio**. Escribe `rubenqg31.github.io` (sin `https://` ni carpeta).

## Paso 8 · Pruébala de verdad

1. Abre tu web y pulsa **Acceso para el profesor**. Entra con tu email y contraseña.
2. En **Horario y precio**, pon tus datos y horas, y guarda.
3. Abre la web desde el móvil (o en una ventana de incógnito) y pide una clase como si fueras un alumno.
4. En tu sesión de profesor aparecerá en **Solicitudes**. Acéptala y mira cómo le llega el aviso al "alumno".

---

## Cosas a tener en cuenta

- **Los alumnos no necesitan cuenta.** Su historial de solicitudes queda ligado a su dispositivo y navegador. Si abren la web desde otro móvil, no verán sus solicitudes anteriores, pero tú sí las tienes todas.
- **El aviso al alumno aparece en la propia web**, no por email. Por eso el formulario pide teléfono o email: puedes escribirle tú para confirmar.
- **Para cambiar algo de la página**, edita `index.html` en GitHub con el lápiz ✏️ y pulsa **Commit changes**. La web se actualiza sola en un par de minutos.
