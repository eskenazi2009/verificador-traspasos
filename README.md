# Verificador de Traspasos

Página web para verificar los traspasos de **C99 Oficina** a las 4 tiendas New Balance (**A2 Multiplaza, A3 Albrook, A4 Dorado, A7 Metromall**): cruza el Excel que manda cada tienda (lo recibido físicamente) contra el Excel de traspasos descargado del sistema, por **referencia y talla**, y genera un reporte por tienda de qué referencias están OK y cuáles tienen diferencias.

Todo se procesa en el navegador; los archivos no se suben a ningún servidor.

## Cómo se usa

1. Carga el Excel de **traspasos del sistema** (uno solo, con las 4 tiendas).
   - Detecta sola la fila de encabezados, las columnas de Referencia, Talla, Cantidad y la columna de **tienda destino**, y asigna cada valor de esa columna a su tienda (por código `A2`/`A3`/`A4`/`A7` o por nombre). Se puede ajustar en *Ajustar columnas*.
   - *Filtrar por otra columna* sirve si el export trae traspasos que no se quieren verificar (ej. por documento o fecha).
2. Carga el Excel **físico** de cada tienda en su casilla. No hace falta tener las 4: las que falten salen como *Sin archivo de tienda*.
   - Acepta **una fila por talla** o **tallas en columnas** (`Referencia | 7 | 7.5 | 8 ...`).
3. Clic en **Verificar traspasos**. Hay una pestaña de **Resumen** con todas las tiendas y una pestaña por tienda con el detalle.
4. **Descargar reporte Excel**: hoja *Resumen* + por cada tienda una hoja por referencia y una hoja por talla. También se puede imprimir / guardar como PDF la pestaña abierta.

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
