# Documento de Especificación de Requisitos de Software (ERS)
**Estándar IEEE 830 (Adaptación Anexo 4 - DSY1104)**  
**Proyecto:** PixelVault - Tienda de Videojuegos Físicos (Estilo Steam + 16-Bit Arcade)  
**Versión:** 2.0 (Entrega Parcial 1 Ampliada - Frontend Completo)  
**Institución:** Escuela de Informática y Telecomunicaciones - DUOC UC  
**Equipo de Desarrollo Frontend:** Jim Charles, Emanuel Reyes y Maximiliano Peral  
**Fecha:** Septiembre 2026  

---

## Ficha del Documento

| Fecha | Revisión | Autor / Rol | Modificación |
| :--- | :--- | :--- | :--- |
| 15/09/2026 | 1.0 | Jim Charles, Emanuel Reyes, Maximiliano Peral | Versión inicial del documento base según Anexo 4 DSY1104. |
| 18/09/2026 | 1.5 | Jim Charles, Emanuel Reyes, Maximiliano Peral | Integración de roles Operador, Repartidor y Editor, módulo de crónicas y trazabilidad de pedidos. |
| 21/09/2026 | 2.0 | Jim Charles, Emanuel Reyes, Maximiliano Peral | Actualización completa: Tarifa de despacho RM a $4.000, autogeneración de códigos por consola, tickets PVT-000001, logística en 3 etapas, panel de Staff unificado, badges reactivos y perfiles técnicos de desarrollo. |

---

## 1. Introducción

### 1.1. Propósito
El propósito del presente documento es definir de forma exhaustiva y formal los requisitos funcionales y no funcionales de **PixelVault**, plataforma web de comercio electrónico y gestión integral para la venta, catalogación, distribución logística y administración de videojuegos en formato físico. Su diseño combina la inmersión del tema oscuro de **Steam** con acentos visuales vibrantes de la época **16-bit arcade**.

### 1.2. Ámbito del Sistema
- **Nombre del Sistema:** PixelVault.
- **Alcance Funcional:** 
  1. Comercialización y catalogación de videojuegos físicos sellados para consolas (PS5, Nintendo Switch, Xbox Series X) y PC.
  2. Búsqueda y filtrado reactivo en tiempo real con vistas duales de cuadrícula y tabla.
  3. Ficha técnica interactiva en modal con control estricto de unidades en bodega.
  4. Carro de compras con validación de inventario, registro obligatorio de cliente, cálculo de IVA y tarifa fija de despacho a la Región Metropolitana ($4.000 CLP).
  5. Logística de pedidos en tres etapas: `En preparación` (bodega) &rarr; `Asignado a repartidor` (vehículo designado) &rarr; `En camino` (ruta activa iniciada por el repartidor) &rarr; `Entregada` (con foto de recepción obligatoria).
  6. Generación correlativa automática de códigos de inventario por consola (`PS5-015`, `NSW-014`, etc.).
  7. Gestión de usuarios con identificadores correlativos enteros, métrica de Staff global y cambio de roles mediante modal con menú desplegable `<select>`.
  8. Gestión editorial de crónicas y noticias en el Blog con carga híbrida de carátulas (URL externa o archivo local desde el dispositivo con recomendación de 1200x675 px).
  9. Soporte al cliente con tickets correlativos (`PVT-000001`) y preguntas frecuentes delimitadas a la RM.
  10. Bitácora centralizada de auditoría reactiva de movimientos del sistema.
- **Restricción de Arquitectura:** El sistema opera con 100% de autonomía en el navegador cliente mediante la Web Storage API (`localStorage` y `sessionStorage`), sin dependencias de backend ni compiladores externos.

### 1.3. Definiciones y Acrónimos
- **ERS:** Especificación de Requisitos de Software (IEEE 830).
- **CRUD:** Create, Read, Update, Delete (Crear, Leer, Actualizar, Eliminar).
- **RBAC:** Role-Based Access Control (Control de Acceso Basado en Roles).
- **DOM:** Document Object Model.
- **LocalStorage:** Almacenamiento web persistente en el navegador cliente.
- **SessionStorage:** Almacenamiento web temporal para control de sesión activa.
- **CLP:** Peso Chileno (moneda oficial del sistema).
- **RM:** Región Metropolitana de Santiago de Chile (área geográfica exclusiva de despacho a domicilio en la versión actual).

