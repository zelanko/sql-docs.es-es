---
title: "XML para conjuntos de filas de esquema de análisis | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0c44abd2ba4be59a86b46a9b0ff74196c570e5e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
  El proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for analysis (XMLA) incluye conjuntos de filas de esquema que devuelven metadatos sobre el estado, la actividad y los objetos de servidor. La recuperación de metadatos es necesaria si está desarrollando una aplicación cliente que se conecte a un modelo de Analysis Services cuyas estructura y características sean variables.  
  
 Los conjuntos de filas de esquema también proporcionan una visión general de los procesos y operaciones internos que pueden ayudarle a supervisar el servidor y solucionar problemas. Para admitir mejor las tareas administrativas ad hoc, puede ejecutar una consulta DMV (Vista de administración dinámica) en la mayoría de los conjuntos de filas de esquema. Las consultas DMV devuelven resultados en un formato tabular legible que puede ver en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 En la tabla siguiente se enumera y se describe cada conjunto de filas de esquema XMLA e identifica si devuelve información específica a los modelos tabulares.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Conjunto de filas<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[Conjunto de filas DISCOVER_CALC_DEPENDENCY](../../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|Devuelve información sobre las dependencias entre tablas, columnas, medidas y fórmulas de columnas calculadas.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos en los libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_CONNECTIONS](../../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_COMMAND_OBJECTS](../../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en los objetos que utiliza el comando al que se hace referencia.|  
|[Conjunto de filas DISCOVER_COMMANDS](../../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|Proporciona información sobre el uso de recursos y la actividad relacionados con los comandos que se están ejecutando actualmente o que se ejecutaron en último lugar en las conexiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_CSDL_METADATA](../../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|Devuelve una definición XML de un origen de datos a un cliente que puede consumir un tabular o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelar y presentar los datos de origen como parte de un informe.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos en los libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)|Devuelve una lista de los orígenes de datos del proveedor XML que están disponibles en el servidor o servicio web.|  
|[Conjunto de filas DISCOVER_DB_CONNECTIONS](../../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente desde el servidor a una base de datos.|  
|[Conjunto de filas DISCOVER_DIMENSION_STAT](../../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|Devuelve estadísticas sobre la dimensión especificada.|  
|[Conjunto de filas DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|Devuelve una lista de nombres, tipos de datos y valores de enumeración de enumeradores admitidos por el proveedor de XMLA para un origen de datos concreto.|  
|[Conjunto de filas DISCOVER_JOBS](../../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|Proporciona información sobre los trabajos activos que se ejecutan en el servidor.|  
|[Conjunto de filas DISCOVER_KEYWORDS &#40; XMLA &#41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|Devuelve información sobre las palabras clave reservadas por el proveedor XMLA.|  
|[Conjunto de filas DISCOVER_LITERALS](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|Devuelve información sobre los literales, incluidos los tipos de datos y valores, admitidos por el proveedor de XMLA.|  
|[Conjunto de filas DISCOVER_LOCATIONS](../../../analysis-services/schema-rowsets/xml/discover-locations-rowset.md)|Devuelve información sobre el contenido de un archivo de copia de seguridad.|  
|[Conjunto de filas DISCOVER_LOCKS](../../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|Proporciona información sobre los bloqueos pendientes actuales en el servidor.|  
|[Conjunto de filas DISCOVER_MEMORYGRANT](../../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|Devuelve una lista de concesiones de cuota de memoria interna utilizadas por los trabajos que se están ejecutando actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_MEMORYUSAGE](../../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|Devuelve las estadísticas de uso de memoria para diversos objetos asignados por el servidor.|  
|[Conjunto de filas DISCOVER_OBJECT_ACTIVITY](../../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|Proporciona el uso de recursos por objeto desde el inicio del servicio.|  
|[Conjunto de filas DISCOVER_OBJECT_MEMORY_USAGE](../../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|Proporciona información sobre los recursos de memoria utilizados por los objetos.|  
|[Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT](../../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|Devuelve estadísticas sobre la dimensión que está asociada a una partición.|  
|[Conjunto de filas DISCOVER_PARTITION_STAT](../../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|Devuelve estadísticas sobre agregaciones de una partición determinada.|  
|[Conjunto de filas DISCOVER_PERFORMANCE_COUNTERS](../../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|Devuelve el valor de uno o varios contadores de rendimiento especificados.|  
|[Conjunto de filas DISCOVER_PROPERTIES](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|Devuelve una lista de información y valores sobre las propiedades estándar y específicas del proveedor admitidas por el proveedor de XMLA para el origen de datos especificado.|  
|[Conjunto de filas DISCOVER_SCHEMA_ROWSETS](../../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|Devuelve los nombres, restricciones, descripción y otra información para todos los valores de enumeración y cualquier valor de enumeración específico del proveedor adicional admitidos por el proveedor XMLA.|  
|[Conjunto de filas DISCOVER_SESSIONS](../../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|Proporciona información sobre el uso de los recursos y la actividad en las sesiones abiertas actualmente en el servidor.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](../../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|Proporciona información en el nivel de columna y segmento acerca de las tablas de almacenamiento utilizado por una tabla o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] base de datos.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos en los libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMNS](../../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|Permite al cliente determinar la asignación de columnas a las tablas de almacenamiento utilizadas por una tabla o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] base de datos.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos en los libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_STORAGE_TABLES](../../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|Devuelve información acerca de las tablas usadas en un modelo.<br /><br /> Se aplica a los modelos tabulares implementados en una instancia de Analysis Services y [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos en los libros de Excel que se ejecutan en un entorno de SharePoint.|  
|[Conjunto de filas DISCOVER_TRACE_COLUMNS](../../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|Describe las columnas de seguimiento proporcionadas por el proveedor de seguimiento.|  
|[Conjunto de filas DISCOVER_TRACE_DEFINITION_PROVIDERINFO](../../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|Devuelve información básica sobre el proveedor de seguimiento, como su nombre y descripción.|  
|[Conjunto de filas DISCOVER_TRACE_EVENT_CATEGORIES](../../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|Describe las categorías de eventos proporcionadas por el proveedor de seguimiento.|  
|[Conjunto de filas DISCOVER_TRACES](../../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|Devuelve información sobre los seguimientos que se ejecutan en un servidor.|  
|[Conjunto de filas DISCOVER_TRANSACTIONS](../../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|Devuelve el conjunto actual de transacciones pendientes en el sistema.|  
|[Conjunto de filas DISCOVER_XML_METADATA](../../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)|Devuelve un documento XML que describe un objeto solicitado.|  
  
 <sup>1</sup> todos los conjuntos de filas de esquema enumerados aquí son compatibles con el proveedor de origen de datos MSOLAP para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con XMLA en Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Usar dinámica vistas de administración &#40; DMV &#41; para supervisar Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [Al recuperar los metadatos de un origen de datos analíticos](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  

