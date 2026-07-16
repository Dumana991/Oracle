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

## Limitación técnica encontrada

Durante la extracción desde este entorno, el acceso HTTP directo al dominio `simuladoresvistapublica.colombiacompra.gov.co` fue bloqueado por el proxy corporativo del contenedor con respuesta `403 Forbidden` al intentar abrir un túnel HTTPS. Por esa razón no fue posible descargar programáticamente la información viva del portal desde la terminal del repositorio.

## Entregables generados

- `reports/oci_simulaciones_vista_publica_reporte.html`: reporte ejecutivo en formato texto/HTML, visible en la web y copiable a Excel.
- `reports/oci_simulaciones_vista_publica.csv`: estructura tabular compatible con Excel; incluye una fila explicativa `SIN_DATOS_EXTRAIDOS` porque la extracción real fue bloqueada desde este entorno.
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

## Recomendación operativa

Ejecutar la extracción en una red que permita acceso HTTPS al dominio oficial y registrar cada simulación OCI cerrada en el archivo entregado. El reporte está preparado para consolidar el conteo de simulaciones OCI, el valor mínimo global y el proveedor más competitivo.
