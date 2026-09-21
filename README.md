# PixelVault - Tienda de Videojuegos Físicos (16-Bit Arcade & Steam Style)

**Evaluación Parcial 1 - Desarrollo Fullstack (DSY1104)**  
**Institución:** Escuela de Informática y Telecomunicaciones - DUOC UC  
**Equipo de Desarrollo Frontend:**
- **Jim Charles** - Líder Técnico & Arquitecto Frontend (Administrador)
- **Emanuel Reyes** - Ingeniero Frontend & Lógica Transaccional (Administrador)
- **Maximiliano Peral** - Desarrollador Frontend & UI/UX (Administrador)

---

## 🎮 Descripción del Proyecto
**PixelVault** es una plataforma web para la comercialización, gestión editorial, logística de despacho y administración integral de videojuegos en formato físico. Su diseño combina la elegancia e inmersión del tema oscuro de **Steam** con acentos visuales retro y efectos **16-bit arcade** (CRT scanlines, fuentes pixeladas y transiciones fluidas).

El frontend está construido enteramente con **Bootstrap v5.3.3** (CSS y componentes JS) y JavaScript nativo integrado en cada vista, siguiendo los lineamientos pedagógicos y la estructura limpia del estándar del curso (`proyecto_front`), sin dependencias de backend ni transpiladores. Toda la persistencia opera de forma reactiva en el navegador mediante `localStorage` y `sessionStorage`.

---

## 📁 Estructura del Repositorio

```text
Fullstack/
├── tienda_videojuegos/              # Aplicación Web Frontend Principal
│   ├── css/
│   │   └── estilos.css              # Hoja de estilos (Steam + 16-Bit Arcade, CRT effects)
│   ├── img/                         # Carátulas locales y avatares oficiales
│   ├── index.html                   # Portada (Carrusel dinámico de destacados, news ticker, métricas)
│   ├── catalogo.html                # Catálogo interactivo (Filtros, Grid/Tabla, modal, CRUD, códigos auto)
│   ├── carrito.html                 # Carro de compras (Cálculo de IVA, despacho RM $4.000, checkout)
│   ├── login.html                   # Autenticación y panel simétrico de cuentas oficiales demo
│   ├── registro.html                # Registro de clientes con ID correlativo y modal de términos
│   ├── nosotros.html                # Identidad, misión, visión y perfiles técnicos de los desarrolladores
│   ├── contacto.html                # Consultas con tickets correlativos PVT-000001 y FAQ despacho RM
│   ├── blog.html                    # Crónicas editoriales con carga de imágenes (URL/dispositivo 1200x675)
│   ├── usuarios.html                # Gestión de usuarios, métrica unificada de Staff y cambio de roles modal
│   ├── pedidos.html                 # Logística de pedidos (3 etapas de despacho, ruta repartidor y foto entrega)
│   └── historial.html               # Bitácora centralizada de auditoría de movimientos del sistema
│
├── tienda_videojuegos_estudio/      # Versión comentada pedagógicamente para estudio y preparación de defensa
├── bootstrap.md                     # Documentación de componentes y utilidades de Bootstrap 5.3.3
├── Planilla_Requerimientos.md       # Matriz oficial de requerimientos funcionales y no funcionales (R.1 a R.23)
├── Historias_de_Usuario.md          # Especificación ágil de Historias de Usuario (Épicas 1 a 9, HU-1 a HU-30)
├── ERS_Especificacion_Requisitos.md # Documento de Especificación de Requisitos de Software (IEEE 830)
└── README.md                        # Guía general de inicio y documentación del proyecto
```

---

## 🔑 Credenciales Oficiales de Demostración y Evaluación

La pantalla de inicio de sesión (`login.html`) incorpora un **Panel de Demostración y Evaluación Rápida** con tarjetas simétricas clickeables que autorrellenan instantáneamente el usuario y la contraseña:

| Usuario | Contraseña | Rol / Perfil | Alcance y Responsabilidades en el Sistema |
| :--- | :--- | :--- | :--- |
| **Jim** | `admin` | Administrador | Control total del sistema, catálogo, inventario, usuarios, métricas y auditoría. |
| **Emanuel** | `admin` | Administrador | Supervisión logística, control de stock físico y configuración general. |
| **Maximiliano** | `admin` | Administrador | Gestión editorial de crónicas, curaduría de títulos destacados y auditoría. |
| **fernando** | `operador` | Operador | Gestión de productos en catálogo y preparación de pedidos en almacén/bodega. |
| **adriana** | `editor` | Editor | Redacción, edición y publicación de crónicas y noticias en el Blog. |
| **ilie** | `repartidor` | Repartidor | Visualización exclusiva de despachos asignados, inicio de ruta y carga de foto de entrega. |
| **francisco** | `cliente` | Cliente / Usuario | Exploración de catálogo, carrito, seguimiento de compras en "Mis Compras" y contacto. |

---

## ✨ Características Técnicas y Funcionales Destacadas

1. **Logística de Despacho en Tres Etapas:**
   - `En preparación`: Comanda recepcionada en bodega. Alerta reactiva en barra de navegación para administradores y operadores.
   - `Asignado a repartidor`: Conductor asignado desde la bodega. Notificación reactiva inmediata al repartidor responsable.
   - `En camino`: El repartidor (o el administrador en caso de contingencia) activa `Iniciar Ruta`.
   - `Entregada`: El conductor carga obligatoriamente una foto real del paquete entregado en el domicilio como comprobante digital de recepción.
2. **Despacho Fijo en Región Metropolitana ($4.000 CLP):**
   - Selección dinámica en carrito: "Retiro en Tienda Física" ($0 - Gratis) o "Despacho a Domicilio (Solo Región Metropolitana - $4.000)", recalculando subtotales, IVA y total de orden al instante.
3. **Generación Automática de Códigos de Inventario por Consola:**
   - En el formulario de nuevo videojuego, elegir la plataforma (`PlayStation 5`, `Nintendo Switch`, `Xbox Series X`, `PC`) calcula correlativamente el siguiente código ascendente sin colisiones (ej. `PS5-015`, `NSW-014`).
4. **Tickets Correlativos de Soporte (`PVT-000001`):**
   - El formulario de contacto emite comprobantes de atención correlativos correlacionados en `localStorage`.
5. **IDs Secuenciales de Usuario y Panel de Staff Unificado:**
   - Identificadores correlativos enteros continuos desde 1 en adelante y métrica superior en `usuarios.html` que totaliza todo el personal operativo (Administradores, Operadores, Editores y Repartidores).
6. **Selector de Rol Modal con Auditoría Limpia:**
   - Cambio de roles mediante menú `<select>` en ventana modal Bootstrap, garantizando exactamente un registro en la bitácora tras la confirmación.
7. **Gestión Editorial de Crónicas con Carga Híbrida de Medios:**
   - Permite vincular imágenes vía URL externa o subir directamente archivos desde el dispositivo móvil/PC con vista previa y recomendación de resolución óptima (`1200 x 675 px (16:9)`).
8. **Atmósfera Gamer Retro (Efectos CRT y Scanlines):**
   - Micro-animaciones CSS3 inmersivas con barrido de haz de tubo de rayos catódicos al transicionar entre páginas.

---

## 🚀 Cómo Ejecutar el Proyecto Localmente

1. Accede a la carpeta raíz del frontend:
   ```bash
   cd Fullstack/tienda_videojuegos
   ```
2. Inicia un servidor HTTP local estático:
   ```bash
   # Opción con Python:
   python -m http.server 8080
   
   # Opción con Node.js / npx:
   npx serve .
   ```
3. Abre tu navegador web en: `http://localhost:8080`
