# PixelVault - Tienda de Videojuegos Físicos (16-Bit Arcade & Steam Style)

**Evaluación Parcial 1 - Desarrollo Fullstack (DSY1104)**  
**Institución:** Escuela de Informática y Telecomunicaciones  
**Equipo de Desarrollo Frontend:**
- Jim Charles
- Emanuel Reyes
- Maximiliano Peral

---

## 🎮 Descripción del Proyecto
**PixelVault** es una plataforma web para la comercialización y administración de videojuegos en formato físico. Su diseño combina la inmersión del tema oscuro de **Steam** con acentos visuales vibrantes de la época **16-bit arcade**.

El frontend está desarrollado con **Bootstrap v5.3.3** (CSS y componentes JS) y JavaScript nativo integrado en cada vista, siguiendo los lineamientos pedagógicos y la estructura limpia del estándar del curso (`proyecto_front`), sin dependencias complejas de compilación ni backend.

---

## 📁 Estructura del Repositorio

```text
Fullstack/
├── tienda_videojuegos/              # Frontend de la aplicación
│   ├── css/
│   │   └── estilos.css              # Hoja de estilos con diseño Steam + 16-Bit
│   ├── index.html                   # Página principal (destacados, ofertas, métricas admin)
│   ├── catalogo.html                # Catálogo interactivo (filtros, cuadrícula/tabla, modal, gestión admin)
│   ├── carrito.html                 # Carrito de compras y emisión de comprobante de compra
│   ├── nosotros.html                # Presentación del equipo desarrollador frontend
│   └── login.html                   # Autenticación con perfiles Administrador y Cliente
│
├── bootstrap.md                     # Documentación de componentes y utilidades de Bootstrap 5.3.3
├── Planilla_Requerimientos.md       # Matriz y planilla formal de requisitos funcionales y no funcionales
└── ERS_Especificacion_Requisitos.md # Documento de Especificación de Requisitos de Software (IEEE 830)
```

---

## 🔑 Credenciales de Acceso para Evaluación

El sistema cuenta con persistencia reactiva en `localStorage` y las siguientes cuentas de prueba:

| Usuario | Contraseña | Perfil / Rol | Permisos |
| :--- | :--- | :--- | :--- |
| **Jim** | `admin` | Administrador | Gestión de catálogo, métricas de inventario, edición y ajuste de stock. |
| **Emanuel** | `admin` | Administrador | Gestión de catálogo, métricas de inventario, edición y ajuste de stock. |
| **Maximiliano** | `admin` | Administrador | Gestión de catálogo, métricas de inventario, edición y ajuste de stock. |
| **geek** | `user` | Cliente | Exploración de catálogo, visualización de fichas y simulación de compra en carrito. |

---

## 🚀 Cómo Ejecutar el Proyecto Localmente

1. Clona este repositorio:
   ```bash
   git clone https://github.com/tecnofoxsolutions-crypto/PixelVault-Frontend.git
   ```
2. Accede a la carpeta del sitio web:
   ```bash
   cd Fullstack/tienda_videojuegos
   ```
3. Abre `index.html` directamente en tu navegador web favorito o levanta un servidor estático:
   ```bash
   # Opción con Python:
   python -m http.server 8080
   
   # Opción con Live Server (VS Code / Antigravity IDE)
   ```
