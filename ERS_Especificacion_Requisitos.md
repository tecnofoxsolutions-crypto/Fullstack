# Documento de Especificación de Requisitos de Software (ERS)
**Estándar IEEE 830 (Adaptación Anexo 4 - DSY1104)**  
**Proyecto:** PixelVault - Tienda de Videojuegos Físicos (Estilo Steam + 16-Bit Arcade)  
**Versión:** 1.1 (Entrega Parcial 1 - Frontend)  
**Institución:** Escuela de Administración y Negocios - Informática  
**Equipo de Desarrollo Frontend:** Jim Charles, Emanuel Reyes y Maximiliano Peral  
**Fecha:** Septiembre 2026  

---

## Ficha del Documento

| Fecha | Revisión | Autor / Rol | Modificación |
| :--- | :--- | :--- | :--- |
| 15/09/2026 | 1.1 | Jim Charles, Emanuel Reyes, Maximiliano Peral | Ajuste de arquitectura a 5 vistas HTML sin JS externo (estándar `proyecto_front`), cuentas oficiales de evaluación y restricciones de visualización para clientes. |

---

## 1. Introducción

### 1.1. Propósito
El propósito del presente documento es definir de forma formal los requisitos funcionales y no funcionales de **PixelVault**, una plataforma web de comercio electrónico orientada a la venta y administración de videojuegos en formato físico con estética inspirada en Steam y toques retro 16-bit arcade. Este documento está dirigido al equipo de desarrollo y a los docentes evaluadores de la asignatura DSY1104.

### 1.2. Ámbito del Sistema
- **Nombre del Sistema:** PixelVault.
- **Lo que el sistema hace:** Permite a los clientes explorar un catálogo de 15 videojuegos físicos para diversas plataformas (PC, PS5, Xbox Series X, Nintendo Switch), filtrar títulos en tiempo real, examinar la ficha técnica de cada juego en un modal interactivo con enfoque comercial limpio, gestionar un carrito de compras con control estricto de unidades en bodega, simular la compra descontando stock en almacenamiento local y permitir a los administradores gestionar el catálogo (CRUD), ajustar stock desde el modal y visualizar métricas globales en la página principal.
- **Lo que el sistema NO hace en esta etapa:** No se conecta a un backend remoto ni bases de datos SQL externas. Toda la persistencia opera de forma autónoma en el cliente mediante la Web Storage API (`localStorage` y `sessionStorage`). No requiere formularios de registro público de momento, operando con las cuentas oficiales designadas para la evaluación.

### 1.3. Definiciones, Acrónimos y Abreviaturas
- **ERS:** Especificación de Requisitos de Software (IEEE 830).
- **CRUD:** Create, Read, Update, Delete (Crear, Leer, Actualizar y Eliminar).
- **DOM:** Document Object Model.
- **LocalStorage:** Almacenamiento local persistente en el navegador web del cliente.
- **SessionStorage:** Almacenamiento web temporal asociado a la sesión activa.
- **Stock Crítico:** Cantidad mínima de copias en bodega que genera alerta preventiva para administradores.
- **CLP:** Peso Chileno (moneda oficial del sistema).

