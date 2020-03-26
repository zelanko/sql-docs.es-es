---
title: Generación de perfiles de datos y notificaciones de DQS
ms.date: 03/15/2020
ms.prod: sql
ms.reviewer: jroth
ms.technology: data-quality-services
ms.topic: conceptual
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e0bd9585a48ee30368d145c79f8431e922801a9c
ms.sourcegitcommit: c30a2def43c86860aeec69d3e3029f2296544b13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/25/2020
ms.locfileid: "80243405"
---
# <a name="data-profiling-and-notifications-in-data-quality-services-dqs"></a>Generación de perfiles de datos y notificaciones en Data Quality Services (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)](DQS) es un servicio de generación de perfiles de datos. DQS analiza los datos de un origen y muestra estadísticas sobre los datos de las actividades de DQS.

## <a name="attributes-goals-benefits"></a>Atributos, objetivos, ventajas

### <a name="attributes-of-dqs"></a>Atributos de DQS

La generación de perfiles de DQS tiene los siguientes atributos:

- Proporciona medidas automatizadas de calidad de los datos.
- Está integrado en los proyectos de calidad de datos y administración del conocimiento de DQS.
- Es dinámica y ajustable.

### <a name="goals-of-dqs"></a>Objetivos de DQS

La generación de perfiles con DQS tiene los dos objetivos principales siguientes:

- Para guiarle a través de los procesos de calidad de los datos y para apoyar sus decisiones.
- Evaluar la eficacia de los procesos.

### <a name="benefits-of-dqs"></a>Ventajas de DQS

La generación de perfiles de DQS tiene las siguientes ventajas:

- Proporciona una visión general de la calidad de los datos de origen y ayuda a identificar los problemas de calidad de los datos.

- Evalúa los procesos de calidad de los datos y guía:
  - Detección de conocimiento
  - Limpieza de datos
  - Directiva de coincidencia
  - Trabajo coincidente

- Presenta la información más relevante en el momento más relevante.

- Genera notificaciones que destacan las estadísticas o los eventos importantes que pueden justificar la acción. Las notificaciones de DQS suelen indicar una condición y recomendar una acción correctiva.

La generación de perfiles de DQS proporciona detección de conocimiento, limpieza de datos y coincidencia de datos. DQS es también herramienta de análisis de datos. Puede crear una base de conocimiento para su análisis. Después, puede ejecutar la detección de conocimiento mediante la base de conocimiento. La detección de conocimiento utiliza estadísticas de generación de perfiles para determinar si la base de conocimiento satisface sus necesidades de detección, limpieza y búsqueda de coincidencias.

## <a name="how-dqs-profiling-works"></a><a name="How"></a>Cómo funciona la generación de perfiles de DQS

La generación de perfiles de DQS no mide la calidad de la base de conocimiento. La generación de perfiles mide la calidad de los datos de origen. La generación de perfiles proporciona estadísticas que indican el efecto de los siguientes esfuerzos:

- La operación específica en administración del conocimiento.
- Un proyecto de calidad de datos en los datos de origen.

### <a name="activity-context"></a>Contexto de actividad

La generación de perfiles está siempre en el contexto de la actividad específica que se está realizando. Puede hacer clic en la pestaña generación de perfiles de una pantalla para mostrar los datos de generación de perfiles. Este clic no le lleva lejos de la fase de la actividad que está realizando. La tabla de generación de perfiles se rellena en tiempo real mientras se realiza el proceso. Por lo tanto, puede evaluar las tareas de calidad de los datos a medida que se realizan.

Puede determinar si los datos de origen tienen mejor calidad después de la limpieza o la eliminación de datos duplicados, y en qué grado.

### <a name="profiling-is-based-on-counts"></a>La generación de perfiles se basa en recuentos

Todos los números de generación de perfiles hacen referencia al recuento de aspectos de valores específicos. En muchos casos, los números hacen referencia al porcentaje del total. Las métricas de unicidad son una excepción. Las métricas de unicidad hacen referencia al número absoluto de valores, independientemente del recuento de aspectos de esos valores.

### <a name="knowledge-driven-solution"></a>Solución controlada por conocimiento

La generación de perfiles forma parte de la solución controlada por conocimiento de DQS. La generación de perfiles proporciona información sobre una base de conocimiento, coincidencia o proceso de limpieza de datos. La información se basa en la asignación entre los campos de origen de datos y los dominios de la base de conocimiento. La generación de perfiles solo se realiza una vez completada la asignación. No se realiza ninguna generación de perfiles durante la fase de asignación de cualquier actividad.

La generación de perfiles siempre está adjuntada a una actividad. El proceso de generación de perfiles se realiza en los datos _asignados_ a los dominios, no en los datos _de_ los dominios.

La generación de perfiles está integrada en los pasos y las actividades siguientes:

- Los pasos **detectar** y **administrar valores de dominio** de la actividad detección de conocimiento.

- Los pasos **limpiar** y **administrar y ver resultados** de la actividad limpieza.

- Los pasos **Directiva de coincidencia** y resultados de **búsqueda** de coincidencias de la actividad directiva de coincidencia.

- Los pasos de **coincidencia** y **exportación** de la actividad de búsqueda de coincidencias.

DQS no proporciona estadísticas sobre la generación de perfiles para la actividad Administración de dominios.

## <a name="profiling-data-by-activity"></a><a name="Activity"></a>Generar perfiles de datos por actividad

