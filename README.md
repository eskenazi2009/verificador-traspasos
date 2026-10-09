# Verificador de Traspasos

Página web para verificar los traspasos de **C99 Oficina** a las 4 tiendas New Balance (**A2 Multiplaza, A3 Albrook, A4 Dorado, A7 Metromall**): cruza el Excel que manda cada tienda (lo recibido físicamente) contra el Excel de traspasos descargado del sistema, por **referencia y talla**, y genera un reporte por tienda de qué referencias están OK y cuáles tienen diferencias.

Todo se procesa en el navegador; los archivos no se suben a ningún servidor.

## Cómo se usa

1. Carga el Excel de **traspasos del sistema** (uno solo, con las 4 tiendas). Siempre tiene este formato, con encabezados en la fila 1:
   `Cód. Barras | Referencia | Talla | Color | Descripción | Cód. Almacén Origen | Cód. Almacén Destino | UDS. Env`
   - Si alguna línea tiene un origen distinto a **C99** o un destino distinto a **A2, A3, A4, A7**, la página marca error con el número de fila y no deja verificar.
   - Debajo del archivo se ven las unidades y referencias que van a cada tienda.
2. Carga en la casilla de cada tienda su archivo de recibo (el **MAPPING RECIBO DE TRASPASOS**). Siempre tiene la hoja `mapping` con encabezados en la fila 1:
   `COD BARRA | Referencia | Talla | Cantidad | Color | DESCRIPCION` — una fila por cada par escaneado (Referencia, Talla, etc. salen de la hoja DATA).
   - Si alguna fila sale **NO COINCIDE** (el código escaneado no está en DATA), la página marca error con el número de fila y no deja verificar.
   - No hace falta tener las 4 tiendas: las que falten salen como *Sin archivo de tienda*.
   - El cruce es por **Referencia + Talla** (los códigos de barras de la tienda son del fabricante y los del sistema son internos, no coinciden).
   - Tallas unisex: si la tienda trae un solo número (ej. `5`) y el sistema tiene esa referencia con talla doble (ej. `H5|M6.5`), el número se toma como la talla de **hombre**.
3. Clic en **Verificar traspasos**. Hay una pestaña de **Resumen** con todas las tiendas y una pestaña por tienda con el detalle.
4. **Descargar reporte Excel**: hoja *Resumen* + por cada tienda una hoja por referencia (Referencia, Color) y una hoja por talla (Referencia, Color, Talla). También se puede imprimir / guardar como PDF la pestaña abierta.

### Estados por talla

| Estado | Significado |
|---|---|
| OK | Físico = Sistema |
| Faltante | Llegó menos de lo enviado |
| Sobrante | Llegó más de lo enviado |
| No recibido | Estaba en el traspaso y no llegó nada |
| No estaba en traspaso | Llegó algo que no estaba en el traspaso |

Una referencia está **OK** solo si todas sus tallas están OK.

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub (ej. `verificador-traspasos`).
2. Sube `index.html` y `README.md` a la rama `main`.
3. En el repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, rama `main`, carpeta `/ (root)` → **Save**.
4. En un par de minutos la página queda en `https://<tu-usuario>.github.io/verificador-traspasos/`.

> Nota: en un plan gratuito de GitHub, Pages requiere que el repositorio sea público. Esto solo expone el código de la página, no los Excel (esos nunca salen del navegador de quien la usa).
