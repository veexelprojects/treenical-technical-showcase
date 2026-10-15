# Expediente, alerta y validación

Caso sintético. No es un paciente real ni una pauta de tratamiento.

## Situación

La clínica abre la ficha de **S-014, “R. Salas”**, 67 años. En la historia aceptada ya constan insuficiencia cardíaca y un inhibidor de la enzima convertidora. No hay propuestas pendientes.

Hoy se carga un laboratorio: creatinina por encima de la serie previa, con dos valores anteriores más bajos en los últimos meses.

## Qué hace cada feature

1. **Expediente.** El laboratorio entra como evento longitudinal. No reescribe la lista de problemas.
2. **Alertas.** El motor ordena la serie, calcula la tendencia y dispara la regla de empeoramiento renal registrada en el paquete de reglas. La misma serie, corrida otra vez, produce la misma alerta. No interviene un modelo.
3. **Bandeja.** La alerta queda por encima de los mensajes y de los pacientes sin actualización reciente. Abrirla lleva a la línea de tiempo de S-014.
4. **Copiloto.** La huella de “reciente” cambió por el laboratorio nuevo. El retrato de base no cambia, porque la medicación y los problemas aceptados siguen iguales. Solo se regenera el artefacto reciente.
5. **Documentación.** En la nota del día el clínico dicta el hallazgo. Al pedir extracción, el sistema propone “ajuste a vigilar” como ítem. Ese ítem cae en la cola. La creatinina ya está en el evento; el ítem propuesto no se convierte solo en un diagnóstico nuevo.

## Qué ve el clínico

- Una alerta explicada por la serie y por la regla, con enlace a la observación.
- Un retrato estable que todavía dice insuficiencia cardíaca y el mismo fármaco de base.
- Una tarjeta de “reciente” que menciona el laboratorio de hoy.
- Una propuesta en revisión, todavía fuera de la historia aceptada.

## Qué no ocurre

El modelo no suaviza la alerta, no gradúa la creatinina como si fuera un paper y no añade una fila de problema porque la nota la mencionó.

Si el clínico acepta la propuesta, la fila pasa al expediente con atribución: quién, cuándo y desde qué nota. La huella del copiloto vuelve a cambiar en el siguiente refresco, y solo entonces el retrato puede mencionar el hecho nuevo.
