# AGENDA DE ENTREVISTAS — v0.1.0

Aplicación web responsive con Firebase Authentication y Cloud Firestore.

## Incluido en esta primera iteración
- Inicio de sesión y cierre de sesión con correo y contraseña.
- Registro de cuenta con nombre y nombre de usuario.
- Perfil inicial con rol `pending` (sin privilegios por defecto).
- Recuperación de contraseña por correo.
- Dashboard inicial conectado a Firestore.
- Creación y listado inicial de calendarios para el administrador principal.
- Reglas iniciales de Firestore con denegación por defecto para colecciones aún no implementadas.

## Configuración necesaria en Firebase Console
1. Crear un proyecto Firebase.
2. Registrar una aplicación web y copiar su configuración.
3. Activar Authentication > Sign-in method > Email/Password.
4. Crear Firestore Database.
5. Publicar `firestore.rules` en Firestore > Rules.
6. En `index.html`, sustituir los valores `REEMPLAZAR_...` de `firebaseConfig`.
7. En `.firebaserc`, sustituir `REEMPLAZAR_PROJECT_ID`.

## Primer administrador
Por seguridad, los registros públicos se crean con rol `pending`. Después de registrar la cuenta que será propietaria, un administrador del proyecto debe cambiar manualmente en Firestore el documento `users/{UID}`:

- `role`: `admin`
- `status`: `active`

No se debe permitir que el usuario se asigne a sí mismo el rol de administrador desde el navegador. En una siguiente iteración se añadirá la gestión de usuarios mediante funciones backend protegidas.

## Nota sobre el acceso por nombre de usuario
El nombre de usuario se registra y se reserva de forma única. El inicio de sesión de esta primera entrega usa correo y contraseña de Firebase Authentication. El acceso seguro con nombre de usuario se implementará mediante una función backend en la siguiente iteración; no se expondrán correos electrónicos en una consulta pública de Firestore.

## Publicación
Este proyecto está preparado para Firebase Hosting. La publicación inicial puede hacerse desde Firebase Console/flujo de despliegue configurado para el repositorio. No contiene dependencias de Node necesarias para el navegador: Firebase SDK se carga desde CDN.
