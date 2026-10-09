# Verificador de Traspasos

Página web para verificar traspasos de oficina a tiendas: cruza el Excel que manda la tienda (lo recibido físicamente) contra el Excel del traspaso descargado del sistema, por **referencia y talla**, y genera un reporte de qué referencias están OK y cuáles tienen diferencias.

Todo se procesa en el navegador; los archivos no se suben a ningún servidor.

## Cómo se usa

1. Llena tienda, número de traspaso y fecha (salen en el reporte).
2. Carga el Excel del **sistema** y el Excel **físico** de la tienda.
   - La página detecta sola la fila de encabezados y las columnas de Referencia, Talla y Cantidad. Si no acierta, se pueden elegir a mano.
   - Acepta los dos formatos: **una fila por talla**, o **tallas en columnas** (matriz tipo `Referencia | 7 | 7.5 | 8 ...`).
   - **Filtrar por columna**: si el export del sistema trae varios traspasos o tiendas, elige la columna (ej. *Tienda destino* o *Documento*) y deja marcados solo los valores que corresponden.
3. Clic en **Verificar traspaso**.
4. Descarga el **reporte Excel** (hojas: Resumen, Por referencia, Detalle por talla, Solo diferencias) o imprímelo / guárdalo como PDF.

El botón **Descargar plantilla para tiendas** da un Excel con las columnas `Referencia | Talla | Cantidad` para que las tiendas lo llenen siempre igual.

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
