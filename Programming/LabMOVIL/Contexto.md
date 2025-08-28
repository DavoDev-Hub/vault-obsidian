# Guía de orientación — labmovilloginback (backend de LabMovil)

---
## 1) Resumen del proyecto

Backend en **Node.js + Express (TypeScript)** que autentica usuarios contra **LDAP (Active Directory)**, consulta información académica en **Oracle** y persiste datos de la app en **MongoDB** (vía Mongoose). Expone endpoints para:

- **Autenticación de usuarios y administradores** (vía LDAP) y emisión de **JWT**.
- **Gestión de usuarios** (búsquedas y datos de contexto).
- **Gestión de equipos de cómputo** (estatus y alta de equipo).
- **Préstamos y devoluciones** de equipos.
- Rutas de **pruebas** para validar conectividad/queries.

**Entrypoint:** `index.ts`

**Middlewares clave:** CORS, parseo JSON/URL-encoded, validación (express-validator), verificación de **JWT** en el header `x-token`.

---

## 2) Stack y dependencias

**Runtime:** Node.js (Express 4.x)

**TypeScript:** sí (pero no viene `typescript` en `devDependencies`; ver “Cómo correr”)

**Paquetes principales (de `package.json`):**

- `express`, `cors`, `dotenv`, `express-validator`, `jsonwebtoken`
- **LDAP:** `ldap-authentication`
- **Oracle:** `oracledb`
- **MongoDB:** `mongoose`
- `moment`

**Nota:** el proyecto usa TypeScript (`.ts`), pero el `package.json` no define scripts de build/start ni incluye `typescript` ni `ts-node` como dependencias de desarrollo. Abajo propongo scripts para normalizarlo.

---

## 3) Estructura del repo y propósito

```
labmovilloginback-main/
├─ index.ts                        # Arranque del servidor y montaje de rutas
├─ classes/
│  ├─ servidor.ts                  # Clase Server (levanta Express; soporta HTTPS opcional comentado)
│  └─ token.ts                     # Utilidad para emitir y verificar JWT
├─ databases/
│  └─ dboracle.conf.ts             # Conexión a Oracle (OCI) y a Mongo (Mongoose)
├─ Models/
│  ├─ usuarios.ts                  # Esquema Usuario (Mongo)
│  ├─ administradores.ts           # Esquema Administrador (Mongo)
│  ├─ equiposcomputo.ts            # Esquema Equipos de Cómputo (Mongo)
│  ├─ estatusequipo.ts             # Esquema Estatus de Equipo (Mongo)
│  ├─ prestamos.ts                 # Esquema Préstamo (Mongo)
│  └─ solicitudes.ts               # Esquema Solicitud del día por usuario (Mongo)
├─ controller/
│  ├─ user.controller.ts           # Login usuario via LDAP + consulta Oracle + lógica Solicitud
│  ├─ administradores.controller.ts# Login administrador via LDAP + creación/listado admins
│  ├─ equipos.controller.ts        # Crear estatus, crear equipo, buscar equipo
│  ├─ prestamos.controller.ts      # Realizar préstamo, devolución, consultas
│  └─ pruebas.controller.ts        # Endpoints de prueba (query Oracle, obtención foto GVD, etc.)
├─ middleware/
│  ├─ validar_token.ts             # Middleware para validar JWT (header `x-token`)
│  ├─ validar_campos.ts            # Integra express-validator (manejo de errores de validación)
│  └─ validar_repetidos.ts         # Reglas de unicidad: equipo repetido, usuario con préstamo, etc.
├─ routes/
│  ├─ usuarios.ts                  # /user/*
│  ├─ administradores.ts           # /admin/*
│  ├─ equiposcomputo.ts            # /equipo/*
│  ├─ prestamos.ts                 # /prestamo/*
│  └─ pruebas.ts                   # /pruebas/*
├─ public/index.html               # Página simple “Acceso Denegado” (servida estáticamente)
├─ package.json, package-lock.json,
├─ tsconfig.json, README.md
└─ .gitignore, .gitattributes
```

**Montaje de rutas** (desde `index.ts`):

- `/pruebas` → `routes/pruebas.ts`
- `/user` → `routes/usuarios.ts`
- `/equipo` → `routes/equiposcomputo.ts`
- `/admin` → `routes/administradores.ts`
- `/prestamo` → `routes/prestamos.ts`

