# Verificador de Traspasos

Página web para verificar los traspasos de **C99 Oficina** a las 4 tiendas New Balance (**A2 Multiplaza, A3 Albrook, A4 Dorado, A7 Metromall**). Compara, por **referencia y talla**:

1. **Surtido sugerido → Sistema**: ¿el traspaso que se pasó en sistema es igual al surtido que se trabajó en oficina?
2. **Sistema → Tienda**: ¿la tienda recibió físicamente lo que dice el traspaso del sistema?

Todo se procesa en el navegador; los archivos no se suben a ningún servidor.

## Cómo se usa

1. Carga el **surtido sugerido** (obligatorio). Primera hoja, encabezados en la fila 1 y la fila TOTAL en la 2:
   `Referencia | Talla | C99 stock | Albrook | Dorado | Metro Mall | Multiplaza | Total`
   - Se usan las columnas de cada tienda; *C99 stock* y *Total* no se usan.
2. Carga el Excel de **traspasos del sistema** (obligatorio, uno solo con las 4 tiendas). Encabezados en la fila 1:
   `Cód. Barras | Referencia | Talla | Color | Descripción | Cód. Almacén Origen | Cód. Almacén Destino | UDS. Env`
   - Si alguna línea tiene un origen distinto a **C99** o un destino distinto a **A2, A3, A4, A7**, la página marca error con el número de fila y no deja verificar.
3. Carga en la casilla de cada tienda su archivo de recibo (el **MAPPING RECIBO DE TRASPASOS**). Son opcionales: sin ellos se verifica solo surtido vs sistema, y el físico se agrega cuando llegue. Siempre tiene la hoja `mapping` con encabezados en la fila 1:
   `COD BARRA | Referencia | Talla | Cantidad | Color | DESCRIPCION` — una fila por cada par escaneado (Referencia, Talla, etc. salen de la hoja DATA).
   - Si alguna fila sale **NO COINCIDE** (el código escaneado no está en DATA), la página marca error con el número de fila y no deja verificar.
   - El cruce es por **Referencia + Talla** (los códigos de barras de la tienda son del fabricante y los del sistema son internos, no coinciden).
   - Tallas unisex: si la tienda trae un solo número (ej. `5`) y la oficina tiene esa referencia con talla doble (ej. `H5|M6.5`), el número se toma como la talla de **hombre**.
4. Clic en **Verificar traspasos**. Hay una pestaña de **Resumen** con todas las tiendas y una pestaña por tienda con el detalle: Surtido | Sistema | Físico, con las diferencias *Sistema − Surtido* y *Físico − Sistema*.
5. **Descargar reporte Excel**: hoja *Resumen* + por cada tienda una hoja por referencia y una hoja por talla. También se puede imprimir / guardar como PDF la pestaña abierta.

### Estados por talla

| Estado | Significado |
|---|---|
| OK | Surtido = Sistema (= Físico, si se cargó la tienda) |
| No pasado en sistema | Estaba en el surtido y no está en el traspaso del sistema |
| En sistema sin surtido | Está en el sistema y no estaba en el surtido |
| Sistema con menos / con más | El sistema tiene una cantidad distinta al surtido |
| No recibido en tienda | Estaba en el sistema y no llegó nada |
| Recibido sin traspaso | Llegó algo que no estaba en el sistema |
| Faltante / Sobrante en tienda | Llegó menos / más de lo que dice el sistema |

Una referencia está **OK** solo si todas sus tallas están OK.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub (ej. `verificador-traspasos`).
2. Sube `index.html` y `README.md` a la rama `main`.
3. En el repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, rama `main`, carpeta `/ (root)` → **Save**.
4. En un par de minutos la página queda en `https://<tu-usuario>.github.io/verificador-traspasos/`.

> Nota: en un plan gratuito de GitHub, Pages requiere que el repositorio sea público. Esto solo expone el código de la página, no los Excel (esos nunca salen del navegador de quien la usa).
