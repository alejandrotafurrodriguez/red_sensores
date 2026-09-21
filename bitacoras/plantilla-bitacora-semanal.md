# Bitacora individual - Semana [XX]

> Copia este archivo y renombralo como `s[XX]-[tu-nombre].md`.
> Completa todas las secciones con tus propias palabras. Esta bitacora es
> individual, aunque el codigo pueda haberse construido en equipo.

## 1. Datos de la actividad

- **Estudiante:** [Alejandro Tafur Rodriguez]
- **Equipo:** [Alejandro Tafur Rodriguez]
- **Semana:** [Semana 3]
- **Fecha del laboratorio:** [2026-09-21]
- **Fecha del taller:** [2026-09-21]
- **Tema principal:** [Algoritmos de busqueda puntual]
- **Pregunta de la semana:** [¿Cuánto trabajo necesita un algoritmo para encontrar un dato cuando la cantidad de información crece?]

## 2. Prediccion antes de ejecutar

Antes de abrir o ejecutar el programa, responde:

1. **Que creo que va a ocurrir?**
   [la busqueda linal hara N comparaciones, mientras que la busqueda binaria requerira muy pocas comparaciones, requiriendo solo unas 20 comparaciones para 1.000.000 de registros]

2. **Que parte del programa o del algoritmo puede fallar?**
   [la busqueda binaria por PM2.5, por que los datos no estan ordenados por ese atributo y no se cumple la precondicion del algoritmo]

3. **Como comprobare mi prediccion?**
   [ejecutando BancoDePruebas: comparare las metricas en consola para la linal vs. binaria y verifique los errores de busqueda al intentar usar binaria sobre PM2.5 no ordenado]

## 3. Evidencia del laboratorio

### Resultado observado

[experimento 1 y 2: para 1.000.000 de lecturas, la busqueda lineal realizo 1.000.000 de comparaciones (54,314ms), mientras que la busqueda binaria realizo solo 20 comparaciones, siendo 50.000 veces mas eficiente
experimento 3: ante un dato inexistente en 100.000 registros, la busqueda lineal realizo 100.000 comparaciones y la binaria solo 17
experimento 4: de 20 valores PM2.5 existentes, la busqueda lineal encontro los 20, mientras que la busqueda binaria encontro 0]

### Diferencia entre la prediccion y el resultado

[el resultado coincidio totalmente con la prediccion: la busqueda binaria demostro una eficiencia logaritmica frente a una lineal en datos ordenados, y fallo por completo al aplicarse sobre PM2.5 por no cumplir la precondicion de ordenamiento]

### Error o comportamiento inesperado

- **Que ocurrio?** [la busqueda binaria no encontro ninguno de los 20 datos de PM2.5 que si existian en el arreglo]
- **Por que ocurrio?** [Por que los datos no estaban ordenados por PM2.5, violando la precondicion que requiere el algoritmo]
- **Como lo corregimos o que falta corregir?** [para usar busqueda binaria por PM2.5 debemos ordenar primero el arreglo por este criterio o recurrir a la busqueda lineal]

## 4. Explicacion en lenguaje llano

Explica el concepto principal como se lo explicarias a una persona de doce
anos. Usa entre tres y cinco lineas y evita palabras tecnicas que no expliques.

> [Buscar un dato linealmente es como revisar un libro página por página desde el inicio hasta encontrar lo que buscas. La búsqueda binaria es como abrir el libro por la mitad: si el tema está más adelante, descartas la primera mitad completa y repites el proceso con lo que queda. Así reduces a la mitad las opciones en cada paso, siempre y cuando las páginas estén ordenadas.]

### Ejemplo o analogia

[Buscar una palabra en un diccionario impreso. Gracias a que las palabras están en orden alfabético, abres el libro cerca de la letra deseada y descartas bloques enteros de páginas. Si las palabras estuvieran desordenadas, tendrías que leer palabra por palabra de principio a fin. La analogía deja de ser exacta porque en el diccionario no siempre abrimos exactamente en la mitad matemática, mientras que el algoritmo sí lo hace de forma estricta.]

## 5. El vacio que encontre

Al intentar explicar el tema, identifica el punto que aun no comprendes bien.

- **Mi duda concreta es:** [¿Por qué la búsqueda binaria arrojó 0 aciertos en PM2.5 si los datos sí existían en el arreglo?]
- **Lo que ya puedo explicar es:** [Que la búsqueda binaria requiere obligatoriamente que la estructura de datos esté ordenada por el criterio de búsqueda antes de ejecutar el algoritmo.]
- **Para resolver la duda consulte:** [El experimento 4 de BancoDePruebas.java y la documentación de decisiones de diseño (docs/decisiones.md)]
- **Ahora lo entiendo asi:** [Al no cumplirse la precondición de ordenamiento sobre PM2.5, el algoritmo descarta por error la mitad del arreglo donde sí estaba el dato, generando un falso negativo]

## 6. Trazado de la solucion

Escoge una ejecucion, recorrido o caso representativo y trazalo paso a paso.
Incluye los valores importantes despues de cada paso.

