---
title: Generación de perfiles de datos y notificaciones de DQS
ms.date: 04/01/2020
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 1e5c51996ba85b9645650f453a0e4ed18478ccf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "80607821"
---
# <a name="data-profiling-and-notifications-in-dqs"></a>Generación de perfiles de datos y notificaciones de DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La generación de perfiles de datos en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) es el proceso que consiste en analizar los datos de un origen de datos existente y mostrar estadísticas sobre ellos en actividades de DQS. Proporciona medidas automatizadas de la calidad de los datos. La generación de perfiles de DQS está integrada en los proyectos de calidad de datos y administración del conocimiento de DQS. es dinámica y ajustable. La generación de perfiles tiene dos objetivos importantes: en primer lugar, guiarle a través de los procesos de calidad de datos y ayudarle a tomar decisiones, y en segundo lugar, evaluar la eficacia de los procesos. El proceso de generación de perfiles de DQS tiene las siguientes ventajas:  
  
-   La generación de perfiles proporciona una visión general de la calidad de los datos de origen, y le ayuda a identificar problemas relacionados con la calidad de los datos.  
  
-   La generación de perfiles evalúa la eficacia de los procesos de calidad de datos, sirviéndole de guía en las actividades de detección de conocimiento, limpieza de datos, directiva de coincidencia y búsqueda de coincidencias.  
  
-   La generación de perfiles le muestra la información más importante en el momento adecuado.  
  
-   El proceso de generación de perfiles genera notificaciones que destacan las estadísticas o los eventos importantes que pueden merecer la acción. En muchos casos, las notificaciones de DQS indicarán una condición y recomendarán la acción que puede realizar para remediarla.  
  
 La generación de perfiles le permite utilizar Data Quality Services no solo para la detección de conocimiento, la limpieza y la búsqueda de coincidencias, sino también como herramienta de análisis. Puede crear una base de conocimiento para el análisis, y ejecutar la detección de conocimiento utilizando dicha base de conocimiento para determinar, a partir de las estadísticas de la generación de perfiles, si esta satisface sus necesidades de detección, limpieza y búsqueda de coincidencias.  
  
##  <a name="how-profiling-works"></a><a name="How"></a>Cómo funciona la generación de perfiles  
 La generación de perfiles no mide la calidad de la base de conocimiento. Mide la calidad de los datos de origen. La generación de perfiles proporciona estadísticas que indican el efecto de la operación específica que está realizando en la administración del conocimiento o en un proyecto de calidad de datos en los datos de origen. La generación de perfiles siempre está en el contexto de la actividad específica que se está realizando. Puede hacer clic en la pestaña generación de perfiles de una pantalla para mostrar los datos de generación de perfiles sin mantener la fase de la actividad que está realizando. La tabla de generación de perfiles se rellena en tiempo real a medida que se realiza el proceso, lo que le permite evaluar las tareas de calidad de los datos a medida que las está haciendo. Puede determinar si los datos de origen tienen mejor calidad después de la limpieza o la eliminación de datos duplicados, y en qué grado.  
  
 Todos los números de generación de perfiles hacen referencia al número de apariciones de un valor y, en muchos casos, hacen referencia al porcentaje del total, con la excepción de las métricas de unicidad. Las métricas de unicidad hacen referencia al número absoluto de valores, independientemente del número de repeticiones de estos.  
  
 La generación de perfiles forma parte de la solución controlada por conocimiento de DQS. Proporciona información sobre una base de conocimiento, la búsqueda de coincidencias o el proceso de limpieza de datos basándose en la asignación entre los campos del origen de datos y los dominios de la base de conocimiento. El perfil solo se realiza una vez completada la asignación; no se realiza ninguna generación de perfiles durante la fase de asignación de cualquier actividad. La generación de perfiles siempre está adjuntada a una actividad. El proceso de generación de perfiles se realiza en los datos asignados a los dominios, no en los datos de los dominios. Se integra en los siguientes pasos de las actividades:  
  
-   Los pasos **Detectar** y **Administrar valores del dominio** de la actividad Detección de conocimiento  
  
-   Los pasos **Limpieza** y **Administrar y ver resultados** de la actividad Limpieza  
  
-   Los pasos **Directiva de coincidencia** y **Resultados de búsqueda de coincidencias** de la actividad Directiva de coincidencia  
  
-   Los pasos **Coincidencia** y **Exportar** de la actividad Coincidencia  
  
 DQS no proporciona estadísticas de generación de perfiles para la actividad de administración de dominios.  
  
