# Uso de IA
Utilicé Gemini para identificar los errores de enrutamiento/validación y Cursor con el agente Claude Sonnet 5.5 para generar los reemplazos de código exactos.
Gemini me ayude a explicar los pasos para abordar los problemas de la mejor manera y principalmente con los codigos para la terminal, sobre todo para generar el zip. Tambien me ayudó bastante cuando la base de datos de Mongo DB no se conectaba con mi backend. 

Cursor se encargó de corregir los 4 errores con la ayuda de un prompt especifico y claro que generó Gemini.

Prompt usado en Cursor: 

Act as an expert Full-Stack Developer. I am taking a timed practical exam and need to fix 4 specific bugs in my codebase without changing the UI, architecture, or any other logic. 

Please apply the following exact fixes to these 4 files:

1. In `frontend/src/paginas/FormularioAvistamiento.tsx`:
Find the line inside the `enviar` function:
`datos[id ? 'criatura' : 'criaturaId'] = form.criatura;`
Change it to:
`datos.criatura = form.criatura;`

2. In `backend/src/services/avistamientos.service.ts`:
Find the `listar` function. Currently, the return statement is:
`return Avistamiento.find(criaturaId ? { criatura: criaturaId } : {}).sort({ fecha: -1, _id: -1 }).lean();`
Add `.populate('criatura')` before `.sort()`. It should look like:
`return Avistamiento.find(criaturaId ? { criatura: criaturaId } : {}).populate('criatura').sort({ fecha: -1, _id: -1 }).lean();`

3. In `backend/src/services/criaturas.service.ts`:
Find the `actualizar` function. Currently, the update operation is:
`const doc = await Criatura.findByIdAndUpdate(idValido(id), { $set: cambios }, { new: true });`
Add `runValidators: true` to the options object. It should look like:
`const doc = await Criatura.findByIdAndUpdate(idValido(id), { $set: cambios }, { new: true, runValidators: true });`

4. In `frontend/src/paginas/ListaCriaturas.tsx`:
Find the `useEffect` hook that fetches the data (the one containing `listarCriaturas(tipo)`). Its dependency array is currently `[recarga]`. 
Change the dependency array to include `tipo`. It should look like:
`}, [recarga, tipo]);`

Apply ONLY these changes. Do not refactor the code or add any styling.
