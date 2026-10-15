# Pregunta con evidencia y protocolo

Caso sintético. Las fuentes de abajo están escritas como ilustración. No son el resultado de una búsqueda real.

## Situación

El clínico tiene enlazado a **S-014** y pregunta, en modo **Rapid**:

> ¿Cabe intensificar el tratamiento de la insuficiencia cardíaca con la función renal de esta semana?

La institución tiene un protocolo vigente, versión 3: en empeoramiento renal reciente, no se inicia un fármaco nuevo de ese grupo hasta repetir el laboratorio, y el formulario local lista dos principios activos.

## Qué hace cada feature

1. **Asistente.** Toma el modo Rapid, el enlace al paciente y la identidad de quien pregunta. No abre una generación de algoritmo.
2. **Expediente.** Aporta la historia aceptada y el laboratorio de hoy. Las propuestas todavía en cola no entran.
3. **Alertas.** En Rapid no se pide la revisión de conducta. La alerta renal existe en la ficha; Audit la incorporaría como contexto. Rapid no la reescribe.
4. **Gobernanza.** Resuelve el protocolo de la institución, versión 3, para esta persona.
5. **Evidencia.** Recupera pasajes sobre el tratamiento en insuficiencia cardíaca y función renal. Un ensayo que responde la pregunta ordena por encima de una nota de prensa en una revista de más nombre. Un preprint no se presenta como guía. La ficha técnica del fármaco, si la pregunta es de medicamento, no se sustituye por una noticia.
6. **Runtime.** Devuelve la respuesta en streaming, con citas, y separa dos voces.

## Cómo se lee la respuesta

La ilustración, no una cita real, sería de esta forma:

- **Evidencia.** La literatura recuperada sostiene el uso del grupo farmacológico en insuficiencia cardíaca, con vigilancia renal. Cada frase que afirma eso apunta a un pasaje, con tipo de estudio.
- **Política institucional.** El protocolo v3 pide repetir el laboratorio antes de iniciar. Eso se etiqueta como protocolo, no como resultado de un ensayo.
- **Expediente.** La creatinina de esta semana es la razón por la que el protocolo aplica. El número sale del evento, no del modelo.

No hay una tercera voz que diga “entonces inicie hoy”.

## Qué no ocurre

- La respuesta no se guarda sola en la lista de problemas de S-014.
- Si el clínico elige empujar una frase al perfil, esa frase espera en la cola hasta que la acepta.
- Cambiar a **Dive** ampliaría la recuperación y el ranking. No cambiaría el protocolo ni saltaría la cola.
- Cambiar a **Audit** añadiría una puntuación citada por dimensiones de la conducta, usando la alerta ya calculada. No lanzaría una segunda búsqueda más profunda: para eso está Dive.