La generación de perfiles de DQS utiliza las siguientes dimensiones de calidad de datos estándar para representar la calidad de los datos:

- Integridad: la medida en la que están presentes los datos.
- Precisión: la medida en la que se pueden usar los datos para su uso previsto.
- Unicidad: la medida en la que distintos valores representan entidades diferentes.

De forma predeterminada, los valores NULL y vacíos se consideran ausentes o reducen el porcentaje de integridad. Sin embargo, puede definir otros valores equivalentes a NULL. También se considera que faltan estos valores.

La generación de perfiles le proporciona las estadísticas necesarias para evaluar los procesos, pero debe saber cómo interpretarlas. Para ello, examínelas columna por columna.

### <a name="differing-sets-of-profiling-statistics"></a>Diferentes conjuntos de estadísticas de generación de perfiles

Las actividades de DQS tienen conjuntos de estadísticas de generación de perfiles diferentes, de la manera siguiente:

- Solo la actividad Limpieza tiene estadísticas de generación de perfiles para la precisión (en porcentaje por dominio). La precisión se ve afectada por la validez, la coherencia, los errores de sintaxis y las reglas de dominio.

- Solo la actividad Limpieza dispone de estadísticas de generación de perfiles para los valores correctos, corregidos y sugeridos en el origen, y para los valores corregidos y sugeridos por dominio (ambos en número de porcentaje).

- Las actividades Detección de conocimiento y Limpieza tienen estadísticas de generación de perfiles para la validez (limpieza por registro, detección de conocimiento por registro y dominio). Las actividades de directiva de coincidencia y de coincidencia no tienen estadísticas para la validez.

- Se proporcionan estadísticas de generación de perfiles para la unicidad, para el origen y el dominio. Esta instrucción se aplica a las actividades siguientes:
  - Detección de conocimiento.
  - Directiva de coincidencia.
  - Coincidencia.
  - Pero _no_ para la actividad de limpieza.

DQS ofrece estadísticas de generación de perfiles específicas relacionadas con una actividad. Para obtener más información, vea las secciones de **generación de perfiles** en los temas siguientes:

- [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)

- [Limpiar datos mediante el conocimiento de&#41; interno de DQS &#40;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)

- [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)

## <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>Generación de perfiles de datos en la supervisión de actividades

La información de generación de perfiles está disponible no solo en las páginas de actividades de Data Quality Client, sino también en supervisión de actividades. La información se refiere a las actividades de detección de conocimiento, Directiva de coincidencia, coincidencia y limpieza. La información está disponible en las páginas de actividades de Data Quality Client y en supervisión de la actividad.

Puede ver todos los elementos siguientes en una ubicación:

- Propiedades
- Procesos de cálculo relacionados con las actividades
- Información de generación de perfiles generada para cada actividad

Seleccione una actividad en la tabla de actividades para mostrar los resultados de la generación de perfiles en la segunda tabla. También puede exportar los resultados de la generación de perfiles.

Para obtener más información, consulte [DQS Administration](../data-quality-services/dqs-administration.md).

## <a name="notifications"></a><a name="Notifications"></a>Notificaciones

DQS genera notificaciones para indicar cuándo es posible que desee realizar una acción basada en estadísticas de generación de perfiles. DQS utiliza notificaciones para los hechos importantes sobre el origen de datos. Estos hechos muestran la eficacia de la actividad actual en relación con el propósito para el que se ejecutó. Las notificaciones proporcionan sugerencias y recomendaciones que indican una condición. Las notificaciones también pueden recomendar cómo mejorar una actividad de detección de conocimiento, limpieza de datos o búsqueda de coincidencias de datos.

DQS envía una notificación cuando detecta un problema que podría interesarle. Como escenario de ejemplo, cuando la integridad y la precisión son tanto del 100%, la actividad de limpieza de datos podría no producir valores corregidos o sugeridos. DQS puede publicar una notificación para esa situación. Esta notificación indicaría que es posible que la actividad no sea necesaria. La ejecución de la actividad sigue siendo su decisión.

Una notificación se indica mediante una información sobre herramientas con un signo de exclamación, en la pestaña **generación de perfiles** . las estadísticas asociadas a la notificación están coloreadas en rojo para indicar la justificación estadística de la notificación.

### <a name="disable-notifications"></a>Deshabilitar notificaciones

Las notificaciones están habilitadas de forma predeterminada. Sin embargo, puede deshabilitar las notificaciones mediante el Data Quality Client Página principal. En la sección **Administración** , use la pestaña **Configuración general** .

Cuando se deshabilitan las notificaciones, no se muestran las sugerencias de herramientas y las estadísticas no se colorean en rojo. La generación de perfiles sigue siendo operativa mientras las notificaciones están deshabilitadas. No hay ninguna mejora en el rendimiento al deshabilitar las notificaciones.

Para conocer las condiciones específicas asociadas con las notificaciones para una actividad, vea los temas siguientes:

- [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)

- [Limpiar datos mediante el conocimiento de&#41; interno de DQS &#40;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)

- [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)

- [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)

## <a name="related-tasks"></a>Related Tasks

| Descripción de la tarea | Tema |
| :--------------- | :---- |
| Describe cómo habilitar o deshabilitar las notificaciones en DQS. | [Habilitar o deshabilitar notificaciones de generación de perfiles en DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md) |
|||