---

## 4) Variables de entorno (obligatorias)

Detectadas en código:

- `PORT` — Puerto donde levanta Express.
- `JWT_SECRET` — Secreto para firmar/verificar JWT.
- `MONGO_DB_CNN` — Cadena de conexión a MongoDB (Atlas o local).
- `ociUser`, `ociPass`, `ociURL` — Credenciales/DSN para Oracle (`oracledb`).
- `LDAPURL` — Host:puerto de tu servidor LDAP/AD (se arma `ldap://<LDAPURL>`).

**Ejemplo de `.env` (plantilla):**

```env
PORT=3000
JWT_SECRET=super-secreto-por-defecto
MONGO_DB_CNN=mongodb://usuario:pass@host:27017/labmovil
ociUser=USUARIO_ORACLE
ociPass=PASSWORD_ORACLE
ociURL=HOST_ORACLE:PUERTO/SERVICE_NAME
LDAPURL=ldap.midominio.local:389
```

> **Importante (seguridad):** Hay **credenciales LDAP de administrador hardcodeadas** en controladores (adminDn/adminPassword y bases de búsqueda). **Debes moverlas a variables de entorno** y retirar el secreto del repo. No copio esos valores aquí; están visibles en el código actual y deben **rotarse**.

---

## 5) Cómo correr el proyecto (local)

1. **Requisitos:**
    
    - Node.js 18+ (recomendado) y npm.
    - **Oracle Instant Client** instalado y accesible (Linux/macOS: `LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH`; Windows: en PATH). Necesario para el paquete `oracledb`.
    - Una instancia de **MongoDB** accesible por `MONGO_DB_CNN`.
    - Archivo `.env` con las variables anteriores.
    
2. **Instalar dependencias:**
    
```bash
    npm install
    ```
    
3. **Añadir herramientas de TypeScript (sugerido):**
    
```bash
    npm install --save-dev typescript ts-node @types/express @types/jsonwebtoken @types/cors     @types/express-validator
    ```
    
4. **Agregar scripts a `package.json` (sugerencia):**
    
    ```json
    "scripts": {
      "dev": "ts-node index.ts",
      "build": "tsc",
      "start": "node dist/index.js"
    }
    ```
    
    Y en `tsconfig.json`, confirma salida a `./dist` si compilas.
    
5. **Ejecutar en desarrollo:**

```bash
    npm run dev
    ```
    
    o compilar y ejecutar:
    
    ```bash
    npm run build && npm start
    ```
    

> **Tip:** Si te falla `oracledb`, suele ser por librerías de Oracle no encontradas. Verifica variables de entorno del Instant Client y que `ociURL` sea correcto.

---

## 6) Modelos (MongoDB)

### Usuario (`Models/usuarios.ts`)

Campos principales (parcial; el esquema es extenso):

- Identidad: `dn`, `usuarioname` (sAMAccountName), `correoedu`, `displayname`, `id` (ID interno), etc.
- Datos académicos: `carrera`, `grado`, `grupo`…
- Flags/fechas: varios, con manejo de fechas en **moment**.

### Administrador (`Models/administradores.ts`)

- `nombre` (String, requerido)
- `iduaa` (Number)
- `cuentaedu` (String)
- `fecharegistro` (auto con moment)

### Estatus de equipo (`Models/estatusequipo.ts`)

- `nombre` (String, req.)
- `descripcion` (String) 
- `creado` (auto con moment)

### Equipo de cómputo (`Models/equiposcomputo.ts`)

- `nombreequipo` (String, req.)
- `estatus` (ObjectId → `EstatusEquipo`, req.)
- `tipoequipo`, `numeroinventario`, `modelo`, `numeroserie`, `carga`, `lecturacarga`, `fecharegistro` (auto)

### Préstamo (`Models/prestamos.ts`)

- `usuarioId` (ObjectId → `Usuario`, req.)
- `equipoId` (ObjectId → `EquiposComputo`, req.)
- `usuarioAdm` (ObjectId → admin que registra)
- `fechainicio` (auto now), `fechafin` (auto now + 2h), `estatus` (bool)
### Solicitud (`Models/solicitudes.ts`)

