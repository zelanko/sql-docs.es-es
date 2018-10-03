---
title: XML para conjuntos de filas de esquema de análisis | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50f95f4049d03c8d822c3e56ba5ff235705bf4de
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121185"
---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
  El proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for analysis (XMLA) incluye conjuntos de filas de esquema que devuelven metadatos sobre el estado, la actividad y los objetos de servidor. La recuperación de metadatos es necesaria si está desarrollando una aplicación cliente que se conecte a un modelo de Analysis Services cuyas estructura y características sean variables.  
  
 Los conjuntos de filas de esquema también proporcionan una visión general de los procesos y operaciones internos que pueden ayudarle a supervisar el servidor y solucionar problemas. Para admitir mejor las tareas administrativas ad hoc, puede ejecutar una consulta DMV (Vista de administración dinámica) en la mayoría de los conjuntos de filas de esquema. Las consultas DMV devuelven resultados en un formato tabular legible que puede ver en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 En la tabla siguiente se enumera y se describe cada conjunto de filas de esquema XMLA e identifica si devuelve información específica a los modelos tabulares.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Rowset<sup>1</sup>|Descripción|  
|------------------------|-----------------|  
|[Conjunto de filas DISCOVER_CALC_DEPENDENCY](discover-calc-dependency-rowset.md)|Devuelve información sobre las dependencias entre tablas, columnas, medidas y fórmulas de columnas calculadas.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y los modelos de PowerPivot de libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_CONNECTIONS](discover-connections-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_COMMAND_OBJECTS](discover-command-objects-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en los objetos que utiliza el comando al que se hace referencia.|  
|[Conjunto de filas DISCOVER_COMMANDS](discover-commands-rowset.md)|Proporciona información sobre el uso de recursos y la actividad relacionados con los comandos que se están ejecutando actualmente o que se ejecutaron en último lugar en las conexiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_CSDL_METADATA](discover-csdl-metadata-rowset.md)|Devuelve una definición XML de un origen de datos a un cliente que puede utilizar un modelo tabular o de PowerPivot y presenta el origen de datos como parte de un informe.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y los modelos de PowerPivot de libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_DATASOURCES](discover-datasources-rowset.md)|Devuelve una lista de los orígenes de datos del proveedor XML que están disponibles en el servidor o servicio web.|  
|[Conjunto de filas DISCOVER_DB_CONNECTIONS](discover-db-connections-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente desde el servidor a una base de datos.|  
|[Conjunto de filas DISCOVER_DIMENSION_STAT](discover-dimension-stat-rowset.md)|Devuelve estadísticas sobre la dimensión especificada.|  
|[Conjunto de filas DISCOVER_ENUMERATORS](discover-enumerators-rowset.md)|Devuelve una lista de nombres, tipos de datos y valores de enumeración de enumeradores admitidos por el proveedor de XMLA para un origen de datos concreto.|  
|[Conjunto de filas DISCOVER_JOBS](discover-jobs-rowset.md)|Proporciona información sobre los trabajos activos que se ejecutan en el servidor.|  
|[Conjunto de filas DISCOVER_KEYWORDS &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)|Devuelve información sobre las palabras clave reservadas por el proveedor XMLA.|  
|[Conjunto de filas DISCOVER_LITERALS](discover-literals-rowset.md)|Devuelve información sobre los literales, incluidos los tipos de datos y valores, admitidos por el proveedor de XMLA.|  
|[Conjunto de filas DISCOVER_LOCATIONS](discover-locations-rowset.md)|Devuelve información sobre el contenido de un archivo de copia de seguridad.|  
|[Conjunto de filas DISCOVER_LOCKS](discover-locks-rowset.md)|Proporciona información sobre los bloqueos pendientes actuales en el servidor.|  
|[Conjunto de filas DISCOVER_MEMORYGRANT](discover-memorygrant-rowset.md)|Devuelve una lista de concesiones de cuota de memoria interna utilizadas por los trabajos que se están ejecutando actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_MEMORYUSAGE](discover-memoryusage-rowset.md)|Devuelve las estadísticas de uso de memoria para diversos objetos asignados por el servidor.|  
|[Conjunto de filas DISCOVER_OBJECT_ACTIVITY](discover-object-activity-rowset.md)|Proporciona el uso de recursos por objeto desde el inicio del servicio.|  
|[Conjunto de filas DISCOVER_OBJECT_MEMORY_USAGE](discover-object-memory-usage-rowset.md)|Proporciona información sobre los recursos de memoria utilizados por los objetos.|  
|[Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT](discover-partition-dimension-stat-rowset.md)|Devuelve estadísticas sobre la dimensión que está asociada a una partición.|  
|[Conjunto de filas DISCOVER_PARTITION_STAT](discover-partition-stat-rowset.md)|Devuelve estadísticas sobre agregaciones de una partición determinada.|  
|[Conjunto de filas DISCOVER_PERFORMANCE_COUNTERS](discover-performance-counters-rowset.md)|Devuelve el valor de uno o varios contadores de rendimiento especificados.|  
|[Conjunto de filas DISCOVER_PROPERTIES](discover-properties-rowset.md)|Devuelve una lista de información y valores sobre las propiedades estándar y específicas del proveedor admitidas por el proveedor de XMLA para el origen de datos especificado.|  
|[Conjunto de filas DISCOVER_SCHEMA_ROWSETS](discover-schema-rowsets-rowset.md)|Devuelve los nombres, restricciones, descripción y otra información para todos los valores de enumeración y cualquier valor de enumeración específico del proveedor adicional admitidos por el proveedor XMLA.|  
|[Conjunto de filas DISCOVER_SESSIONS](discover-sessions-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las sesiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](discover-storage-table-column-segments-rowset.md)|Proporciona información en el nivel de columna y de sector acerca de las tablas de almacenamiento utilizadas por una base de datos tabular o de PowerPivot.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y los modelos de PowerPivot de libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMNS](discover-storage-table-columns-rowset.md)|Permite al cliente determinar la asignación de columnas a las tablas de almacenamiento utilizadas por una base de datos tabular o de PowerPivot.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y los modelos de PowerPivot de libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLES](discover-storage-tables-rowset.md)|Devuelve información acerca de las tablas usadas en un modelo.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y los modelos de PowerPivot de libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_TRACE_COLUMNS](discover-trace-columns-rowset.md)|Describe las columnas de seguimiento proporcionadas por el proveedor de seguimiento.|  
|[Conjunto de filas DISCOVER_TRACE_DEFINITION_PROVIDERINFO](discover-trace-definition-providerinfo-rowset.md)|Devuelve información básica sobre el proveedor de seguimiento, como su nombre y descripción.|  
|[Conjunto de filas DISCOVER_TRACE_EVENT_CATEGORIES](discover-trace-event-categories-rowset.md)|Describe las categorías de eventos proporcionadas por el proveedor de seguimiento.|  
|[Conjunto de filas DISCOVER_TRACES](discover-traces-rowset.md)|Devuelve información sobre los seguimientos que se ejecutan en un servidor.|  
|[Conjunto de filas DISCOVER_TRANSACTIONS](discover-transactions-rowset.md)|Devuelve el conjunto actual de transacciones pendientes en el sistema.|  
|[Conjunto de filas DISCOVER_XML_METADATA](discover-xml-metadata-rowset.md)|Devuelve un documento XML que describe un objeto solicitado.|  
  
 <sup>1</sup> todos los conjuntos de filas de esquema enumerados aquí son compatibles con el proveedor de origen de datos MSOLAP para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con XMLA en Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Usar vistas de administración dinámica &#40;DMV&#41; supervisar Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [Recuperación de metadatos de un origen de datos analíticos](../../multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
