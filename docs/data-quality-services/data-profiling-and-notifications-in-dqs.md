---
title: "Generación de perfiles de datos y notificaciones de DQS | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94e8301b0df36349494fbfc9e900957dee5e8852
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="data-profiling-and-notifications-in-dqs"></a>Generación de perfiles de datos y notificaciones de DQS
  La generación de perfiles de datos en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) es el proceso que consiste en analizar los datos de un origen de datos existente y mostrar estadísticas sobre ellos en actividades de DQS. Proporciona medidas automatizadas de la calidad de los datos. La generación de perfiles de DQS está integrada en los proyectos de calidad de datos y administración del conocimiento de DQS. Es dinámica y ajustable. La generación de perfiles tiene dos objetivos importantes: en primer lugar, guiarle a través de los procesos de calidad de datos y ayudarle a tomar decisiones, y en segundo lugar, evaluar la eficacia de los procesos. El proceso de generación de perfiles de DQS tiene las siguientes ventajas:  
  
-   La generación de perfiles proporciona una visión general de la calidad de los datos de origen, y le ayuda a identificar problemas relacionados con la calidad de los datos.  
  
-   La generación de perfiles evalúa la eficacia de los procesos de calidad de datos, sirviéndole de guía en las actividades de detección de conocimiento, limpieza de datos, directiva de coincidencia y búsqueda de coincidencias.  
  
-   La generación de perfiles le muestra la información más importante en el momento adecuado.  
  
-   El proceso de generación de perfiles genera notificaciones que destacan las estadísticas o los eventos importantes que pueden justificar la realización de una acción. En muchos casos, las notificaciones de DQS indicarán una condición y recomendarán la acción que puede realizar para remediarla.  
  
 La generación de perfiles le permite utilizar Data Quality Services no solo para la detección de conocimiento, la limpieza y la búsqueda de coincidencias, sino también como herramienta de análisis. Puede crear una base de conocimiento para el análisis, y ejecutar la detección de conocimiento utilizando dicha base de conocimiento para determinar, a partir de las estadísticas de la generación de perfiles, si esta satisface sus necesidades de detección, limpieza y búsqueda de coincidencias.  
  
##  <a name="How"></a> Cómo funciona la generación de perfiles  
 La generación de perfiles no mide la calidad de la base de conocimiento. Mide la calidad de los datos de origen. La generación de perfiles le proporciona estadísticas que indican el efecto de la operación específica que está realizando en la administración del conocimiento o en un proyecto de calidad de datos en los datos de origen. La generación de perfiles está siempre en el contexto de la actividad específica que se está realizando. Puede hacer clic en la pestaña de generación de perfiles de una pantalla para mostrar datos sobre la generación de perfiles sin abandonar la fase de la actividad que está realizando. La tabla de generación de perfiles se rellena en tiempo real mientras se realiza el proceso, permitiéndole evaluar las tareas de calidad de los datos al mismo tiempo que las lleva a cabo. Puede determinar si los datos de origen tienen mejor calidad después de la limpieza o la eliminación de datos duplicados, y en qué grado.  
  
 Todos los números procedentes de la generación de perfiles hacen referencia al número de repeticiones de un valor, y en muchos casos al porcentaje del total, a excepción de las métricas de unicidad. Las métricas de unicidad hacen referencia al número absoluto de valores, independientemente del número de repeticiones de estos.  
  
 La generación de perfiles forma parte de la solución controlada por conocimiento de DQS. Proporciona información sobre una base de conocimiento, la búsqueda de coincidencias o el proceso de limpieza de datos basándose en la asignación entre los campos del origen de datos y los dominios de la base de conocimiento. La generación de perfiles solo se realiza una vez finalizada la asignación; no se realiza ninguna tarea de este tipo durante la fase de asignación de las actividades. La generación de perfiles siempre está adjuntada a una actividad. El proceso de generación de perfiles se realiza en los datos asignados a los dominios, no en los datos de estos. La generación de perfiles está integrada en los pasos y las actividades siguientes:  
  
-   Los pasos **Detectar** y **Administrar valores del dominio** de la actividad Detección de conocimiento  
  
-   Los pasos **Limpieza** y **Administrar y ver resultados** de la actividad Limpieza  
  
-   Los pasos **Directiva de coincidencia** y **Resultados de búsqueda de coincidencias** de la actividad Directiva de coincidencia  
  
-   Los pasos **Coincidencia** y **Exportar** de la actividad Coincidencia  
  
 DQS no proporciona estadísticas sobre la generación de perfiles para la actividad Administración de dominios.  
  
