
### 1.1. Roles del sistema

- **Alumno:**
    - Inicia sesión con su correo institucional (Microsoft 365 OAuth2).
    - Se inscribe a:
        - Una actividad relacionada con su carrera (congreso o conferencia).
        - Una actividad extracurricular (videojuegos, deportes, etc.).
    - Visualiza su horario de actividades inscritas.
    - Genera códigos QR para asistir a cada sesión.
- **Administrador/Organizador:**
    - Gestiona las actividades, conferencias (crear, editar, eliminar).
    - Controla el registro de asistencia mediante escaneo de códigos QR.
    - Valida asistencia (incluyendo llegadas tardías hasta 30 min).
    - Genera reportes en PDF y Excel.
    - Visualiza estadísticas de participación.

- **Ponente:**
    - No tiene acceso al sistema. Su participación es informativa.

### 1.2. Inscripción y validaciones

- Solo se permite inscribirse a dos actividades:
    - Una de tipo "académica".
    - Una de tipo "extracurricular".
- El sistema valida:
    - Que no existan empalmes en horarios.
    - Que haya cupo disponible.
    - Que no repita tipo de actividad.
- Las inscripciones solo están disponibles durante el periodo habilitado.
    

### 1.3. Asistencia
- Se debe asistir a **todos los congresos y conferencias** del programa.
- Los QR:
    - Se generan desde el portal del alumno.
    - Contienen identificador encriptado, nombre y fecha.
    - Tienen una duración de 1 hora.
    - Se validan desde el celular del administrador.
- El sistema registra hora y fecha de escaneo.
    

### 1.4. Comunicación
- Enviar correos de:
    - Confirmación de inscripción.
    - Recordatorio previo a la actividad.
    - Resumen semanal si es necesario.
- Notificaciones internas al ingresar al sistema.
    

### 1.5. Reportes y estadísticas

- Por actividad:
    - Lista de inscritos.
    - Lista de asistencia.
    - Exportación en PDF y Excel.
        
- Generales:
    - Total de asistencias por actividad.
    - Porcentaje de cumplimiento.
    - Número de estudiantes que cumplieron con todos los requisitos.