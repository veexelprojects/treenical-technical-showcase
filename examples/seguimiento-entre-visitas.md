# Seguimiento entre visitas

Caso sintético. No describe un plan de cuidado real.

## Situación

Al cerrar la consulta de **S-014**, la nota queda guardada por el clínico. El plan de la nota dice que conviene saber, a los pocos días, si apareció mareo o hinchazón. El clínico no quiere un segundo canal ni un mensaje de texto con el síntoma escrito en la notificación.

## Qué hace cada feature

1. **Documentación.** Conserva la nota y la transcripción por separado. La plantilla estructuró la nota. No programa el contacto: eso no es una sección del editor.
2. **Mensajes.** Ya existe un hilo activo de S-014, abierto por enlace. El clínico deja una tarjeta de check-in a tres días, prioridad rutinaria, con una pregunta concreta. El paciente entra con el enlace y la contraseña de ese hilo. No crea cuenta.
3. **Aviso.** Si el producto señala el pendiente fuera del enlace, el aviso no incluye síntomas, laboratorios ni el nombre del fármaco.
4. **Bandeja, si nadie responde.** Al vencer la ventana, la tarjeta pasa a “en silencio” y aparece en la bandeja como check-in, no como “paciente sin actualización en el roster”. Son señales distintas: una tenía fecha y dueño; la otra es ausencia larga de cambios en la ficha.
5. **Bandeja, si responde.** Una respuesta de mareo marcado sube al hilo y a la bandeja como check-in respondido. El escritorio del clínico lo ve en el momento. El texto no se copia al expediente.
6. **Validación.** El clínico puede promover un resumen del intercambio. Ese resumen entra a la cola. Aceptarlo escribe en el expediente y deja atribución. Descartarlo deja el chart como estaba.
7. **Cierre del hilo.** Cuando la sesión caduca o el clínico la cierra, los mensajes se borran. La nota de la visita y cualquier fila ya aceptada permanecen.

## Qué no ocurre

- El silencio no genera una alerta de laboratorio. La alerta sigue saliendo solo de la serie y de la regla.
- La respuesta del paciente no dispara un algoritmo ni una nota nueva.
- El copiloto no lee el hilo. Lee filas aceptadas. Hasta que alguien promueve y acepta, el retrato no menciona el mareo.

## Por qué el objeto es una tarjeta

Un párrafo libre más en el chat no dice si el paciente contestó, si la ventana venció o si alguien tiene que mirarlo. La tarjeta tiene estado. La bandeja solo necesita ese estado para poner el ítem en la lista correcta.