---

## 2. Descripción General

### 2.1. Perspectiva del Producto
PixelVault está estructurado en 11 vistas HTML vinculadas por una barra de navegación común y una hoja de estilos centralizada (`css/estilos.css`), incorporando **Bootstrap 5.3.3** en modo oscuro nativo (`data-bs-theme="dark"`).

```text
Estructura de Vistas:
1.  index.html       - Portada principal (Carrusel de destacados, banner, ticker de noticias, métricas).
2.  catalogo.html    - Catálogo interactivo (Filtros, Grid/Tabla, modal de detalle, CRUD admin y códigos automáticos).
3.  carrito.html     - Carro de compras (Validación de stock, selección de entrega, despacho RM $4.000, comanda).
4.  login.html       - Inicio de sesión con panel simétrico de cuentas oficiales de demostración.
5.  registro.html    - Registro de clientes con ID correlativo entero y modal interactivo de términos.
6.  nosotros.html    - Presentación institucional, misión, visión y perfiles técnicos de los desarrolladores.
7.  contacto.html    - Formulario de consultas con tickets correlativos PVT-000001 y FAQ de despacho RM.
8.  blog.html        - Crónicas y noticias gamer con editor de carga de imágenes (URL/archivo 1200x675).
9.  usuarios.html    - Gestión de usuarios, métrica unificada de Staff y cambio de roles modal.
10. pedidos.html     - Módulo de logística de pedidos (3 etapas, panel repartidor, foto de entrega y Mis Compras).
11. historial.html   - Bitácora completa de auditoría de movimientos del sistema.
```

### 2.2. Roles y Actores del Sistema

| Rol | Cuentas Oficiales de Evaluación | Atribuciones y Permisos |
| :--- | :--- | :--- |
| **Administrador** | `Jim` (admin)<br>`Emanuel` (admin)<br>`Maximiliano` (admin) | Control total del sistema: catálogo, inventario, métricas, gestión de roles de usuario, forzado logístico, gestión editorial y bitácora de auditoría. |
| **Operador** | `fernando` (operador) | Gestión de productos en catálogo, actualización de stock en bodega y preparación de pedidos para despacho o retiro. |
| **Editor** | `adriana` (editor) | Redacción, edición, borrado y publicación de crónicas y noticias en el Blog de preservación. |
| **Repartidor** | `ilie` (repartidor) | Visualización exclusiva de pedidos asignados, activación de ruta (`Iniciar Ruta`) y carga obligatoria de fotografía como comprobante de entrega. |
| **Cliente** | `francisco` (cliente) | Navegación comercial, carrito de compras, seguimiento en "Mis Compras", tickets de contacto y consultas. |
| **Visitante Anónimo** | Sin cuenta | Exploración libre del catálogo, lectura de blog, página de nosotros y registro de cuenta nueva. |

---

## 3. Requisitos Específicos

### 3.1. Requisitos Funcionales (RF)

#### RF-01: Semilla Inicial de 15 Videojuegos Físicos
El sistema inicializa automáticamente en `localStorage` (`pixelvault_productos_v3`) una semilla de 15 videojuegos físicos con carátula, plataforma, género, precio en CLP, stock, stock crítico y sinopsis.

#### RF-02: Autenticación RBAC y Cuentas de Evaluación Rápida
Valida credenciales en `sessionStorage` con expiración de 30 minutos y bloqueo de 60 segundos tras 5 intentos fallidos consecutivos. `login.html` provee tarjetas simétricas clickeables para autorrelleno instantáneo de credenciales demo.

#### RF-03: Catálogo Interactivo y Vistas Alternables (Grid / Tabla)
Permite buscar por texto libre, filtrar por plataforma y género simultáneamente. Los clientes ven tarjetas limpias sin datos de bodega; administradores y operadores ven controles de stock, estado y edición.

