# Auditoría · Versión A

A-01 (No registra avistamiento): 
Causa: En el frontend, al crear un registro, se enviaba la llave criaturaId al backend en lugar de criatura. 
Solución: Corregir la asignación en FormularioAvistamiento.tsx para que siempre envíe datos.criatura = form.criatura.   

A-02 (Lista no identifica criatura): 
Causa: El método listar en el servicio de avistamientos devuelve los documentos crudos sin unirlos con la colección de criaturas. 
Solución: Añadir .populate('criatura') a la consulta de Mongoose en avistamientos.service.ts.   

A-03 (Acepta peligro 999): 
Causa: En el servicio de criaturas, la actualización ignora las reglas del esquema (rango 1-10) porque findByIdAndUpdate no las ejecuta por defecto. 
Solución: Añadir la opción runValidators: true en criaturas.service.ts.   

A-04 (Filtro no actualiza): 
Causa: El useEffect que carga las criaturas no tiene la variable del filtro (tipo) en su arreglo de dependencias. Solución: Cambiar el arreglo de [recarga] a [recarga, tipo] en ListaCriaturas.tsx. 