- `usuario` (String, req. — se guarda un identificador tipo `al<ID>`)
- `estatus` (bool, default `true`)
- `fecharegistro` (Date auto; se usa para “una solicitud por día”)

---

## 7) Flujos clave

### A) Login de **Usuario** (`POST /user/login`)

1. Valida credenciales contra **LDAP** (`ldap-authentication`).
2. (Lógica anti-roles): evita admvo/prof si así lo determinan OU/grupos.
3. Consulta **Oracle** (vistas como `v_aluvig`) para verificar vigencia del alumno.
4. Crea/actualiza `Usuario` en Mongo con datos LDAP.
5. Garantiza **1 Solicitud activa por día** (`Solicitud`), creando una si no existe.
6. Responde con `ok`, **token JWT**, y datos del usuario.

### B) Login de **Administrador**

- Existen dos rutas:
    - `POST /admin/login` (por iduaa/correo; emite JWT si coincide con colección `Administradores`).
    - `POST /admin/loginadmin` (autenticación directa en **LDAP**). Verifica pertenencia a grupo **`gpo_labmovil`** u OU específica antes de permitir acceso. Retorna token y claims.

### C) Gestión de **Equipos**

- Crear estatus: `POST /equipo/crearestatus`
- Alta de equipo: `POST /equipo/crearequipo` (requiere JWT; valida `nombreequipo`, `estatus` es ObjectId válido, y unicidad `nombreequipo`).
- Búsqueda de equipo: `GET /equipo/findequipo` (query; ver controlador para filtros aceptados).

### D) **Préstamos**

- Crear préstamo: `POST /prestamo/crear` (JWT). Body: `usuarioId`, `equipoId`. Middlewares impiden préstamo si el **usuario ya tiene uno activo** o si el **equipo ya está prestado**.
- Devolución: `PUT /prestamo/devolucion` (JWT). Body: `idprestamo` (MongoId). Marca `estatus=false` y setea `fechafin`.
- Consultas:
    - `GET /prestamo/consultaprestamo?nombreequipo=...` (JWT) — busca préstamos por equipo.
    - `GET /prestamo/consulta` (JWT) — listado/consulta general.

### E) **Pruebas**
- `GET /pruebas/` — ejecuta query simple a Oracle.
- `GET /pruebas/foto` — ejemplo para obtener foto (GVD) por LDAP/Oracle (ver controlador).

---
## 8) Middlewares y validaciones
- **`verificaToken`**: lee `x-token`, valida JWT con `Token.comprobarToken` y coloca `req.usuario` (payload). Responde `{ ok:false, mensaje:'Token incorrecto' }` si falla.
- **`validar_campos`**: convierte errores de `express-validator` en respuesta 400 con `{ ok:false, errors:[...] }`.
- **`validar_repetidos`**: helpers usados como `body().custom(...)`:
    - `existeequipo(nombreequipo)` — evita alta de equipos duplicados.
    - `usuarioconprestamo(usuarioId)` — evita múltiples préstamos activos para un usuario.
    - `equipoprestado(equipoId)` — evita prestar equipo ya prestado.
    - `correorepetido(cuentaedu)` — evita admins con correo duplicado.

---

## 9) Endpoints (resumen práctico)
> **Todas las rutas marcadas 🔒 requieren JWT** en header `x-token`.
### Autenticación y usuarios (`/user`)

- `POST /user/login` — login de usuario (LDAP + Oracle). **Body**: `{ user, pass }`. **Resp**: `{ ok, token, usuario, ... }`.
- 🔒 `GET /user/finduser?idusuario=...` — busca detalle de usuario + su `Solicitud` vigente del día.
- 🔒 `GET /user/findusuarios?tipo=...&idusuario=...&page=1&limit=20` — búsqueda paginada.

### Administradores (`/admin`)

- 🔒 `POST /admin/crear` — crea admin. **Body**: `{ nombre, iduaa, cuentaedu }` (valida duplicados).
- `POST /admin/login` — login por datos del admin registrado en Mongo.
- `POST /admin/loginadmin` — login directo al LDAP (valida pertenencia a `gpo_labmovil`). **Body**: `{ user, pass }`.
- 🔒 `GET /admin/getadmins` — lista admins.
- 🔒 `GET /admin/getuser` — datos del admin autenticado.

