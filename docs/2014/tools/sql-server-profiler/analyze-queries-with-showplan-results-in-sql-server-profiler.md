---
title: Analizar consultas con resultados de SHOWPLAN en SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], Showplan
- Profiler [SQL Server Profiler], Showplan results
- SQL Server Profiler, Showplan results
ms.assetid: 6a2f7727-141c-4f59-8613-2e452bc78467
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0eb13d2997c9b2b29c85489f30a161a96f64c70c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211108"
---
# <a name="analyze-queries-with-showplan-results-in-sql-server-profiler"></a>Analizar consultas con resultados de SHOWPLAN en SQL Server Profiler
  Puede agregar clases de eventos Showplan a una definición de seguimiento que permitan que el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] recopile y muestre información del plan de consulta en el seguimiento. También es posible extraer los eventos Showplan de los otros eventos recopilados en el seguimiento y guardarlos en un archivo XML independiente.  
  
 La extracción de eventos Showplan del seguimiento puede hacerse de dos formas:  
  
-   En el momento de la configuración de seguimiento, mediante la pestaña **configuración de extracción de eventos** . tenga en cuenta que esta pestaña no aparece hasta que se selecciona uno de los eventos SHOWPLAN en la pestaña selección de **eventos** .  
  
-   Mediante la opción **Extraer eventos de SQL Server** del menú **Archivo** .  
  
-   Mediante la extracción y almacenamiento de eventos individuales al hacer clic con el botón derecho en un evento concreto y seleccionar **Extraer datos de evento**.  
  
## <a name="showplan-events"></a>Showplan (eventos)  
 Los eventos de seguimiento Showplan se enumeran y describen en la siguiente tabla:  
  
|Nombre del evento|Descripción|  
|----------------|-----------------|  
|**Estadísticas de rendimiento**|Indica la primera vez que se guarda en caché un plan de presentación compilado, cuándo se vuelve a compilar y cuándo se quita de la caché del plan. La columna **TextData** contiene el plan de presentación en formato XML. Para obtener más información, vea [Performance Statistics (clase de eventos)](../../relational-databases/event-classes/performance-statistics-event-class.md).|  
|**SHOWPLAN All**|Muestra el plan de consulta con detalles completos de la compilación de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecutada. Por ejemplo, puede mostrar listas de columnas y estimaciones de costes. Para más información, consulte [Showplan All Event Class](../../relational-databases/event-classes/showplan-all-event-class.md).|  
|**SHOWPLAN All para la compilación de consultas**|Tiene lugar cuando se compila o se vuelve a compilar una consulta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es el equivalente en tiempo de compilación del evento **Showplan All** . **SHOWPLAN All** tiene lugar cuando se ejecuta una consulta. **SHOWPLAN All for Query compile** se produce cuando se compila una consulta. Para más información, consulte [Showplan All for Query Compile Event Class](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md).|  
|**Perfil de SHOWPLAN Statistics**|Muestra el plan de consulta con detalles completos acerca del tiempo de ejecución de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que se está ejecutando, incluido el número real de filas que pasan por cada operación. Para más información, consulte [Showplan Statistics Profile Event Class](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md).|  
|**Texto del plan de presentación**|Muestra como datos binarios el árbol del plan de la consulta de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que se está ejecutando. Para más información, consulte [Showplan Text Event Class](../../relational-databases/event-classes/showplan-text-event-class.md).|  
|**Texto de SHOWPLAN (sin codificar)**|Muestra como texto el árbol del plan de consulta de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que se está ejecutando. Esta clase de evento muestra la misma información que Showplan Text, pero en formato de texto en lugar de datos binarios. Para obtener más información, vea [Showplan Text &#40;Unencoded&#41;, clase de eventos](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md).|  
|**SHOWPLAN XML**|Muestra el plan de consulta con los datos completos recopilados durante la optimización de la consulta. Este evento solo se genera al optimizar un plan de consulta. Para más información, consulte [Showplan XML Event Class](../../relational-databases/event-classes/showplan-xml-event-class.md).|  
|**SHOWPLAN XML for Query compilar**|Muestra el plan de consulta al compilar la consulta. Para más información, consulte [Showplan XML for Query Compile Event Class](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md).|  
|**Perfil de SHOWPLAN XML Statistics**|Muestra el plan de consulta con detalles completos acerca del tiempo de ejecución en formato XML. Por ejemplo, esta clase de evento captura el número de filas que pasan por cada operador de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que se está ejecutando. Para más información, consulte [Showplan XML Statistics Profile Event Class](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Rendimiento (categoría de eventos)](../../relational-databases/event-classes/performance-event-category.md)  
  
  
