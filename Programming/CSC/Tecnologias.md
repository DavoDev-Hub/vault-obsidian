Frontend

| Herramienta      | ¿Para qué sirve?                               | ¿Por qué usarla?                                                                 |
| ---------------- | ---------------------------------------------- | -------------------------------------------------------------------------------- |
| **React.js**     | Biblioteca para construir interfaces web.      | Es la más demandada a nivel global. Hay muchas vacantes para React.              |
| **Vite**         | Build tool para React (más rápido que CRA).    | Rápido, moderno y recomendado por la comunidad actual.                           |
| **TypeScript**   | Lenguaje con tipado estático (superset de JS). | Mejora la calidad del código y es muy valorado en vacantes frontend y fullstack. |
| **Tailwind CSS** | Framework de utilidades CSS.                   | Permite construir interfaces modernas rápido y sin escribir CSS clásico.         |
|                  |                                                |                                                                                  |

**Extras recomendados:**

- `react-router-dom` → para rutas internas.
- `axios` o `fetch` → para llamadas al backend.
- `zod` o `yup` → para validaciones de formularios.

Backend

|Herramienta|¿Para qué sirve?|¿Por qué usarla?|
|---|---|---|
|**Node.js**|Entorno de ejecución para JavaScript/TS.|Muy usado, ideal para construir servidores API rápidos.|
|**Express.js**|Framework minimalista para servidores.|Sencillo, flexible, aún muy demandado en el mercado.|
|**TypeScript**|Tipado estático en backend.|Te da experiencia con buenas prácticas y reduce errores.|
|**Prisma ORM**|Mapeo de datos entre TS y PostgreSQL.|Popular, moderno, con autocompletado inteligente y migraciones fáciles.|
|**Nodemailer** + **Microsoft Graph API**|Envío de correos.|Fundamental para sistemas con notificaciones. Microsoft Graph se integra con correos institucionales.|
|**jsonwebtoken (JWT)**|Para sesiones si usas login alternativo a Microsoft.|Común en APIs modernas.|

**Autenticación**

|Herramienta|¿Para qué sirve?|¿Por qué usarla?|
|---|---|---|
|**Microsoft OAuth2 (Azure AD)**|Login con correo institucional.|Experiencia profesional. Aprendes cómo se autentican apps reales en entornos corporativos.|

Base de datos

| Herramienta    | ¿Para qué sirve?                   | ¿Por qué usarla?                                                        |
| -------------- | ---------------------------------- | ----------------------------------------------------------------------- |
| **PostgreSQL** | Base de datos relacional robusta.  | Una de las más usadas en el mundo laboral. Ideal para proyectos serios. |
| **Prisma ORM** | Conexión eficiente con PostgreSQL. | Facilita el trabajo con TypeScript + PostgreSQL.                        |

**Despliegue**

| Herramienta          | ¿Para qué sirve?                          | ¿Por qué usarla?                                                                                 |
| -------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Vercel**           | Hospedar frontend moderno (React + Vite). | Gratis, rápido y muy usado para frontends modernos.                                              |
| **Railway / Render** | Hospedar backend Node + PostgreSQL.       | Fácil de usar, gratuito con límites. Te introduce al mundo DevOps ligero.                        |
| **Azure (opcional)** | Alternativa empresarial.                  | Si quieres experiencia real con la nube de Microsoft. Ideal si haces login con OAuth2 Microsoft. |

**Desarrollo y pruebas**

| Herramienta                  | ¿Para qué sirve?                 | ¿Por qué usarla?                              |
| ---------------------------- | -------------------------------- | --------------------------------------------- |
| **Postman / Thunder Client** | Probar tu API REST sin frontend. | Imprescindible para backend y debugging.      |
| **Jest / Vitest (opcional)** | Pruebas automatizadas.           | Plus para tu CV si aprendes testing desde ya. |

Herramientas de desarrollo

| Herramienta           | ¿Para qué sirve?                                                        |
| --------------------- | ----------------------------------------------------------------------- |
| **Git + GitHub**      | Control de versiones y portafolio público.                              |
| **Docker (opcional)** | Para empaquetar tu app y desplegar fácilmente. Muy buscado en empresas. |


Ruta de implementación sugerida

- **Configurar backend Node + TS + Express**
- Integrar Prisma y PostgreSQL
- Agregar endpoints (actividades, QR, asistencia, etc.)
- Configurar login Microsoft OAuth
- Crear frontend con React + Vite + Tailwind
- Conectar al backend
- Desplegar frontend y backend en Vercel + Railway/Azure

