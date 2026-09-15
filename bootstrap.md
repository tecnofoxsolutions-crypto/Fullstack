# Documentación de Componentes y Utilidades de Bootstrap 5.3.3
**Proyecto:** PixelVault - Tienda de Videojuegos Físicos (Estilo Steam + 16-Bit Arcade)  
**Fuente Oficial:** [https://getbootstrap.com/](https://getbootstrap.com/)  
**Versión Utilizada:** Bootstrap v5.3.3 (CSS & JS Bundle vía CDN oficial de jsDelivr)  
**Semilla de Catálogo:** 15 Videojuegos Físicos Emblemáticos (Modernos & Clásicos Arcade)  
**Estructura:** 5 archivos HTML (`index.html`, `catalogo.html`, `carrito.html`, `login.html`, `nosotros.html`) + 1 CSS (`css/estilos.css`), con scripts integrados en cada vista (siguiendo el estándar de `proyecto_front`).  
**Equipo de Desarrollo Frontend:** Jim Charles, Emanuel Reyes y Maximiliano Peral.  

Este documento detalla cada uno de los componentes, clases utilitarias y elementos visuales de **Bootstrap 5** implementados en la construcción del frontend de la tienda de videojuegos físicos, explicando su función técnica, configuración y rol en la experiencia de usuario.

---

## 1. Integración de Bootstrap en el Proyecto

Todas las vistas incorporan Bootstrap 5.3.3 mediante sus enlaces CDN oficiales y habilitan el modo oscuro nativo (`data-bs-theme="dark"`), logrando la estética inmersiva de **Steam** combinada con acentos retro **16-bit arcade**:

```html
<!-- En el <head> -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<link rel="stylesheet" href="css/estilos.css">

<!-- En la etiqueta <html> para activar el tema oscuro estilo Steam -->
<html lang="es" data-bs-theme="dark">

<!-- Antes del cierre de </body> para componentes interactivos (Modals, Dropdowns) -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

---

## 2. Catálogo de Componentes Oficiales Implementados

### 2.1. Barra de Navegación (`Navbar`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/navbar/](https://getbootstrap.com/docs/5.3/components/navbar/)
- **Ubicación en el proyecto:** Cabecera de todas las páginas (`index.html`, `catalogo.html`, `carrito.html`, `nosotros.html`, `login.html`).
- **Clases clave utilizadas:**
  - `navbar`: Contenedor principal de la barra.
  - `navbar-expand-lg`: Permite que la barra se colapse en pantallas pequeñas (móviles) y se expanda en pantallas grandes.
  - `navbar-steam`: Clase personalizada integrada con `bg-dark` y borde neón cian.
  - `navbar-brand font-arcade`: Logotipo y nombre de la tienda ("PixelVault [16-BIT]") con tipografía arcade.
  - `navbar-nav`: Enlaces directos a las secciones del sitio (`Inicio`, `Catálogo`, `Nosotros`).
  - `nav-link`: Enlaces interactivos con efecto hover nativo.
- **Función en el proyecto:** Proporciona navegación unificada, acceso al carrito con contador dinámico en tiempo real y muestra el estado de sesión del usuario autenticado.

---

### 2.2. Tarjetas de Producto (`Cards`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/card/](https://getbootstrap.com/docs/5.3/components/card/)
- **Ubicación en el proyecto:** Catálogo de videojuegos físicos y títulos destacados de la página de inicio.
- **Clases clave utilizadas:**
  - `card card-juego`: Contenedor de tarjeta con bordes y sombras arcade 16-bit.
  - `card-img-top card-juego-img`: Aplica carátulas en alta resolución con ajuste `object-fit: cover`.
  - `card-body`: Área interna para título, género, plataforma y precio en pesos chilenos (CLP).
  - `card-title`: Tipografía para el nombre del juego.
  - `h-100`: Asegura que todas las tarjetas mantengan la misma altura en la grilla.
  - `shadow-sm`: Sombra suave combinada con sombra dura pixel-art.
- **Regla de visualización implementada:** Los usuarios clientes observan la tarjeta limpia con su plataforma, título, precio y botón de "Ver Detalles". Las insignias de estado interno ("Activo", "Pausado", "Stock Crítico") son exclusivas para el rol de Administrador.

---

### 2.3. Ventana Modal (`Modal`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/modal/](https://getbootstrap.com/docs/5.3/components/modal/)
- **Ubicación en el proyecto:** Ficha técnica en `catalogo.html` y comprobante de compra en `carrito.html`.
- **Clases clave utilizadas:**
  - `modal fade`: Contenedor del diálogo con animación de apertura suave.
  - `modal-dialog modal-lg modal-dialog-centered`: Modal de tamaño amplio y centrado verticalmente.
  - `modal-content`: Contenedor estilizado con fondo oscuro y bordes de alto contraste.
  - `modal-header`: Encabezado con título y botón de cierre (`btn-close`).
  - `modal-body`: Cuerpo principal con carátula ampliada, sinopsis, selector de compra para clientes y controles de ajuste rápido de stock para administradores.
  - `modal-footer`: Botón de cierre y acciones contextuales.
- **Regla de visualización implementada:** Para los clientes, el modal omite códigos internos de inventario y etiquetas numéricas de bodega, manteniendo una experiencia de compra limpia y directa con selector de unidades y botón de "Añadir al Carrito".

---

### 2.4. Formularios y Controles de Entrada (`Forms`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/forms/overview/](https://getbootstrap.com/docs/5.3/forms/overview/)
- **Ubicación en el proyecto:** Formulario de login en `login.html`, mantenedor de videojuegos en `catalogo.html` y filtros de búsqueda.
- **Clases clave utilizadas:**
  - `form-control`: Campos de texto, contraseñas y números con fondo oscuro (`bg-dark border-secondary`).
  - `form-select`: Selectores desplegables para filtrar por plataforma (PS5, Switch, Xbox Series X, PC) y categorías.
  - `form-label`: Etiquetas legibles asociadas a cada control.
  - `form-check-input`: Checkbox para estado de activación de títulos.
  - `input-group` e `input-group-text`: Agrupación visual con icono de lupa para el buscador rápido.

---

### 2.5. Insignias de Estado (`Badges`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/badge/](https://getbootstrap.com/docs/5.3/components/badge/)
- **Ubicación en el proyecto:** Plataformas, roles en navbar y paneles administrativos.
- **Clases clave utilizadas:**
  - `badge text-bg-primary`: Distintivo de plataforma (PlayStation 5, Nintendo Switch, etc.) y rol de Administrador.
  - `badge text-bg-success`: Estado Activo en panel admin y rol Cliente.
  - `badge text-bg-warning`: Alerta de Stock Crítico para administradores.
  - `badge text-bg-danger`: Indicador de producto Agotado o contador de carrito.
  - `badge text-bg-secondary`: Género del juego o productos inactivos.

---

### 2.6. Alertas Dinámicas (`Alerts`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/alerts/](https://getbootstrap.com/docs/5.3/components/alerts/)
- **Ubicación en el proyecto:** Mensajes de error en login, confirmaciones de adición al carrito, avisos de límite de stock y alertas de gestión.
- **Clases clave utilizadas:**
  - `alert alert-danger`: Errores de credenciales o campos obligatorios.
  - `alert alert-warning`: Avisos de stock insuficiente al superar las copias existentes.
  - `alert alert-success`: Confirmación de videojuego guardado o compra simulada con éxito.
  - `d-none`: Oculta las alertas hasta que la validación JavaScript las activa reactivamente.

---

### 2.7. Tablas de Inventario y Carrito (`Tables`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/content/tables/](https://getbootstrap.com/docs/5.3/content/tables/)
- **Ubicación en el proyecto:** Detalle de pedido en `carrito.html` y vista de tabla administrativa en `catalogo.html`.
- **Clases clave utilizadas:**
  - `table table-dark`: Tabla integrada con el tema oscuro de la plataforma.
  - `table-hover`: Resaltado de filas al interactuar con el cursor.
  - `table-responsive`: Contenedor con desplazamiento horizontal fluido en pantallas pequeñas.
  - `align-middle`: Alineación vertical de miniaturas, nombres, precios y botones.

---

### 2.8. Botones y Grupos de Botones (`Buttons`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/components/buttons/](https://getbootstrap.com/docs/5.3/components/buttons/)
- **Ubicación en el proyecto:** Presente en todas las interacciones del sitio.
- **Clases clave utilizadas:**
  - `btn btn-primary`: Acciones primarias ("Finalizar Compra", "Guardar", "Entrar").
  - `btn btn-outline-info`: Acciones de consulta y navegación ("Ver Detalles", "Continuar Comprando").
  - `btn btn-outline-danger`: Acciones destructivas ("Quitar", "Vaciar Carrito", "Eliminar").
  - `btn-group`: Alternador entre vista de cuadrícula y vista de tabla en catálogo.

---

### 2.9. Sistema de Grillas y Layout (`Grid System`)
- **Documentación oficial:** [https://getbootstrap.com/docs/5.3/layout/grid/](https://getbootstrap.com/docs/5.3/layout/grid/)
- **Ubicación en el proyecto:** Estructura responsiva en las 5 vistas del proyecto.
- **Clases clave utilizadas:**
  - `container`: Contenedor responsivo centrado con espaciado lateral automático.
  - `row`: Filas con disposición flexbox.
  - `col-12 col-md-6 col-lg-4 col-xl-3`: Disposición de 4 columnas en monitores grandes, 3 en pantallas medianas, 2 en tablets y 1 en teléfonos móviles.
  - `g-3` / `g-4`: Separación uniforme y proporcional entre columnas.

---

## 3. Cuentas Preconfiguradas para la Evaluación

| Usuario | Contraseña | Perfil / Rol | Persona Asociada | Permisos |
| :--- | :--- | :--- | :--- | :--- |
| `Jim` | `admin` | **Administrador** | Jim Charles | Acceso total: creación, edición, ajuste de stock y métricas. |
| `Emanuel` | `admin` | **Administrador** | Emanuel Reyes | Acceso total: creación, edición, ajuste de stock y métricas. |
| `Maximiliano` | `admin` | **Administrador** | Maximiliano Peral | Acceso total: creación, edición, ajuste de stock y métricas. |
| `geek` | `user` | **Cliente** | Geek Gamer | Consulta de catálogo, visualización de modal y compra en carrito. |
