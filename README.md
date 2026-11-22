# Calculadora para negocios

Calculadora web de costos, precios, margen y markup para comercios y emprendimientos productivos.
Es un único archivo `index.html` (HTML, CSS y JavaScript en línea), sin build, sin frameworks y sin dependencias externas.

**Privacidad:** todo el cálculo ocurre en el navegador. No se guarda ni se envía ningún dato.

## Qué calcula cada parte

### Inicio
Pantalla de bienvenida con los tres pasos de la calculadora y el botón **Empezar**, que lleva a la pestaña 1.

### Configuración general (visible en las tres pestañas de cálculo)
- **Tipo de contribuyente:** Monotributista o Responsable inscripto.
- **Monotributista:** la cuota mensual es un costo fijo y ya incluye el componente de Ingresos Brutos, por eso no se carga ni se suma al costo unitario: la calculadora arma solo el costo variable. Los precios son finales (no se discrimina IVA).
- **Responsable inscripto:** los costos se cargan sin IVA (crédito fiscal) y los precios se toman netos de IVA. La alícuota de IVA es editable (21% inicial): `precio con IVA = precio neto × (1 + IVA/100)`.
- **Ingresos Brutos (solo responsable inscripto):** alícuota editable (0% inicial): `IIBB por unidad = precio neto × alícuota / 100`.

### Pestaña 1: Sector Reventa - Comercio
Costeo por absorción de mercadería comprada para revender.
- Primero se carga la cantidad de unidades y luego se tilda (o no) la casilla **"¿El precio de factura es por unidad?"**.
- `Precio neto de factura = precio de factura − descuentos (%)`
- Gastos de compra: monto total del lote (flete, seguro, carga y descarga, empaque, etc.; filas libres).
- **Precio del lote (casilla sin tildar):** `costo unitario = (precio neto del lote + gastos de compra) ÷ cantidad`
- **Precio por unidad (casilla tildada):** `costo unitario = precio neto por unidad + gastos de compra ÷ cantidad`

### Pestaña 2: Sector Manufactura - Producción
Costeo por absorción de un lote producido.
- Materia prima: `cantidad × precio unitario ÷ (1 − merma/100)`, con merma menor que 100%.
- Mano de obra directa: `valor hora × horas` (más filas libres de otros costos de mano de obra).
- CIF: cada rubro se asigna con su propia **base de asignación** (unidades producidas, horas de mano de obra directa, horas máquina, kilos de materia prima u otra con nombre libre).
  - `Tasa del rubro = monto mensual ÷ base normal del mes`
  - `CIF del lote = tasa × base que consume el lote` (con "unidades producidas" se usa el rendimiento; con "horas de mano de obra directa", las horas cargadas en Mano de obra)
- `Costo unitario = (materia prima + mano de obra + CIF del lote) ÷ rendimiento`

### Pestaña 3: Margen y Markup
- El costo unitario se toma de la pestaña 1, de la pestaña 2 o se carga a mano (y siempre se puede editar).
- Dos formas de cargar el precio: **por multiplicador** (`precio = costo × multiplicador`) o **por precio de venta** (`multiplicador = precio ÷ costo`).
- `Markup = (precio − costo) ÷ costo × 100` (sobre el costo).
- `Margen = (precio − costo) ÷ precio × 100` (sobre el precio de venta).
- Utilidad por unidad y, para Responsable inscripto, IIBB por unidad, margen después de IIBB y precio final con IVA.
- **Estructura de precios:**
  - **Efectivo** = precio de venta.
  - **Tarjeta y Mercado Pago** = efectivo × (1 + ajuste %), normalmente un recargo.
  - **Descuento** y **Precio mayorista** = precio de Tarjeta y Mercado Pago × (1 + ajuste %), normalmente negativo.
- **Descargar PDF:** arma un informe con los valores actuales y abre el diálogo de impresión. Elegí "Guardar como PDF" como destino.

Los números aceptan coma o punto como separador decimal (`2,5` o `2.5`) y punto para miles en montos (`1.000.000`). El símbolo `$` es fijo y no se convierte moneda: ingresá los valores en la moneda que uses (USD o ARS).

## Cómo abrirla
- **En tu compu:** descargá el repositorio y abrí `index.html` con doble clic en cualquier navegador moderno. No necesita servidor ni conexión.
- **En línea:** publicala con GitHub Pages (ver abajo).

## Cómo activar GitHub Pages
1. Subí el contenido de `calculadora-para-negocios/` al repositorio (con `index.html` en la raíz o en una carpeta).
2. En GitHub, entrá a **Settings → Pages**.
3. En **Build and deployment → Source**, elegí **Deploy from a branch**.
4. Elegí la rama (por ejemplo `main`) y la carpeta: `/ (root)` si `index.html` está en la raíz, o `/docs` si lo ubicaste ahí.
5. Guardá. En uno o dos minutos la página queda publicada en `https://<usuario>.github.io/<repositorio>/`.

## Personalización
- **Nombre del estudio:** editá el atributo `data-estudio` en la etiqueta `<html>` de `index.html` (hoy: "Cr. Ignacio Dukardt"). Se usa en el encabezado, el pie y el informe PDF.

## Pendiente
- Impuesto a las ganancias: no está incluido en esta versión. El punto de extensión está marcado en el código (`PUNTO DE EXTENSIÓN`, dentro de `calcT3`).
- Alícuotas de Ingresos Brutos verificadas por jurisdicción: hoy las carga el usuario.

---
Estimación orientativa. No reemplaza el asesoramiento profesional.