#### RF-04: Autogeneración Correlativa de Código Individual por Consola
Al crear un nuevo videojuego en `catalogo.html`, la selección de consola autocalcula el siguiente código correlativo disponible con su propia serie numérica independiente de 4 dígitos (`PlayStation 5` &rarr; `PS5-0001`, `PS5-0002`...; `PC` &rarr; `PC-0001`, `PC-0002`...; `Nintendo Switch` &rarr; `NSW-0001`...; `Xbox Series X` &rarr; `XSX-0001`...). Cada plataforma gestiona su propio contador correlativo ascendente a partir de sus existencias.

#### RF-05: Carrito con Control Estricto de Inventario
El cliente no puede solicitar más unidades físicas de las disponibles en bodega. La cantidad máxima en los selectores se ajusta dinámicamente al stock real de `localStorage`.

#### RF-06: Checkout con Tarifa Fija de Despacho en Región Metropolitana ($4.000 CLP)
El cliente debe estar autenticado obligatoriamente para finalizar la compra. La selección de "Despacho a Domicilio (Solo Región Metropolitana)" suma $4.000 CLP al total, mientras que "Retiro en Tienda Física" se mantiene en $0 (Gratis). Se descuenta el stock en bodega y se emite comanda con código correlativo `PV-000001` ascendente.

#### RF-07: Logística de Despacho en Tres Fases y Comprobante Fotográfico
1. Bodega recepciona comanda en estado `En preparación`.
2. Operador/Admin asigna repartidor y la orden avanza a `Asignado a repartidor`.
3. Repartidor responsable visualiza el pedido y pulsa `Iniciar Ruta`, pasando a `En camino`.
4. Repartidor entrega en domicilio y carga obligatoriamente una foto real del paquete para pasar el pedido a `Entregada`.

#### RF-08: Notificaciones Numéricas Reactivas en Barra de Navegación
Insignia circular dinámica con pulso arcade sobre el enlace `📦 Pedidos` que alerta a operadores/admins de pedidos en preparación y a repartidores de despachos pendientes de inicio de ruta.

#### RF-09: Gestión de Roles Modal con Auditoría Limpia
En `usuarios.html`, el administrador modifica roles mediante una ventana modal con menú desplegable `<select>`, generando exactamente un registro en la bitácora de auditoría tras su confirmación.

#### RF-10: Soporte con Tickets Correlativos (`PVT-000001`) y Cobertura RM
El formulario en `contacto.html` emite tickets secuenciales continuos y la sección FAQ especifica que la cobertura de despacho físico aplica exclusivamente a la Región Metropolitana.

#### RF-11: Gestión Editorial de Crónicas con Carga Híbrida de Medios
Módulo de blog con mantenedor para roles Admin y Editor, permitiendo asociar imágenes vía URL externa o mediante carga de archivos desde el dispositivo cliente (convertidos a Base64 vía `FileReader`), recomendando resolución óptima de 1200x675 px (16:9).

#### RF-12: Bitácora Centralizada de Auditoría
Registro inmutable en `historial.html` que documenta fecha, autor, categoría, acción y detalle de cada movimiento en productos, compras, usuarios, crónicas y despachos.

---

### 3.2. Requisitos No Funcionales (RNF)

- **RNF-01 (Estética y Experiencia Retro):** Interfaz inmersiva Steam + 16-Bit Arcade con fuentes pixeladas, acentos cian/dorados y micro-animaciones CRT (scanlines y haz de tubo catódico) al transicionar entre vistas.
- **RNF-02 (Rendimiento):** Búsqueda reactiva, recálculo de carrito y filtrado de pedidos en menos de 50 milisegundos en el cliente.
- **RNF-03 (Seguridad del DOM y Prevención XSS):** Manipulación de contenido dinámico mediante `textContent` y creación segura de nodos con `document.createElement`.
- **RNF-04 (Autonomía y Persistencia):** Funcionamiento 100% autónomo y desacoplado mediante la Web Storage API.
- **RNF-05 (Responsividad Bootstrap):** Maquetación fluida y adaptable en resoluciones desde 320px hasta monitores ultra-wide 4K.
