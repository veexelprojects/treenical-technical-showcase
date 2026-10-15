# Treenical — Technical Showcase

Repositorio público de arquitectura y decisiones de diseño. Sirve para explicar cómo está construido Treenical en una aplicación de hackathon, sin abrir el producto.

Producto en vivo: [treenical.lovable.app](https://treenical.lovable.app)

El código de producción, los prompts propietarios, la infraestructura y las configuraciones internas permanecen privados.

## Para quien revisa en inglés

Treenical is a clinical operating system for clinicians and institutions. It keeps the longitudinal record, the note, the literature search, the institutional protocol, and the patient conversation in one workspace, and it refuses to let a language model write the chart on its own.

This repository explains the system design of every shipped feature except clinical-algorithm generation. It contains problem framing, architecture diagrams, design decisions, synthetic walkthroughs, and screenshots of the public product surface. It does not contain production source code, prompts, infrastructure, or internal configuration.

## Problema

El trabajo clínico está partido en piezas que no se hablan entre sí. El expediente vive en un sistema, la literatura en otro, el protocolo del hospital en un PDF, la nota en un editor, y el mensaje del paciente en un portal o en un teléfono. Cada pieza obliga al clínico a rearmar el contexto a mano.

Un modelo de lenguaje, usado solo, empeora esa fractura. Inventa una cita, mezcla una noticia con una ficha técnica, trata un preprint como si fuera una guía, y escribe en el expediente una frase que nadie revisó. La institución, además, no quiere la misma respuesta en dos hospitales con formularios, recursos y normas distintas.

Treenical existe para que una decisión de cabecera pueda ver, a la vez, al paciente, la evidencia y la regla local, y para que nada de lo que produce un modelo entre al expediente sin una persona.

## Solución

Un solo espacio de trabajo, con un dueño claro para cada pregunta:

| Pregunta | Quién la responde |
|---|---|
| ¿Quién es este paciente a lo largo del tiempo? | Expediente y línea longitudinal |
| ¿Qué cambió en los laboratorios, con la misma entrada y la misma salida? | Motor de alertas determinista |
| ¿Qué dice la literatura sobre esta pregunta? | Búsqueda de evidencia |
| ¿Qué exige esta institución? | Gobernanza |
| ¿Qué quedó dicho en la consulta? | Documentación clínica |
| ¿Qué necesita el paciente entre visitas? | Mensajes y seguimiento |
| ¿Qué hay que hacer ahora? | Bandeja de trabajo |
| ¿Cómo se razona con todo eso delante? | Asistente, en tres profundidades |

El asistente cita, separa evidencia de política institucional y, cuando el clínico enlaza un paciente, razona con ese expediente. Lo que el modelo propone para el chart espera en una cola hasta que una persona lo acepta.

La generación de algoritmos clínicos, árboles de decisión y mapas mentales queda fuera de este showcase.

## Tecnologías

La superficie de trabajo es una aplicación web en **TypeScript** y **React**. El estado remoto de cada pantalla pasa por una capa de datos por módulo, no por consultas sueltas repartidas en la interfaz.

El sistema de registro es una base **relacional** con **seguridad por fila**. Esa política es la frontera de autorización del clínico: la interfaz no decide por su cuenta quién puede leer un expediente.

Las operaciones que necesitan un secreto, un modelo o una identidad que no es una cuenta de producto corren en **funciones de servidor**. El navegador no habla con el proveedor del modelo.

Las llamadas a modelo y la recuperación de literatura pasan por un **runtime de IA** compartido. Cada feature pide una capacidad (responder, reescribir, extraer, transcribir, resumir). No lleva su propio cliente, ni su propia copia de un prompt. Los prompts, el enrutamiento concreto de modelos y la configuración de ese runtime no se publican aquí.

La literatura se recupera de índices biomédicos y de un conjunto curado de editores profesionales. El cifrado publicado del producto es **TLS** en tránsito y **AES-256** en reposo, con control de acceso por roles.

## Cómo está organizado

```text
README.md          Problema, solución y tecnologías
architecture/      Diagramas y decisiones por feature
demo/              Capturas del producto público
examples/          Recorridos sintéticos, sin pacientes reales
```

## Mapa de arquitectura

1. [Contexto del sistema](architecture/01-contexto.md)
2. [Identidad, organizaciones y acceso](architecture/02-identidad-y-acceso.md)
3. [Expediente longitudinal](architecture/03-expediente.md)
4. [Alertas clínicas](architecture/04-alertas.md)
5. [Asistente clínico](architecture/05-asistente.md)
6. [Evidencia](architecture/06-evidencia.md)
7. [Gobernanza](architecture/07-gobernanza.md)
8. [Documentación clínica](architecture/08-documentacion.md)
9. [Mensajes y seguimiento](architecture/09-mensajes-y-seguimiento.md)
10. [Copiloto del paciente](architecture/10-copiloto.md)
11. [Bandeja de trabajo](architecture/11-bandeja.md)
12. [Fronteras que atraviesan todas las features](architecture/12-fronteras.md)

El índice comentado está en [architecture/README.md](architecture/README.md).

## Qué permanece privado

- El código de producción y su historial.
- Los prompts, las plantillas de salida y los casos de evaluación.
- La infraestructura, los proyectos, las claves, las políticas internas y la configuración de despliegue.
- La generación de algoritmos clínicos.

© 2026 Treenical. Todos los derechos reservados. Este repositorio describe la arquitectura para evaluación. No otorga licencia sobre el producto, los modelos ni el contenido clínico.
