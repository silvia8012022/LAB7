# Historias de usuario de búsqueda

| Campo | Valor |
| --- | --- |
| Proyecto | Proyecto Simbiosis |
| Fecha | [dd/mm/aaaa] |
| Versión | [Versión de trabajo] |
| Estado | Borrador |

## Fuentes comunes

- [Acta de UC-21 Buscar recetas](../captura/acta-acuerdos-uc-21-buscar-recetas.md), v1.1, Vigente.
- [Catálogo de requisitos](catalogo-requisitos.md), UR-08 y FR pertinentes.
- [Modelo de casos de uso](../modelos/modelo-casos-de-uso.md), UC-21.

## Épica de búsqueda

Como cocinero o usuario del sistema, quiero buscar recetas por texto libre, seleccionando ingredientes incluidos y excluyendo ingredientes no deseados, para encontrar fácilmente opciones culinarias adaptadas a mis gustos, disponibilidad de despensa o restricciones alimentarias.

Estado: descompuesta en US-01, US-02 y US-03. Conserva la necesidad conjunta.

## Justificación de la división

La división en tres historias independientes separa tres capacidades funcionales distintas de búsqueda, permitiendo que cada una entregue valor útil de forma autónoma:

US-01 permite una búsqueda rápida y general por texto (título, descripción, etiquetas).

US-02 resuelve la necesidad de aprovechar ingredientes específicos disponibles en la cocina.

US-03 aborda de forma independiente la seguridad y preferencias del usuario (alergias o intolerancias) mediante la exclusión.

Esta separación evita dividir el trabajo por componentes técnicos o pantallas y permite un desarrollo e integración incremental sin que una historia bloquee el uso de las otras.

## US-01
Título: Buscar mediante una palabra o frase

Como usuario del sistema, quiero buscar recetas introduciendo un término o frase en el cuadro de búsqueda, para localizar rápidamente recetas cuyo título, descripción o etiquetas contengan dicho texto.

Fuentes: UR-08; UC-21; FR-085; acta de UC-21 v1.1, apartado 3.1.

Criterios de aceptación

CA-01. Dado que el usuario introduce un término o frase clave en el buscador (ej. "pasta" o "salsa verde"), cuando ejecuta la búsqueda, entonces el sistema muestra el listado de recetas que contienen la coincidencia en su título, descripción o etiquetas.

CA-02. Dado que el usuario busca un término que no coincide con ninguna receta del catálogo, cuando se procesa la búsqueda, entonces el sistema muestra un mensaje indicando que no hay resultados junto con sugerencias de ayuda y recetas recomendadas (FR-102).

CA-03. Dado que el usuario intenta realizar una búsqueda con el campo de texto vacío o formado solo por espacios, cuando presiona el botón de búsqueda, entonces el sistema requiere al usuario introducir al menos un carácter válido sin ejecutar una consulta vacía.

## US-02


Título: Buscar por ingredientes incluidos

Como usuario con ingredientes disponibles en la cocina, quiero seleccionar uno o varios ingredientes necesarios en la búsqueda, para obtener un listado de recetas que utilicen obligatoriamente dichos ingredientes en su preparación.

Fuentes: UR-08; UC-21; FR-086; acta de UC-21 v1.1, apartado 3.2.
Criterios de aceptación

    CA-01. Dado que el usuario selecciona uno o varios ingredientes a incluir (ej. "tomate" y "huevo"), cuando aplica la búsqueda, entonces el sistema devuelve únicamente las recetas que incluyan todos los ingredientes seleccionados.

    CA-02. Dado que el usuario empieza a escribir el nombre de un ingrediente en el filtro de inclusión, cuando escribe al menos dos caracteres, entonces el sistema despliega sugerencias autocompletadas de ingredientes existentes en el catálogo.

    CA-03. Dado que la combinación de ingredientes incluidos no coincide con ninguna receta registrada, cuando se ejecuta la búsqueda, entonces el sistema muestra una notificación informando de la ausencia de coincidencias junto con alternativas para suavizar el filtro (FR-102).
## US-03

