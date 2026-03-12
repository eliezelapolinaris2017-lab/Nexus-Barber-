# Nexus Salón V6 Auth

Incluye:
- Login real con email y contraseña usando Firebase Auth
- Crear usuario desde la app
- Indicador visible de sincronización
- Datos separados por usuario autenticado
- Configuración guardada por usuario
- Servicios guardados por usuario
- Citas sincronizadas por usuario

## Cómo conectarlo con X email
1. En Firebase Console abre **Authentication**
2. Activa **Email/Password**
3. Publica esta app
4. En la pantalla inicial escribe tu email y contraseña
5. Pulsa **Crear acceso** la primera vez
6. Luego entra con ese mismo email
7. Después te pedirá el PIN de tu negocio

## Cómo saber si está conectado
Arriba verás un badge:
- **Conectando / Sincronizando**
- **Sync activo**
- **Error sync**

## Firestore esperado
- `users/{uid}` guarda nombre negocio, PIN y servicios
- `users/{uid}/appointments/{appointmentId}` guarda citas

## Reglas mínimas recomendadas
```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      match /appointments/{appointmentId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}
```