### Equipos (`/equipo`)

- `POST /equipo/crearestatus` — crea estatus.
- 🔒 `POST /equipo/crearequipo` — alta de equipo. **Body**: `{ nombreequipo, estatus, ... }`.
- 🔒 `GET /equipo/findequipo?...` — consulta equipos.

### Préstamos (`/prestamo`)

- 🔒 `POST /prestamo/crear` — crear préstamo. **Body**: `{ usuarioId, equipoId }`.
- 🔒 `PUT /prestamo/devolucion` — cerrar préstamo. **Body**: `{ idprestamo }`.
- 🔒 `GET /prestamo/consultaprestamo?nombreequipo=...` — buscar préstamo por equipo.
- 🔒 `GET /prestamo/consulta` — consulta general.

### Pruebas (`/pruebas`)

- `GET /pruebas/` — ping con query a Oracle.
- `GET /pruebas/foto` — demo foto.

---

## 10) JWT y seguridad

- **Header esperado:** `x-token` en rutas 🔒.
- **Secreto:** `JWT_SECRET` (env). No uses el default del código en producción.
- **Credenciales LDAP hardcoded:** mover a `.env` (p. ej. `LDAP_ADMIN_DN`, `LDAP_ADMIN_PASS`, `LDAP_SEARCH_BASE`, etc.) y **rotar** inmediatamente los secretos ya expuestos.
- **HTTPS opcional:** en `classes/servidor.ts` hay bloque comentado para levantar HTTPS con certificados locales.

---

## 11) Cosas a corregir / pendientes técnicos

- `classes/servidor.ts`: typo en tipo `express.Aplication` → `express.Application`.
- Falta `typescript`/`ts-node` y scripts `dev/build/start` en `package.json`.
- Externalizar **todas** las constantes LDAP (adminDn, adminPassword, `userSearchBase`) a variables de entorno.
- Revisar si `mongoose` y `oracledb` se usan en **todas** las rutas; hay archivos con código comentado/ejemplo.
- `public/index.html`: solo “Acceso Denegado”; confirmar si debe servir como raíz.

---

## 12) Ejemplos de uso (curl)

### Login usuario

```bash
curl -X POST http://localhost:3000/user/login \
  -H 'Content-Type: application/json' \
  -d '{"user":"miusuario","pass":"miclave"}'
```

Responde `{ ok:true, token:"...", usuario:{...} }`.

### Alta de equipo (requiere JWT)

```bash
curl -X POST http://localhost:3000/equipo/crearequipo \
  -H 'Content-Type: application/json' \
  -H 'x-token: <TOKEN>' \
  -d '{"nombreequipo":"LAP-001","estatus":"<ObjectId>","modelo":"Dell 5410"}'
```

### Crear préstamo (requiere JWT)

```bash
curl -X POST http://localhost:3000/prestamo/crear \
  -H 'Content-Type: application/json' \
  -H 'x-token: <TOKEN>' \
  -d '{"usuarioId":"<ObjectId Usuario>","equipoId":"<ObjectId Equipo>"}'
```

---

## 13) ¿Por dónde empezar (sugerencia para ti)?

1. **Configurar `.env`** con tus endpoints de LDAP/Mongo/Oracle.
2. **Instalar** dependencias y herramientas TypeScript; agregar scripts.
3. **Probar `/pruebas/`** para confirmar que Oracle conecta.
4. **Probar `/user/login`** con un usuario real del LDAP.
5. **Crear un `Estatus` y un `Equipo`**, y validar flujos de préstamo/devolución.
6. **Revisar tus issues** con este mapa en mano (si quieres pásamelos y te hago el plan de ataque por issue).

---
## 14) Glosario rápido

- **Solicitud (modelo)**: registro diario por usuario; asegura una sola solicitud activa al día.
- **Préstamo activo**: `Prestamo.estatus === true`.
- **`x-token`**: header con JWT para rutas protegidas.

---
## 15) Notas extra

- Se usa `moment` para fechas (formato/español). Considerar migración a `luxon` o `Intl` si desean menos dependencias.
- La base Oracle usa vistas tipo `v_aluvig` para validar vigencia; si cambian nombres de vistas/columnas, ajusta la consulta en controladores.