# CANON DEL PROYECTO EDUALERTA

Este documento define las reglas de diseño, arquitectura y requerimientos funcionales para EduAlerta. Debe respetarse en todas las modificaciones futuras.

---

## 1. Arquitectura Multi-Página
- **index.html**: Pantalla de Login institucional. No mezcla dashboards. Valida y redirige a la página exclusiva según el perfil.
- **familia.html**: Panel exclusivo para Padres / Tutores Familiares.
- **docente.html**: Panel exclusivo para Docentes.
- **directivo.html**: Panel exclusivo para Equipos Directivos Institucionales.
- **admin_red.html**: Panel exclusivo para el Gerente / Tutor Legal del Consorcio (Red de Colegios del Sur).
- Cada página cuenta con su botón de **Cerrar Sesión** que vuelve a `index.html`.

---

## 2. Paleta de Colores y Sistema Visual
- **Fondo General**: Claro y limpio (`#F8FAFC` o blanco).
- **Tipografía**: `Plus Jakarta Sans` o `Inter`.
- **Color Primario (Acciones/Branding)**: Azul eléctrico `#0066FF`.
- **Color de Títulos/Texto Principal**: Azul marino muy oscuro / pizarra `#001433`.
- **Tarjetas de Estado (Wireframe 2 & 3)**:
  - **Alerta Crítica**: Fondo rosa pastel (`#FFF0F0`), acentos e iconos rojos (`#E53E3E`).
  - **En Seguimiento**: Fondo ámbar pastel (`#FFFBEB`), acentos e iconos ámbar (`#D97706`).
  - **Trayectoria Regular / Sin Alerta**: Fondo verde pastel (`#F0FDF4`), acentos e iconos verde (`#059669` / `#52B788`).
- **Logo Institucional**: Birrete azul + "EduAlerta" (`WhatsApp Image 2026-10-04 at 11.24.07.jpeg`).
- **Ilustración Escolar**: Edificio escolar con tejado celeste y árboles verdes (`ESCUELA`).

---

## 3. Responsive & Controles de Navegación
- **Menú Hamburguesa**: **Solo visible en pantallas móviles o menores a 720px** (`hidden max-[720px]:block` o `block md:hidden`). En pantallas de escritorio (>= 720px) no debe mostrarse el menú hamburguesa innecesario; se visualiza la barra institucional limpia.
- **Formularios de Login**: En desktop (>= 1024px) se disponen los roles a los costados de la tarjeta (2 a la izquierda, 2 a la derecha) o mediante selector desplegable rápido para que la página no se extienda excesivamente hacia abajo. En móvil, se apilan de forma compacta y balanceada.

---

## 4. Requerimientos Nutritivos por Rol

### A. Familia / Tutor (`familia.html`)
- Alumno a cargo: Lautaro Martínez (4° Año B).
- **Selector bimestral** (1° a 4° Bimestre del año 2026).
- **Tabla completa de materias** con:
  - Nombre de la materia y docente titular.
  - Nota parcial y cierre bimestral.
  - Inasistencias en esa materia.
  - Estado de aprobación / seguimiento.
- **Métricas:** Asistencia semanal, promedio general bimestral, participación en clase.
- **Gráfico de evolución de asistencia** (curva porcentual 100% -> 75% -> 50% -> 30%).
- **Gestión de Inasistencias:** Modal para justificar faltas y adjuntar certificado.
- **Canales de contacto directo nativos:** Llamar (`tel:`) y WhatsApp (`wa.me`) con el Docente, Directora y Cooperadora.

### B. Docente (`docente.html`)
- Cátedra: Matemática - 4° Año División B (28 alumnos).
- Selector bimestral (2026).
- Métricas del curso: Promedio general, tasa de aprobación %, estudiantes en alerta y en seguimiento.
- Gráfico de barras apiladas mensual por condición (Alerta / Seguimiento / Sin alerta).
- Nómina completa de alumnos con nota, inasistencias y botones para Llamar (`tel:`) y WhatsApp (`wa.me`) a la familia.
- Modal para registrar observaciones pedagógicas.

### C. Directivo Escolar (`directivo.html`)
- Establecimiento: Escuela Secundaria N° 12 (243 alumnos en 10 divisiones, 26 docentes).
- Métricas de toda la escuela: Asistencia institucional general, retención de matrícula, tasa de aprobación, alertas críticas de deserción.
- Gráfico de distribución de alertas en los 5 años (1° a 5°).
- **Detalle de cada docente:**
  - Materias que dicta y cursos a cargo.
  - **Faltas acumuladas del docente en el año.**
  - **Calendario / días de trabajo** (ej: Lunes, Miércoles, Viernes 7:30 a 12:40).
  - **Cantidad de alumnos a cargo.**
  - Estado de carga del libro de temas y notas.
  - Botones de contacto directo (llamada y WhatsApp).
- Casos prioritarios de alerta de la escuela con contacto inmediato a las familias.
- Canal directo con la Gerencia de la Red del Sur.

### D. Gerente / Tutor Legal de la Red (`admin_red.html`)
- Alcance: 5 Colegios Asociados (1.420 alumnos).
- Métricas consolidadas: Inversión USD 127K, ingresos SaaS USD 42.6K/año, break-even Mes 14, retención 96.8%.
- **Navegación interactiva por Colegio:**
  - Posibilidad de seleccionar cualquiera de las 5 sedes (Palermo, Belgrano, San Isidro, Quilmes, Lomas de Zamora).
  - Al ingresar a un colegio, ver:
    * Métricas específicas de esa sede (matrícula, retención, alertas).
    * Responsable directivo (nombre, teléfono, WhatsApp, mail).