##  <a name="Activity"></a> Generar perfiles de datos por actividad  
 La generación de perfiles de DQS utiliza dimensiones de calidad de datos estándar para representar la calidad de los datos: integridad (la medida en la que están presentes los datos), precisión (la medida en la que los datos se pueden utilizar para su uso previsto) y unicidad (la medida en la que distintos valores representan entidades diferentes). De forma predeterminada, los valores NULL y los valores vacíos se consideran como ausentes, por lo que reducen el porcentaje de integridad; sin embargo, también es posible definir otros valores equivalentes a NULL, en cuyo caso también se considerarán como ausentes.  
  
 La generación de perfiles le proporciona las estadísticas necesarias para evaluar los procesos, pero debe saber cómo interpretarlas. Para ello, examínelas columna por columna.  
  
 Las actividades de DQS tienen conjuntos de estadísticas de generación de perfiles diferentes, de la manera siguiente:  
  
-   Solo la actividad Limpieza tiene estadísticas de generación de perfiles para la precisión (en porcentaje por dominio). La precisión se ve afectada por la validez, la coherencia, los errores de sintaxis y las reglas de dominio.  
  
-   Solo la actividad Limpieza dispone de estadísticas de generación de perfiles para los valores correctos, corregidos y sugeridos en el origen, y para los valores corregidos y sugeridos por dominio (ambos en número de porcentaje).  
  
-   Las actividades Detección de conocimiento y Limpieza tienen estadísticas de generación de perfiles para la validez (limpieza por registro, detección de conocimiento por registro y dominio). Las actividades de directiva de coincidencia y de coincidencia no tienen estadísticas para la validez.  
  
-   La actividad Limpieza no dispone de estadísticas de generación de perfiles para la unicidad. Las actividades Detección de conocimiento, Directiva de coincidencia y Coincidencia tienen estadísticas de generación de perfiles para la unicidad tanto en número como en porcentaje para el origen y por dominio.  
  
 Para obtener más información sobre las estadísticas específicas de generación de perfiles relacionadas con una actividad, vea las secciones de generación de perfiles en los temas siguientes:  
  
-   [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="Monitoring"></a> Generar perfiles de datos en la supervisión de actividades  
 La información sobre la generación de perfiles para las actividades Detección de conocimiento, Directiva de coincidencia, Coincidencia y Limpieza no solo está disponible en las páginas de actividades de Data Quality Client, sino también en la supervisión de actividades. La supervisión de la actividad le proporciona información general sobre las actividades actuales y las anteriores. Además de las propiedades y los procesos de cálculo relacionados con las actividades, también puede ver la información sobre la generación de perfiles generada para cada actividad en una ubicación. Seleccione una actividad en la tabla de actividades para mostrar los resultados de la generación de perfiles en una tabla que aparecerá debajo. También puede exportar los resultados de la generación de perfiles. Para obtener más información, consulte [DQS Administration](../data-quality-services/dqs-administration.md).  
  
##  <a name="Notifications"></a> Notificaciones  
 Además de recopilar y mostrar estadísticas y métricas importantes mediante la generación de perfiles, DQS generará notificaciones (si están habilitadas) que le indicarán cuándo puede realizar una acción basándose en las estadísticas de generación de perfiles mostradas. DQS utiliza notificaciones para resaltar hechos importantes sobre el origen de datos, y para mostrar la eficacia de la actividad actual en relación con el propósito para el que se ha ejecutado. Las notificaciones proporcionan sugerencias y recomendaciones que indican una condición, y le sugieren cómo mejorar una actividad de detección de conocimiento, de limpieza de datos o de búsqueda de coincidencias de datos.  
  
 Las notificaciones de DQS se utilizan para plantear una cuestión que puede interesarle, o para solucionar un posible problema. Lo que haga con la información de la notificación dependerá de lo relevante que sea para sus propósitos. Por ejemplo, imagine que DQS envía una notificación cuando la limpieza de datos no genera ningún valor corregido ni sugerido, mientras la integridad y la precisión son del 100%. Esta notificación indicaría que es posible que no sea necesario ejecutar la actividad. No obstante, usted será el que decida si debe ejecutarse o no.  
  
 Las notificaciones se indican mediante una información sobre herramientas con un signo de exclamación en la pestaña **Generación de perfiles** . Las estadísticas asociadas con la notificación están coloreadas en rojo para indicar la justificación estadística para la notificación.  
  
 Puede habilitar (el valor predeterminado) o deshabilitar las notificaciones en la pestaña **Configuración general** de la sección **Administración** de la página de inicio de Data Quality Client. Si se deshabilitan las notificaciones, la información sobre herramientas no se muestra y las estadísticas no se colorean en rojo. El hecho de deshabilitar de las notificaciones no conlleva ninguna mejora significativa del rendimiento. La generación de perfiles seguirá siendo operativa aunque se deshabiliten las notificaciones.  
  
 Para conocer las condiciones específicas asociadas con las notificaciones para una actividad, vea los temas siguientes:  
  
-   [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo habilitar o deshabilitar las notificaciones en DQS.|[Habilitar o deshabilitar notificaciones de generación de perfiles en DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  