Título: Excluir ingredientes

Como usuario con alergias, intolerancias o preferencias alimentarias, quiero indicar ingredientes que deben ser excluidos del resultado de búsqueda, para obtener un listado de recetas seguras que no contengan ninguno de esos elementos.

Fuentes: UR-08; UC-21; FR-087; acta de UC-21 v1.1, apartado 3.3.

Criterios de aceptación

CA-01. Dado que el usuario especifica uno o más ingredientes a excluir (ej. "cacahuete" o "marisco"), cuando ejecuta la búsqueda, entonces el sistema omitirá de los resultados todas las recetas que contengan dichos ingredientes.

CA-02. Dado que el usuario establece filtros de exclusión en combinación con una búsqueda por texto o por ingredientes incluidos, cuando confirma la consulta, entonces el sistema aplica la exclusión de forma estricta asegurando que no aparezcan recetas no deseadas.

CA-03. Dado que el usuario intenta agregar un mismo ingrediente a la lista de incluidos y a la de excluidos simultáneamente, cuando intenta confirmar la adición, entonces el sistema notifica el conflicto e impide la selección contradictoria.


## Revisión INVEST

La revisión abarca US-01, US-02 y US-03. «Aplicado» indica si se ha realizado la comprobación. «Cumple» indica si todas las historias cumplen el criterio. Si alguna no lo cumple, indicar «No» e identificar la historia y el motivo en la justificación. Si no se ha realizado la comprobación o faltan datos, indicar «Pendiente» en «Cumple».

| Criterio | Pregunta de revisión | Aplicado | Cumple | Justificación |
| --- | --- | --- | --- | --- |
| Independiente | ¿Puede implementarse cada historia y ofrecer un resultado útil sin implementar antes las otras historias del conjunto? Puede compartir infraestructura con ellas. | [Sí] | [Sí] | US-01, US-02 y US-03: Cada historia ofrece un filtro de búsqueda funcional e independiente (palabra/frase, inclusión o exclusión). Comparten el motor de búsqueda subyacente, pero cada una aporta un resultado útil de forma autónoma. |
| Negociable | ¿Cada historia explica qué necesita la persona y deja margen para discutir los detalles de la solución, respetando los acuerdos confirmados? | [Sí] | [Sí] |US-01, US-02 y US-03: Todas definen la intención de negocio y la capacidad requerida respetando los acuerdos del acta UC-21 v1.1 sin forzar aspectos de diseño o implementación técnica concreta.|
| Valiosa | ¿La parte «para…» de cada historia explica el beneficio que obtiene la persona al usar esa capacidad? | [Sí] | [Sí] | US-01, US-02 y US-03: Cada historia explicita un beneficio claro: US-01 facilita el hallazgo rápido, US-02 aprovecha ingredientes disponibles y US-03 garantiza la seguridad ante alergias o intolerancias. |
| Estimable | ¿Están claros el alcance y los datos necesarios para estimar el trabajo de cada historia? | [Sí] | [Sí] | US-01, US-02 y US-03: Al estar delimitadas por sus criterios de aceptación específicos y los Requisitos Funcionales del catálogo (FR-085, FR-086, FR-087), el equipo puede estimar su esfuerzo sin ambigüedades|
| Pequeña | ¿Se centra cada historia en una única capacidad de alcance manejable? | [Sí] | [Sí]| US-01, US-02 y US-03: La épica inicial se ha descompuesto adecuadamente en tres capacidades funcionales concretas. Ninguna representa una tarea técnica ni abarca múltiples pantallas.|
| Comprobable | ¿Los criterios de aceptación de cada historia describen acciones y resultados observables que permiten distinguir un comportamiento correcto de uno incorrecto? | [Sí] | [Sí] |US-01, US-02 y US-03: Todos los criterios están formalizados mediante el patrón Dado... cuando... entonces..., especificando inputs claros y comportamientos observables del sistema (incluyendo el caso especial FR-102).   |

## Dudas pendientes

[Cuestiones pendientes de aclaración. Si no quedan cuestiones, indicar «Ninguna».]