## 5. Favicon y Pestaña del Navegador
- En el `<head>` de todas las páginas HTML se debe incluir el icono oficial de EduAlerta:
  `<link rel="icon" type="image/jpeg" href="WhatsApp Image 2026-10-04 at 11.24.07.jpeg">`.

---

## 6. Visualización Gráfica Flexible (Barras y Torta)
- Los dashboards que exhiben distribución de alumnos, alertas o sedes deben permitir al usuario alternar entre:
  - **Gráfico de Barras** (comparativo mensual o por división/sede).
  - **Gráfico de Torta / Donut** (SVG interactivo que muestre el desglose porcentual de Alertas, En seguimiento y Sin alertas/Regulares).
- Controles de selección limpios y accesibles en la cabecera de la tarjeta del gráfico.

---

## 7. Densidad Funcional y Notificaciones Interconectadas
- La aplicación debe transmitir sensación de robustez, completitud y contenido vivo:
  - **Docente:**
    - Carga de Inasistencias con selección de estudiante, fecha y motivo.
    - Carga de Calificaciones con cálculo automático y observaciones.
    - **Disparador de Notificación:** Al registrar una falta o una nota, el sistema emite una notificación que se almacena en `localStorage` (`edualerta_notificaciones`) y simula un despacho push y por WhatsApp a la familia.
  - **Familia:**
    - **Centro de Notificaciones en vivo** con badge en la campanita que recibe las alertas generadas por el docente.
    - Calendario de exámenes bimestrales y fechas clave.
    - Historial de comunicados institucionales y estado de cuota cooperadora.
  - **Directivo:**
    - Monitor de ausentismo docente del día y suplencias.
    - Registro de convivencia y actas institucionales.
    - Calendario escolar y reporte exportable.
  - **Gerente de Red:**
    - Matriz financiera SaaS (USD 127K inversión, USD 42.6K SaaS anual, Mes 14 break-even).
    - Desglose profundo e interactivo de las 5 sedes con directores y docentes.

---

## 8. Sistema Estético de Notificaciones (Toasts vs Alert Nativo)
- **Prohibido el uso de `alert(...)` nativo del navegador:** Causa una experiencia tosca y desalineada con la identidad visual.
- **Sistema Universal `mostrarToast(mensaje, tipo, titulo)`:**
  - Componente flotante elegante con esquinas redondeadas (`rounded-2xl`), fondo suave con borde temático (verde para `success`, rojo para `error`, ámbar para `warning`, azul para `info`), icono FontAwesome y texto jerárquico.
  - Auto-desvanecimiento fluido en 3.5 a 4 segundos o cierre manual con botón discreto.

---

## 10. Vista de Torta / Donut como Predeterminada Universal
- En **todas las pantallas con dashboard analítico** (`admin_red.html`, `directivo.html`, `docente.html`, `familia.html`), la vista en formato **Torta / Donut (`chart-pie`)** debe cargarse activa y visible por defecto.
- El usuario puede alternar a barras/curvas si lo desea, pero la experiencia inicial siempre prioriza la síntesis visual de torta.

---

## 11. Jerarquía y Permisos Estrictos de Contacto
- **Docente:**
  - El docente **NO puede llamar por teléfono al padre/tutor** (`tel:` prohibido para docentes).
  - El docente se comunica exclusivamente mediante **Correo Electrónico Institucional (`mailto:`)** con asunto y cuerpo predefinido de seguimiento pedagógico, y canal WhatsApp institucional.
- **Directivo:**
  - La dirección escolar sí cuenta con la atribución de realizar **llamadas telefónicas directas (`tel:`)** a las familias de estudiantes en riesgo crítico de deserción o inasistencias reiteradas.

---

## 12. Presentación No Invasiva de Alertas a Familias
- Prohibidos los banners fijos o sticky persistentes en la parte superior que resten espacio visual y generen mala sensación.
- Al ingresar la familia al portal, si existen alertas pendientes sin leer, el sistema dispara automáticamente una **notificación flotante suave (toast)** que dura 4 segundos y se auto-cierra de forma limpia. El conteo permanece en el badge de la campanita para consulta manual.

---

## 13. Supervisión Integral por Colegio en Gerencia de Red
- Cada colegio de la Red del Sur seleccionado en `admin_red.html` debe exponer una radiografía completa de 4 niveles:
  1. **Equipo Directivo de la Sede:** Director/a, Vicedirector/a, Secretario/a Académico con canales de contacto.
  2. **Grados y Divisiones:** Listado de todas las divisiones (1° a 5° Año, turnos Mañana y Tarde, preceptores asignados, cupos y cantidad de alertas).
  3. **Plantel Docente y Cátedras:** Profesores titulares, materias y cursos a cargo.
  4. **Nómina de Alumnos en Seguimiento:** Casos prioritarios con asistencia, promedio y contacto con el tutor.

---

## 14. Estandarización de Navbars
- Todos los encabezados (`<header>`) en los 4 perfiles deben conservar la misma estructura simétrica y limpia:
  - **Izquierda:** Botón hamburguesa (sólo `<720px`), Logo oficial de EduAlerta, separador y título descriptivo del rol.
  - **Derecha:** Contenedor agrupado `flex items-center space-x-3 sm:space-x-4` que alberga consecutivamente:
    1. Campanita de notificaciones interactivas con badge de no leídas.
    2. Avatar y nombre del usuario logueado.
    3. Botón de cierre de sesión hacia `index.html`.


