# Análisis de simulaciones cerradas - Nube Pública V - OCI

Fecha de elaboración: 2026-07-16.

## Alcance solicitado

Se requiere revisar el portal público de simuladores de Colombia Compra Eficiente, filtrar por:

- Estado de Simulación: Cerrado.
- Instrumento: Nube pública V.
- Elementos por página: 100.
- Detalle de cada `#Simulación`.
- Nube: Oracle Cloud Infrastructure / OCI.
- Pestaña: Respuestas.
- Métrica: menor `Precio Ofertado Con Impuestos` entre proveedores.

## Estado real de la consulta

La captura proporcionada por el usuario confirma que el portal **sí devuelve simulaciones** al aplicar los filtros `Cerrado` y `Nube pública V`. Por ejemplo, en la captura se ven los números `39229`, `39267`, `39311`, `39310`, `39302`, `39278`, `39268`, `38947` y `39265`.

La simulación `39311` quedó validada como `Oracle Cloud Infrastructure`: corresponde al evento de cotización `26536`, RFI `214768` y tiene `7` respuestas. Al comparar la columna `Precio Ofertado Con Impuestos`, el menor valor visible es **COP $728.930.575,00**, ofertado por **ITERIA SAS - IAD Software por Catalogo II**. Este registro se incorporó al CSV y al reporte HTML.

Esto no confirma todavía que esas simulaciones sean OCI: es necesario abrir cada una, revisar el campo **Nube** y, solo para las que indiquen `Oracle Cloud Infrastructure` / `OCI`, revisar la pestaña **Respuestas** para calcular el menor `Precio Ofertado Con Impuestos`.

## Limitación técnica de la automatización

Durante la extracción desde este entorno, el acceso HTTP directo al dominio `simuladoresvistapublica.colombiacompra.gov.co` fue bloqueado por el proxy corporativo del contenedor con respuesta `403 Forbidden` al intentar abrir un túnel HTTPS. Por esa razón no fue posible descargar programáticamente la información viva del portal desde la terminal del repositorio.

El valor `0` del reporte significa **cero registros descargados automáticamente por el contenedor**, no cero resultados en el portal ni cero simulaciones OCI.

## Entregables generados

- `reports/oci_simulaciones_vista_publica_reporte.html`: reporte ejecutivo en formato texto/HTML, visible en la web y copiable a Excel.
- `reports/oci_simulaciones_vista_publica.csv`: estructura tabular compatible con Excel, lista para incorporar exclusivamente las simulaciones OCI que se validen en el portal.
- Nota: se evita depender de archivos binarios porque la vista web del repositorio puede mostrar el mensaje `Archivo binario no mostrado` o `Los archivos binarios no se admiten`.

## Estructura analítica del reporte compatible con Excel

Columnas principales del detalle:

1. Número de simulación.
2. Entidad compradora.
3. Nombre u objeto de la simulación.
4. Estado.
5. Instrumento.
6. Nube identificada.
7. Proveedor ganador por menor precio.
8. Precio ofertado con impuestos mínimo.
9. Moneda.
10. Número de proveedores evaluados.
11. URL pública de la simulación.
12. Observaciones de validación.

## Siguiente paso para completar el análisis

Desde el navegador que sí tiene acceso al portal, abrir cada `#Simulación` de la lista filtrada y recopilar solo las que indiquen OCI. Para cada una, copiar o guardar los datos de la pestaña **Respuestas**. Si se comparte esa información (archivo descargado, texto o capturas legibles), se puede completar el CSV y el reporte con el proveedor y precio mínimo reales.

## Recomendación operativa

Ejecutar la extracción en una red que permita acceso HTTPS al dominio oficial y registrar cada simulación OCI cerrada en el archivo entregado. El reporte está preparado para consolidar el conteo de simulaciones OCI, el valor mínimo global y el proveedor más competitivo.
