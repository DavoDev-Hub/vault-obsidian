### 2.1. Tecnologías propuestas

- **Frontend:** React o Vue.js con Tailwind CSS.
- **Backend:** Node.js + Express o Spring Boot.
- **Base de datos:** PostgreSQL.
- **Autenticación:** OAuth2 con Azure AD (Microsoft 365).
- **Correo:** Microsoft Graph API o SMTP institucional.
- **Despliegue:** Azure, Render o Vercel.


### 2.2. Seguridad

- Validación de identidad vía correo institucional
- Expiración de QR para evitar reutilización.
- Validación de QR contra backend para evitar falsificación.
- Autorización por roles.

### 2.3. Disponibilidad

- Acceso desde navegador y dispositivos móviles.
- Se recomienda conexión a internet para escaneo de QR, pero se considerará una versión offline como mejora futura.

### 2.4. Mantenibilidad y escalabilidad

- Arquitectura de tres capas (frontend, backend, base de datos).
- Diseño modular para facilitar la incorporación de nuevas funcionalidades.