##  <a name="profiling-data-by-activity"></a><a name="Activity"></a> Generar perfiles de datos por actividad  
 La generación de perfiles de DQS utiliza dimensiones de calidad de datos estándar para representar la calidad de los datos: integridad (la medida en la que están presentes los datos), precisión (la medida en la que los datos se pueden utilizar para su uso previsto) y unicidad (la medida en la que distintos valores representan entidades diferentes). De forma predeterminada, se considera que los valores NULOs y vacíos están ausentes o menos el porcentaje de integridad; sin embargo, también puede definir otros valores equivalentes a NULL, en cuyo caso también se considerarán ausentes.  
  
 La generación de perfiles le proporciona las estadísticas necesarias para evaluar los procesos, pero debe saber cómo interpretarlas. Para ello, examínelas columna por columna.  
  
 Las actividades de DQS tienen conjuntos de estadísticas de generación de perfiles diferentes, de la manera siguiente:  
  
-   Solo la actividad Limpieza tiene estadísticas de generación de perfiles para la precisión (en porcentaje por dominio). La precisión se ve afectada por la validez, la coherencia, los errores de sintaxis y las reglas de dominio.  
  
-   Solo la actividad Limpieza dispone de estadísticas de generación de perfiles para los valores correctos, corregidos y sugeridos en el origen, y para los valores corregidos y sugeridos por dominio (ambos en número de porcentaje).  
  
-   Las actividades Detección de conocimiento y Limpieza tienen estadísticas de generación de perfiles para la validez (limpieza por registro, detección de conocimiento por registro y dominio). La Directiva de coincidencia y las actividades de coincidencia no tienen estadísticas para la validez.  
  
-   La actividad de limpieza no tiene estadísticas de generación de perfiles para la unicidad. Las actividades Detección de conocimiento, Directiva de coincidencia y Coincidencia tienen estadísticas de generación de perfiles para la unicidad tanto en número como en porcentaje para el origen y por dominio.  
  
 Para obtener más información sobre las estadísticas de generación de perfiles específicas relacionadas con una actividad, vea las secciones de generación de perfiles en los artículos siguientes:  
  
-   [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="profiling-data-in-activity-monitoring"></a><a name="Monitoring"></a>Generación de perfiles de datos en la supervisión de actividades  
 La información de generación de perfiles para las actividades detección de conocimiento, Directiva de coincidencia, coincidencia y limpieza está disponible no solo en las páginas de actividades de Data Quality Client, sino que también está disponible en supervisión de actividades. La supervisión de la actividad le proporciona información general sobre las actividades actuales y las anteriores. Además de las propiedades y los procesos de cálculo relacionados con las actividades, también puede ver la información sobre la generación de perfiles generada para cada actividad en una ubicación. Seleccione una actividad en la tabla de actividades para mostrar los resultados de la generación de perfiles en una tabla que aparecerá debajo. También puede exportar los resultados de la generación de perfiles. Para obtener más información, consulte [DQS Administration](../data-quality-services/dqs-administration.md).  
  
##  <a name="notifications"></a><a name="Notifications"></a>Notificaciones  
 Además de recopilar y mostrar estadísticas y métricas importantes mediante la generación de perfiles, DQS generará notificaciones (si están habilitadas) que le indicarán cuándo puede realizar una acción basándose en las estadísticas de generación de perfiles mostradas. DQS utiliza notificaciones para resaltar hechos importantes sobre el origen de datos y para mostrar la eficacia de la actividad actual en comparación con el propósito para el que se ejecutó. Las notificaciones proporcionan sugerencias y recomendaciones que indican una condición, y le sugieren cómo mejorar una actividad de detección de conocimiento, de limpieza de datos o de búsqueda de coincidencias de datos.  
  
 Las notificaciones de DQS se utilizan para plantear una cuestión que puede interesarle, o para solucionar un posible problema. El hecho de que se actúe sobre la notificación dependerá de si es relevante para sus propósitos. Por ejemplo, imagine que DQS envía una notificación cuando la limpieza de datos no genera ningún valor corregido ni sugerido, mientras la integridad y la precisión son del 100%. Esta notificación indicaría que es posible que no sea necesario ejecutar la actividad. No obstante, usted será el que decida si debe ejecutarse o no.  
  
 Las notificaciones se indican mediante una información sobre herramientas con un signo de exclamación en la pestaña **generación de perfiles** . las estadísticas asociadas a la notificación están coloreadas en rojo para indicar la justificación estadística de la notificación.  
  
 Puede habilitar (el valor predeterminado) o deshabilitar las notificaciones en la pestaña **Configuración general** de la sección **Administración** de la página de inicio de Data Quality Client. Cuando se deshabilita la notificación, no se muestran las sugerencias de herramientas y las estadísticas no se colorean en rojo. No hay ninguna mejora significativa en el rendimiento al deshabilitar las notificaciones. La generación de perfiles seguirá siendo operativa aunque se deshabiliten las notificaciones.  
  
 Para ver las condiciones específicas asociadas con las notificaciones de una actividad, consulte los siguientes artículos:  
  
-   [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Artículo|  
|----------------------|-----------|  
|Describe cómo habilitar o deshabilitar las notificaciones en DQS.|[Habilitar o deshabilitar notificaciones de generación de perfiles en DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