| Paso | Estado de los datos o estructura | Decision o resultado |
|---|---|---|
| 1 | [`[1000, 1010, 1020, 1030, 1040, 1050, 1060]`. Buscando `1060`. Rango: `inicio = 0`, `fin = 6`.] | [`medio = 3` (valor = `1030`). Como `1060 > 1030`, descarta la mitad izquierda y ajusta `inicio = 4`.] |
| 2 | [`[1040, 1050, 1060]`. Rango: `inicio = 4`, `fin = 6`.] | [`medio = 5` (valor = `1050`). Como `1060 > 1050`, descarta la mitad izquierda y ajusta `inicio = 6`.] |
| 3 | [`[1060]`. Rango: `inicio = 6`, `fin = 6`.] | [`medio = 6` (valor = `1060`). Como `1060 == 1060`, ¡coincidencia encontrada!] |
| 4 | [Estado final] | [Retorna el objeto `LecturaSensor` encontrado en el índice 6 tras únicamente 3 comparaciones.] |

**Completa o agrega filas si es necesario.** Si trabajaste con una estructura,
dibuja su estado en cada paso o inserta aqui una imagen legible.

## 7. Decision de diseño

Relaciona lo aprendido con la Plataforma de Monitoreo Ambiental Urbano.

- **Problema que debiamos resolver:** [Permitir consultas rápidas por timestamp en el historial de lecturas ambientales a medida que la base de datos crece a millones de registros.]
- **Estructura, algoritmo o estrategia elegida:** [Búsqueda Binaria sobre arreglos ordenados cronológicamente por timestamp]
- **Alternativa descartada:** [Búsqueda Lineal.]
- **Por que elegimos la primera:** [garantiza una complejidad logaritmica, reduciendo de 1.000.000 a solo 20 comparaciones]
- **Que evidencia respalda la decision:** [Los datos del Experimento 2, donde la búsqueda binaria fue $50.000$ veces más rápida que la lineal para $1.000.000$ de lecturas.]

## 8. Aporte al proyecto

- **Archivo(s) o modulo(s) trabajado(s):** [BuscadorLecturas.java, GeneradorDatos.java, BancoDePruebas.java e IngestaSensores.java]
- **Cambio realizado:** [Implementación de los métodos de búsqueda puntual (lineal y binaria), generación de datos sintéticos, orquestación de experimentos y su integración al flujo principal de ejecución]
- **Como se conecta con la capa anterior:** [Utiliza las estructuras y objetos de lectura (LecturaSensor) ingresados en la fase de ingesta para ejecutar análisis de rendimiento sobre el repositorio]
- **Que queda pendiente para la siguiente semana:** [Implementar algoritmos de ordenamiento para habilitar la búsqueda binaria sobre otros atributos como PM2.5.]

## 9. Commits realizados

Registra los commits que muestran tu aporte individual.

| Commit      | Mensaje | Que demuestra |
|-------------|---|---|
| `[a1b2c3d]` | `[feat(semana-3): implementa motor de busqueda y banco de pruebas]` | [Creación de algoritmos de búsqueda y pruebas experimentales.] |
| `[e3f5g6h]` | `[docs(semana-3): actualiza decisiones de diseño y bitacora s03-alejandro]` | [Documentación técnica y sustentación de resultados.] |

## 10. Reexplicacion final

Despues del taller, vuelve a responder la pregunta de la semana en cinco lineas
o menos. Esta respuesta debe ser mas precisa que la de la seccion 4 y debe
incluir la razon de tu decision tecnica.

> [El trabajo necesario para encontrar un dato depende del algoritmo y del estado de los datos. La búsqueda lineal requiere un trabajo que crece de manera directamente proporcional al tamaño de la información,, realizando hasta $N$ comparaciones. En cambio, la búsqueda binaria divide el espacio de búsqueda a la mitad en cada paso, logrando un crecimiento logarítmico, que requiere máximo 20 comparaciones para un millón de datos, siempre que se cumpla la precondición de que la información esté ordenada ]

## 11. Reflexion individual

Responde con honestidad:

1. **Lo que ahora puedo hacer y antes no podia:**
   [Demostrar con métricas cuantitativas la diferencia de eficiencia entre algoritmos de complejidad $O(n)$]
2. **El error o supuesto que mas me enseno:**
   [Asumir que la búsqueda binaria funciona siempre; comprobar el Experimento 4 me demostró que sin la precondición de orden el algoritmo falla]
3. **La pregunta que llevaria a la proxima clase:**
   [¿Cuál es el costo computacional de ordenar los datos primero para poder usar búsqueda binaria vs. mantener los datos ordenados desde el momento de la inserción?.]
4. **Que parte del trabajo fue realmente mia:**
   [La codificación de las pruebas en BancoDePruebas, la ejecución del análisis comparativo y la redacción de la documentación individual.]

## Lista de verificacion antes de entregar

- [ x ] Escribi la prediccion antes de consultar el resultado.
- [ x ] Inclui evidencia concreta del laboratorio.
- [ x ] Explique un concepto sin depender de jerga.
- [ x ] Registre un vacio, una duda o un error real.
- [ x ] Trace al menos un caso paso a paso.
- [ x ] Justifique una decision del proyecto y una alternativa descartada.
- [ x ] Registre mis commits y mi aporte individual.
- [ x ] Deje claro que queda pendiente.
- [ x ] Renombre el archivo con el formato `sXX-nombre.md`.
