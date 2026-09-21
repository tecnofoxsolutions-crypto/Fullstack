# Documentación de Componentes y Utilidades de Bootstrap 5.3.3
**Proyecto:** PixelVault - Tienda de Videojuegos Físicos (Estilo Steam + 16-Bit Arcade)  
**Fuente Oficial:** [https://getbootstrap.com/](https://getbootstrap.com/)  
**Versión Utilizada:** Bootstrap v5.3.3 (CSS & JS Bundle vía CDN oficial de jsDelivr)  
**Semilla de Catálogo:** 15 Videojuegos Físicos Emblemáticos (Modernos & Clásicos Arcade)  
**Estructura:** 11 archivos HTML (`index.html`, `catalogo.html`, `carrito.html`, `login.html`, `registro.html`, `nosotros.html`, `contacto.html`, `blog.html`, `usuarios.html`, `pedidos.html`, `historial.html`) + 1 CSS (`css/estilos.css`), con scripts integrados en cada vista (siguiendo el estándar de `proyecto_front`).  
**Equipo de Desarrollo Frontend:** Jim Charles, Emanuel Reyes y Maximiliano Peral.  

Este documento detalla cada uno de los componentes, clases utilitarias y elementos visuales de **Bootstrap 5** implementados en la construcción del frontend de PixelVault, explicando su función técnica, configuración y rol en la experiencia de usuario.

---

## 1. Integración de Bootstrap en el Proyecto

Todas las vistas incorporan Bootstrap 5.3.3 mediante sus enlaces CDN oficiales y habilitan el modo oscuro nativo (`data-bs-theme="dark"`), logrando la estética inmersiva de **Steam** combinada con acentos retro **16-bit arcade**:

```html
<!-- En el <head> -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<link rel="stylesheet" href="css/estilos.css">

<!-- En la etiqueta <html> para activar el tema oscuro estilo Steam -->
<html lang="es" data-bs-theme="dark">

<!-- Antes del cierre de </body> para componentes interactivos (Modals, Carousels, Collapse) -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

---

## 2. Catálogo de Componentes Oficiales Implementados

### 2.1. Barra de Navegación (`Navbar`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/navbar/](https://getbootstrap.com/docs/5.3/components/navbar/)
- **Ubicación en el proyecto:** Cabecera de todas las 11 páginas del sitio.
- **Clases clave utilizadas:**
  - `navbar`: Contenedor principal de la barra.
  - `navbar-expand-lg`: Colapsa en menú hamburguesa en pantallas móviles y se expande en escritorio.
  - `navbar-steam`: Estilización personalizada integrada con `bg-dark` y borde cian neón.
  - `navbar-brand font-arcade`: Logotipo y nombre comercial con tipografía pixelada.
  - `navbar-nav`: Lista de navegación con enlaces a Inicio, Catálogo, Blog, Nosotros, Contacto, Mis Compras, Pedidos, Usuarios e Historial.
  - `nav-link`: Enlaces interactivos con efecto hover.
  - `badge-notif-pedidos`: Insignia numérica reactiva con animación de pulso montada sobre el enlace `📦 Pedidos`.
- **Función en el proyecto:** Centraliza el acceso a todos los módulos según el rol autenticado y exhibe alertas numéricas de pedidos pendientes.

---

### 2.2. Tarjetas (`Cards`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/card/](https://getbootstrap.com/docs/5.3/components/card/)
- **Ubicación en el proyecto:** Catálogo, destacados de portada, métricas cuantitativas, crónicas del blog, tarjetas de pedidos y panel de cuentas demo en login.
- **Clases clave utilizadas:**
  - `card card-juego`: Contenedor de tarjeta con bordes arcade y sombras oscuras.
  - `card-img-top card-juego-img`: Ajuste de carátula en alta definición con `object-fit: cover`.
  - `card-body`: Contenedor flexible para contenido interno.
  - `card-title` / `card-text`: Jerarquía tipográfica para títulos y sinopsis.
  - `h-100`: Asegura alturas simétricas y homogéneas en filas de cuadrícula.
  - `shadow-sm` / `shadow`: Profundidad visual integrada con la paleta Steam.

---

### 2.3. Carrusel Dinámico (`Carousel`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/carousel/](https://getbootstrap.com/docs/5.3/components/carousel/)
- **Ubicación en el proyecto:** Sección de videojuegos destacados en `index.html` (para clientes y visitantes).
- **Clases clave utilizadas:**
  - `carousel slide`: Contenedor interactivo del carrusel con transiciones fluidas.
  - `carousel-inner` / `carousel-item`: Diapositivas dinámicas agrupadas de a 3 o 4 tarjetas de juegos.
  - `carousel-control-prev` / `carousel-control-next`: Flechas de navegación lateral.
  - `carousel-indicators`: Botones inferiores indicadores de diapositiva.
- **Función en el proyecto:** Ofrece una vitrina moderna e interactiva de títulos recomendados, adaptándose automáticamente a vistas estáticas cuando navega un Administrador.

---

### 2.4. Ventanas Modales (`Modal`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/modal/](https://getbootstrap.com/docs/5.3/components/modal/)
- **Ubicación en el proyecto:**
  1. `modalDetalle` (`catalogo.html`): Ficha técnica del juego y control de compra/stock.
  2. `modalComprobante` (`carrito.html`): Comprobante formal de orden emitida y desglose de despacho.
  3. `modalRegistroObligatorio` (`carrito.html`): Requisito de cuenta para finalizar checkout.
  4. `modalCambiarRol` (`usuarios.html`): Menú desplegable para asignación limpia de rol.
  5. `modalTerminos` (`registro.html`): Lectura y aceptación interactiva de términos.
  6. `modalComprobanteEntrega` (`pedidos.html`): Carga de fotografía real para finalizar despacho.
  7. `modalEditorArticulo` (`blog.html`): Redacción y carga de portadas (URL/dispositivo).
- **Clases clave utilizadas:**
  - `modal fade`: Animación de apertura y cierre.
  - `modal-dialog modal-dialog-centered modal-lg`: Posicionamiento centrado y tamaño adaptativo.
  - `modal-content`: Contenedor del diálogo con tema oscuro.
  - `modal-header`, `modal-body`, `modal-footer`: Estructura semántica estandarizada.
  - `btn-close btn-close-white`: Botón de cierre accesible en tema oscuro.

---

### 2.5. Insignias y Etiquetas (`Badges`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/badge/](https://getbootstrap.com/docs/5.3/components/badge/)
- **Ubicación en el proyecto:** Plataformas de juegos, roles de usuario, estados de pedidos y notificaciones reactivas.
- **Clases clave utilizadas:**
  - `badge text-bg-primary`: Plataforma PlayStation 5 o rol Administrador.
  - `badge text-bg-info`: Plataformas PC o rol Repartidor / Modalidad Despacho.
  - `badge text-bg-warning`: Stock crítico, estado "En preparación" o rol Operador.
  - `badge text-bg-danger`: Stock agotado o estado "Cancelado".
  - `badge text-bg-success`: Disponibilidad en bodega o estado "Entregada".
  - `badge text-bg-secondary`: Géneros, estado inactivo o rol Editor.
  - `badge-notif-pedidos`: Insignia numérica circular con posición absoluta sobre enlaces del navbar.

---

### 2.6. Alertas y Mensajes de Estado (`Alerts`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/alerts/](https://getbootstrap.com/docs/5.3/components/alerts/)
- **Ubicación en el proyecto:** Mensajes globales de feedback, validaciones y confirmaciones en todas las vistas.
- **Clases clave utilizadas:**
  - `alert alert-success`: Confirmaciones de guardado, alta de producto o comanda emitida.
  - `alert alert-danger`: Errores de validación, claves incorrectas o falta de stock en bodega.
  - `alert alert-warning`: Avisos de stock crítico o sesión requerida.
  - `alert alert-info`: Orientación contextual de filtros o instrucciones de despacho.

---

### 2.7. Formularios, Selectores y Grupos de Entrada (`Forms & Input Groups`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/forms/overview/](https://getbootstrap.com/docs/5.3/forms/overview/)
- **Ubicación en el proyecto:** Formularios de catálogo, registro, login, checkout, blog, contacto y usuarios.
- **Clases clave utilizadas:**
  - `form-control`: Campos de texto, números, contraseñas y áreas de texto con tema oscuro.
  - `form-select`: Menús desplegables para selector de consola, modalidad de entrega y cambio de rol.
  - `input-group`: Combinación de prefijos de ícono/texto con inputs de URL y archivos.
  - `form-check` / `form-check-input`: Casillas de verificación para términos, estado activo y destacado.
  - `form-label` / `form-text`: Etiquetas asociadas por `for` y textos de ayuda accesibles.

---

### 2.8. Tablas Responsivas (`Tables`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/content/tables/](https://getbootstrap.com/docs/5.3/content/tables/)
- **Ubicación en el proyecto:** Tablas en `catalogo.html`, `carrito.html`, `usuarios.html` e `historial.html`.
- **Clases clave utilizadas:**
  - `table table-dark`: Tabla integrada con la paleta oscura de la plataforma.
  - `table-hover`: Resaltado sutil de filas al interactuar con el puntero.
  - `table-responsive`: Envoltorio con barra de desplazamiento horizontal en pantallas móviles.
  - `align-middle`: Alineación vertical precisa de carátulas, datos numéricos y botones de acción.

---

### 2.9. Botones y Grupos de Botones (`Buttons & Button Groups`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/buttons/](https://getbootstrap.com/docs/5.3/components/buttons/)
- **Ubicación en el proyecto:** Presente en todas las interacciones del sitio.
- **Clases clave utilizadas:**
  - `btn btn-primary`: Acciones principales ("Finalizar Compra", "Guardar Videojuego", "Iniciar Sesión").
  - `btn btn-outline-info`: Acciones de consulta ("Ver Detalles", "Continuar Comprando", "Filtrar").
  - `btn btn-outline-warning`: Acciones de edición ("✏️ Editar", "Editar Rol").
  - `btn btn-outline-danger`: Acciones destructivas ("✕ Quitar", "Eliminar", "Vaciar Carrito").
  - `btn-group`: Alternador entre vista de cuadrícula y vista de tabla en catálogo.

---

### 2.10. Sistema de Grillas y Utilidades Flexbox (`Grid & Flexbox`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/layout/grid/](https://getbootstrap.com/docs/5.3/layout/grid/)
- **Ubicación en el proyecto:** Maquetación responsiva en las 11 vistas.
- **Clases clave utilizadas:**
  - `container`: Envoltorio centrado responsivo con márgenes automáticos.
  - `row`: Filas con arquitectura flexbox.
  - `col-12 col-md-6 col-lg-4 col-xl-3`: Grilla fluida de 4 columnas en escritorios grandes, 3 en pantallas medianas, 2 en tablets y 1 en móviles.
  - `g-2`, `g-3`, `g-4`: Separación armónica horizontal y vertical entre columnas.
  - `d-flex`, `justify-content-between`, `align-items-center`, `gap-2/3`: Alineación flexible y espaciado moderno sin CSS manual redundante.

---

## 3. Cuentas Oficiales Preconfiguradas para la Evaluación

| Usuario | Contraseña | Perfil / Rol | Persona Asociada | Alcance de Permisos en la Plataforma |
| :--- | :--- | :--- | :--- | :--- |
| `Jim` | `admin` | **Administrador** | Jim Charles | Acceso maestro: catálogo, usuarios, auditoría, crónicas y logística. |
| `Emanuel` | `admin` | **Administrador** | Emanuel Reyes | Acceso maestro: control de inventario, stock físico y configuración. |
| `Maximiliano` | `admin` | **Administrador** | Maximiliano Peral | Acceso maestro: gestión editorial, destacados y supervisión general. |
| `fernando` | `operador` | **Operador** | Fernando Sierra | Almacén y bodega: control de catálogo y empaque de pedidos. |
| `adriana` | `editor` | **Editor** | Adriana Quispe | Redacción, edición y publicación de crónicas y noticias en el Blog. |
| `ilie` | `repartidor` | **Repartidor** | Ilie Flores | Visualización de pedidos asignados, inicio de ruta y foto de entrega. |
| `francisco` | `cliente` | **Cliente** | Francisco Calabran | Navegación, compra con despacho RM, seguimiento en "Mis Compras" y contacto. |
