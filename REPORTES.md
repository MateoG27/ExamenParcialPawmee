# Reportes de soporte · Versión A

Estos reportes no indican la causa ni qué archivo cambiar. Hay registros semilla para investigar cada incidencia independientemente.

## A-01 · No se registra el avistamiento

### Síntoma y reproducción
En Avistamientos → Registrar avistamiento, elegir una criatura existente y completar testigo, ubicación, fecha y descripción. Guardar no termina correctamente y el registro no aparece.

### Resultado esperado
- El formulario crea el registro (201) y abre su detalle.
- GET y recarga confirman persistencia y asociación a la criatura elegida.
- Una referencia inexistente por cliente HTTP devuelve 404 sin crear un registro.

## A-02 · La lista no identifica a la criatura

### Síntoma y reproducción
Abrir el listado general de avistamientos. Los registros aparecen, pero el nombre de la criatura asociada no se muestra correctamente.

### Resultado esperado
- Cada avistamiento semilla muestra el nombre de su criatura, no solo el id.
- Respuesta API y uso del dato en React tienen una forma coherente.
- Una consulta sin resultados muestra vacío, no una pantalla rota.

## A-03 · Se acepta un peligro inválido

### Síntoma y reproducción
Desde un cliente HTTP, actualizar una criatura con nivelPeligro 999. El sistema lo permite, aunque el rango debe ser 1–10. La validación HTML no protege a la API.

### Resultado esperado
- Un valor válido como 7 se guarda con status 200.
- El valor 999 se rechaza con 400 y mensaje comprensible.
- Un GET después del rechazo conserva el último valor válido.

## A-04 · El filtro no actualiza la pantalla

### Síntoma y reproducción
En Criaturas cambiar Todos a mitica y luego a mecanica, sin pulsar Actualizar lista. La selección y los resultados no corresponden.

### Resultado esperado
- El cambio de selector inicia la consulta correcta y actualiza datos.
- Se distinguen loading, error y empty; mecanica está vacío en la semilla.
- Volver a Todos restaura el listado sin actualización manual.

