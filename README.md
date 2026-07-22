# 🏠 Rellano

**Tu comunidad de vecinos en el bolsillo**

App PWA para comunidades de vecinos con alertas de coches, tablón de anuncios, reservas de zonas comunes, gestión de paquetería y parking.

## 🚀 Setup

### 1. Crear proyecto Firebase

1. Ve a [Firebase Console](https://console.firebase.google.com/)
2. Crea un nuevo proyecto llamado "rellano"
3. Activa **Authentication** → Email/Password
4. Activa **Cloud Firestore** → Crear base de datos (modo producción)
5. Copia las reglas de `firestore.rules` en Firestore → Rules
6. Crea los índices necesarios (Firestore te los pedirá en la consola del navegador)

### 2. Configurar la app

En `index.html`, busca el bloque `firebaseConfig` y rellena con tus datos:

```javascript
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROYECTO.firebaseapp.com",
  projectId: "TU_PROYECTO",
  storageBucket: "TU_PROYECTO.appspot.com",
  messagingSenderId: "TU_SENDER_ID",
  appId: "TU_APP_ID"
};
```

Los datos los encuentras en Firebase Console → Configuración del proyecto → Tu app web.

### 3. Deploy en GitHub Pages

```bash
git init
git add .
git commit -m "Rellano v1"
git remote add origin https://github.com/TU_USUARIO/rellano.git
git push -u origin main
```

En GitHub → Settings → Pages → Source: main branch → /root

### 4. Primer uso

1. Abre la app y regístrate
2. El primer usuario que se registre con un código de comunidad se convierte en **admin**
3. Comparte el código con tus vecinos para que se unan
4. Cada vecino puede añadir sus matrículas

## 📁 Estructura Firestore

```
users/{userId}
  - name, email, unit, communityId, role, createdAt

communities/{communityId}
  - name, code, createdAt
  
  /plates/{plateId}
    - plate, userId, spot, createdAt
  
  /alerts/{alertId}
    - plate, type, note, reporterId, reporterName, createdAt
  
  /notifications/{notifId}
    - userId, type, icon, title, desc, read, createdAt
  
  /posts/{postId}
    - text, tag, authorId, authorName, authorUnit, authorRole
    - likes, comments, pinned, createdAt
  
  /reservations/{resId}
    - spaceId, spaceName, date, slot, userId, userName, userUnit, createdAt
  
  /packages/{pkgId}
    - carrier, desc, code, status, userId, createdAt
  
  /available_spots/{spotId}
    - spot, ownerId, ownerName, ownerUnit, note, createdAt
```

## 🔧 Índices Firestore necesarios

Firestore te pedirá crear estos índices compuestos (aparecerán como errores en la consola del navegador con un link directo para crearlos):

- `notifications`: userId + read + createdAt
- `notifications`: userId + createdAt
- `posts`: createdAt (desc)
- `packages`: userId + createdAt
- `reservations`: spaceId + date

## 📱 Módulos

| Módulo | Estado |
|--------|--------|
| Auth (registro/login) | ✅ Funcional |
| Alertas de coches | ✅ Funcional |
| Tablón de anuncios | ✅ Funcional |
| Reservas zonas comunes | ✅ Funcional |
| Gestión de matrículas | ✅ Funcional |
| Notificaciones | ✅ Funcional |
| Paquetería | ✅ Estructura (admin crea) |
| Parking | ✅ Estructura |
| Documentos | 🔜 Próximamente |
| Votaciones | 🔜 Próximamente |
| Averías | 🔜 Próximamente |
| Contactos | 🔜 Próximamente |
| Cuotas/Pagos | 🔜 Próximamente |
