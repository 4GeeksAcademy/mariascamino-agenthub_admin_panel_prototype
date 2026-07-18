# AgentHub Admin Panel - Especificación Técnica (SPECS.md)

Este documento sirve como el contrato de diseño y comportamiento interactivo para el prototipo del panel de administración de AgentHub.

## 1. Descripción del Producto
AgentHub es una plataforma SaaS donde las empresas pueden alquilar agentes de IA preconfigurados con habilidades específicas (lectura de documentos, navegación web, gestión de calendarios). El Panel de Administración permite a los operadores internos monitorear ingresos, gestionar cuentas de usuario, configurar prompts del sistema de los agentes, catalogar habilidades disponibles, auditar contratos de alquiler y revisar logs de errores en tiempo de ejecución.

## 2. Stack Tecnológico y Restricciones
- **HTML5 Semántico**: Uso estricto de etiquetas como `<aside>`, `<header>`, `<main>`, `<section>` y `<table>`.
- **Styling**: Tailwind CSS cargado únicamente mediante CDN oficial. No se permiten archivos CSS externos ni atributos `style` en línea.
- **Interactividad**: Vanilla JavaScript puro. Sin frameworks (no React, Vue, jQuery) ni herramientas de compilación.
- **Persistencia de Datos**: Datos 100% hardcoded y consistentes entre las vistas del prototipo.
- **Soporte de Tema**: Toggle global de modo claro y oscuro controlado mediante la clase `.dark` en la etiqueta de raíz (`<html>`).

---

## 3. Especificaciones de las Secciones (Mínimo 3 por Sección)

### 3.1. Dashboard (Panel Principal)
1. **Grid de Tarjetas Métricas**: Cuatro tarjetas con un layout responsive (1 columna en móvil, 2 en tablet, 4 en desktop) que muestran: Ingresos Totales (Mes), Pérdidas por Descuentos, Agentes Activos y Agentes en Falla. Cada tarjeta cuenta con un contenedor de icono con un color de acento temático y tipografía en negrita para el valor numérico.
2. **Placeholder del Gráfico Semanal**: Un área de visualización de ancho completo con borde discontinuo (`border-dashed`), un gráfico SVG estilizado que simula las ejecuciones con éxito y un texto descriptivo centrado.
3. **Persistencia Visual**: El estado general de los contadores numéricos (por ejemplo, 1 agente fallando y 3 activos) coincide exactamente con los listados de las secciones de Agentes y de Logs de Error.

### 3.2. Gestión de Usuarios
1. **Tabla de Datos**: Estructura de tabla semántica (`<table>`) con al menos 5 usuarios hardcoded que listan: Nombre, Email, Plan (Enterprise, Pro, Standard) y Estado (Activo, Suspendido).
2. **Menú de Acción Dinámico (⋮)**: Un botón de menú de tres puntos por fila que despliega un dropdown posicionado de manera absoluta con las opciones "Ver detalle" y "Eliminar".
3. **Modal de Detalle**: Al seleccionar "Ver detalle", se abre un modal superpuesto centrado con un fondo difuminado (`backdrop-blur-sm`). El modal muestra el avatar simulado, plan, estado de pago y fecha de registro del usuario. Puede cerrarse mediante un botón "Cerrar", un botón de "X" o haciendo clic en el backdrop.

### 3.3. Gestión de Agentes
1. **Tarjetas de Agentes**: Un listado de 4 agentes detallando: Nombre, Propietario (debe coincidir con la lista de usuarios), Estado operativo (Activo, Inactivo, Failing) y una lista colapsable de habilidades.
2. **Habilidades Colapsables**: Las habilidades de cada agente están ocultas por defecto. Al hacer clic en un control con icono de caret (▼/▲), se expande la lista hacia abajo de manera fluida utilizando transiciones de CSS (`transition-all`).
3. **Modal de Configuración**: La opción "Configurar" del menú de acción abre un modal con un área de texto editable (`<textarea>`) conteniendo el System Prompt del agente, simulando su reprogramación en vivo.

### 3.4. Catálogo de Habilidades
1. **Banner Informativo**: Un contenedor destacado (`bg-gradient-to-r`) al inicio de la sección que explica conceptualmente qué es una "Habilidad" dentro del ecosistema de AgentHub.
2. **Grid de Habilidades**: Cuatro tarjetas de habilidades que muestran: Categoría en badge, Nombre de la Habilidad, Descripción de uso y un contador del número de agentes que la tienen habilitada.
3. **Modal de Detalle Técnico**: La opción "Ver detalle" abre un modal mostrando el JSON Schema esperado para la entrada de datos de la API de dicha habilidad en un formato de código de programación.

### 3.5. Contratos de Alquiler
1. **Historial Financiero**: Una tabla con al menos 4 registros que muestra: Cliente, Agente Rentado, Fecha de Inicio, Fecha de Fin y el Monto Total Pagado.
2. **Desglose de Facturación**: La opción "Ver detalle" del dropdown de acción abre un modal con un recibo interactivo desglosado detallando el costo de la licencia base y el precio individualizado por cada habilidad alquilada.
3. **Consistencia de Datos**: Los nombres de los clientes y agentes vinculados coinciden estrictamente con los definidos en las secciones de Usuarios y Agentes.

### 3.6. Registro de Errores (Error Log)
1. **Historial de Excepciones**: Una tabla con al menos 6 entradas de error hardcoded que incluyen: Timestamp, Nombre del Agente, Tipo/Severidad (Critical, Warning, Info) en insignias de color, y Descripción corta.
2. **Visor de Stacktrace**: "Ver detalle" del menú abre un modal que simula un bloque de código terminal (`pre` / `code`) estilizado con fondo oscuro y texto en rojo para examinar el trace técnico del error.
3. **Resolución de Alertas**: La opción "Resolver" del dropdown de acción cambia dinámicamente el badge de error a un estado verde ("Resolved") y tacha el texto del log con un estilo visual atenuado.

---

## 4. Inventario de Componentes Compartidos
- **Sidebar**: Barra de navegación lateral fija con enlaces reactivos y estilos visuales de estado activo.
- **Tarjetas Métricas (Metric Cards)**: Paneles con bordes sutiles y sombras para destacar KPI importantes.
- **Dropdown de Acción**: Menú contextual absoluto de fila activado por el botón `⋮`. Se cierra al hacer clic fuera de él.
- **Modal de Superposición (Overlay Modal)**: Estructura centralizada reutilizable para renderizar detalles de forma dinámica con cierre por backdrop.
- **Badges Semánticos**: Insignias redondeadas de colores para indicar estados (Emerald, Rose, Amber, Purple, Blue, Slate).

---

## 5. Criterios de Aceptación
1. **Funcionamiento SPA**: Al cambiar de sección en el Sidebar, se ocultan y muestran las secciones mediante clases de Tailwind sin provocar un refresco de página.
2. **Toggle de Color**: El interruptor de modo claro/oscuro altera la clase `.dark` del documento de manera global y el estado del color se mantiene intacto al navegar por las secciones.
3. **Comportamiento Dropdown**: Solo un menú de acción `⋮` puede estar abierto a la vez en toda la aplicación. Se cierra automáticamente al dar clic fuera de su contenedor.
4. **Cierre de Modales**: Todos los modales deben poder cerrarse al hacer clic en el botón con la "X", en el botón "Cerrar" del pie de página, o directamente sobre el fondo oscuro y difuminado de la pantalla.