### 1.4. Referencias
- *DSY1104 Evaluación Parcial 1 - Anexo 1 Instrucciones.pdf*.
- *DSY1104 Evaluación Parcial 1 - Anexos 2, 3 y 4*.
- Repositorio base de clase: `proyecto_front`.
- Documentación oficial de Bootstrap v5.3.3: [https://getbootstrap.com/](https://getbootstrap.com/).

---

## 2. Descripción General

### 2.1. Perspectiva del Producto
PixelVault es una aplicación web frontend pura y autónoma estructurada en 5 vistas HTML con estilos CSS centralizados y lógica JavaScript integrada en cada página, respetando estrictamente el patrón modular de `proyecto_front`.

### 2.2. Funciones del Producto
1. **Módulo Público y Clientes:**
   - Inicio con banner gamer, accesos directos y títulos destacados.
   - Catálogo con 15 videojuegos físicos con filtros en tiempo real por texto, plataforma y género.
   - Ficha técnica en modal interactivo (sin códigos internos de bodega ni etiquetas numéricas de stock para clientes).
   - Carrito de compras con validación lógica de cantidades (prohíbe solicitar más unidades de las existentes).
   - Proceso simulado de checkout con cálculo de IVA y comprobante/comanda de orden confirmada.
   - Vista institucional "Nosotros" con reseña del equipo desarrollador.
2. **Módulo de Gestión (Administradores):**
   - Autenticación con cuentas oficiales (`Jim`, `Emanuel`, `Maximiliano` / clave `admin`) y cuenta cliente (`geek` / clave `user`).
   - Bloqueo de 60 segundos ante 5 intentos fallidos consecutivos en el login.
   - Panel de métricas globales en la página de inicio exclusivo para administradores.
   - Mantenedor (CRUD) de videojuegos y control de estados (Activo, Pausado, Agotado, Stock Crítico).
   - Ajuste rápido de inventario directamente dentro del modal de producto.

### 2.3. Características de los Usuarios

| Perfil de Usuario | Cuentas Preconfiguradas | Permisos en el Sistema |
| :--- | :--- | :--- |
| **Administrador** | `Jim / admin`<br>`Emanuel / admin`<br>`Maximiliano / admin` | Acceso total: creación de videojuegos, edición, ajuste de stock en modal, eliminación y visualización de métricas de bodega en la página de inicio. |
| **Cliente** | `geek / user` | Navegación comercial, consulta de catálogo con tarjetas limpias, visualización de modal y compra en carrito con control estricto de stock. |
| **Visitante Anónimo** | Sin cuenta | Exploración de la tienda, catálogo y página de nosotros. |

### 2.4. Restricciones
- Uso exclusivo de HTML5, CSS3 y JavaScript Vanilla con **Bootstrap v5.3.3** vía CDN oficial.
- Persistencia local en el cliente mediante `localStorage` y `sessionStorage`.
- Estructura libre de archivos JS externos independientes, manteniendo el código integrado en cada vista HTML como en `proyecto_front`.

---

## 3. Requisitos Específicos

### 3.1. Requisitos Comunes de las Interfaces
- **Estética:** Tema oscuro (*Dark Gaming*) inspirado en Steam combinado con estética 16-bit arcade (fuentes pixeladas `Silkscreen`, acentos neón y sombras retro), implementado nativamente mediante `data-bs-theme="dark"` de Bootstrap 5.3.3.
- **Responsividad:** Adaptable a dispositivos móviles, tablets y monitores de escritorio mediante el sistema de grillas (`container`, `row`, `col-12 col-md-6 col-lg-4 col-xl-3`).

### 3.2. Requisitos Funcionales Detallados

#### 3.2.1. RF-01: Semilla Inicial de 15 Videojuegos Físicos
- **Actores:** Sistema.
- **Descripción:** Carga automática de un catálogo inicial de exactamente 15 videojuegos físicos en `localStorage` con atributos completos: `id`, `codigo`, `nombre`, `categoria`, `plataforma`, `precio`, `stock`, `stockCritico`, `descripcion`, `imagen` y `activo`.

#### 3.2.2. RF-02: Autenticación con Cuentas Oficiales
- **Actores:** Todos los usuarios.
- **Descripción:** Inicio de sesión que valida credenciales contra las cuentas de evaluación (`Jim`, `Emanuel`, `Maximiliano` y `geek`). Bloqueo de 60 segundos tras 5 intentos fallidos y persistencia de sesión por 30 minutos en `sessionStorage`.

#### 3.2.3. RF-03: Catálogo y Búsqueda Reactiva
- **Actores:** Todos los usuarios.
- **Descripción:** Visualización de videojuegos en tarjetas interactivas. Filtro reactivo simultáneo por texto, plataforma y género. Para clientes, la tarjeta no exhibe etiquetas de estado interno de inventario.

#### 3.2.4. RF-04: Ficha Técnica en Modal Interactivo
- **Actores:** Todos los usuarios.
- **Descripción:** Modal emergente con carátula ampliada, sinopsis, género, plataforma y precio. Para clientes omite códigos internos de bodega y etiquetas numéricas de stock, mostrando selector de unidades y botón de compra. Para administradores incluye controles de ajuste de inventario y edición.

#### 3.2.5. RF-05: Control Estricto de Stock en Carrito
- **Actores:** Cliente.
- **Descripción:** El cliente puede agregar videojuegos al carrito. El sistema valida que la suma de unidades no supere el stock disponible en bodega. Si el stock es 0, el botón queda inhabilitado.

#### 3.2.6. RF-06: Simulación de Compra y Descuento de Stock
- **Actores:** Cliente.
- **Descripción:** En la vista de carrito, el cliente revisa el desglose con subtotal neto, 19% de IVA y total a pagar. Al presionar "Finalizar Compra", se descuentan las unidades compradas del inventario en `localStorage`, se vacía el carrito y se despliega la comanda/orden confirmada en un modal.

#### 3.2.7. RF-07: Mantenedor Administrativo (CRUD) de Videojuegos
- **Actores:** Administrador.
- **Descripción:** Panel protegido que permite dar de alta nuevos títulos físicos, modificar atributos existentes y eliminar títulos con confirmación explícita.

#### 3.2.8. RF-08: Gestión de Inventario Directamente desde el Modal
- **Actores:** Administrador.
- **Descripción:** El administrador puede modificar el número de unidades en stock de un juego directamente desde la ventana modal de detalles.

#### 3.2.9. RF-09: Panel de Métricas de Inventario en Home
- **Actores:** Administrador.
- **Descripción:** En la página de inicio (`index.html`), se despliega un panel cuantitativo con el total de títulos físicos, copias disponibles y plataformas activas. Esta sección es visible únicamente para administradores.

#### 3.2.10. RF-10: Sección Nosotros y Equipo Desarrollador
- **Actores:** Todos los usuarios.
- **Descripción:** Vista institucional con la historia de PixelVault y la presentación oficial de los 3 desarrolladores Frontend: Jim Charles, Emanuel Reyes y Maximiliano Peral.

---

### 3.3. Requisitos No Funcionales
- **Rendimiento:** Operaciones de filtrado y cálculo de carrito en menos de **50 milisegundos**.
- **Seguridad en el DOM:** Manipulación de datos dinámicos mediante `textContent` y creación segura de nodos con `document.createElement`, previniendo inyecciones de código XSS.
- **Fiabilidad:** Sincronización continua de inventario y compras mediante la Web Storage API.
- **Mantenibilidad:** Código estructurado en 5 vistas HTML limpias sin dependencias externas complejas, siguiendo fielmente la pauta de `proyecto_front`.
