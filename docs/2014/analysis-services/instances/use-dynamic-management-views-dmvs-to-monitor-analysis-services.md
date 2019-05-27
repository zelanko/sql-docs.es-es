---
title: Usar vistas de administración dinámica (DMV) para supervisar Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 22b82b2d-867f-4ebf-9288-79d1cdd62f18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a02d8d5b113e4773aa7cdfbbf20975fd70218e1a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079582"
---
# <a name="use-dynamic-management-views-dmvs-to-monitor-analysis-services"></a>Usar vistas de administración dinámica (DMV) para supervisar Analysis Services
  Las vistas de administración dinámica (DMV) de Analysis Services son estructuras de consulta que exponen información sobre las operaciones del servidor local y el estado del servidor. La estructura de consulta es una interfaz para los conjuntos de filas de esquema que devuelven metadatos y la información de supervisión acerca de una instancia de Analysis Services.  
  
 En la mayor parte de las consultas DMV, se usa una instrucción `SELECT` y el esquema `$System` con un conjunto de filas de esquema XML/A.  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 Las consultas DMV devuelven información sobre el estado del servidor actual en el momento en que se ejecutó la consulta. Para supervisar las operaciones en tiempo real, utilice el seguimiento en su lugar. Para más información, consulte [Use SQL Server Profiler to Monitor Analysis Services](use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Ventajas del uso de las consultas DMV](#bkmk_ben)  
  
 [Ejemplos y escenarios](#bkmk_ex)  
  
 [Sintaxis de las consultas](#bkmk_syn)  
  
 [Herramientas y permisos](#bkmk_tools)  
  
 [Referencia de DMV](#bkmk_ref)  
  
##  <a name="bkmk_ben"></a> Ventajas del uso de las consultas DMV  
 Las consultas DMV devuelven información acerca de las operaciones y el consumo de recursos que no están directamente disponibles a través de otros medios.  
  
 Las consultas DMV son una alternativa a la ejecución de comandos de detección XML/A. Para la mayoría de los administradores, escribir una consulta DMV es más sencillo porque la sintaxis de la consulta se basa en SQL. Además, el conjunto de resultados se devuelve en formato tabular que es más fácil de leer y de copiar.  
  
##  <a name="bkmk_ex"></a> Ejemplos y escenarios  
 Una consulta DMV puede ayudarle a responder preguntas sobre las sesiones activas y las conexiones, y qué objetos están utilizando la mayoría de la CPU o de la memoria en un momento concreto. En esta sección se proporcionan ejemplos de escenarios en los que las consultas DMV se usan con más frecuencia. También puede revisar la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409) para consultar las características adicionales sobre cómo usar las consultas DMV para supervisar una instancia de servidor.  
  
 `Select * from $System.discover_object_activity` /** Esta consulta informa de la actividad de los objetos desde que el servicio se ha iniciado por última vez. Para ver consultas de ejemplo basadas en esta DMV, vea [Nuevo System.Discover_Object_Activity](https://go.microsoft.com/fwlink/?linkid=221322)(Nuevo System.Discover_Object_Activity).  
  
 `Select * from $System.discover_object_memory_usage` /** Esta consulta informa del consumo de memoria de cada objeto.  
  
 `Select * from $System.discover_sessions` /** Esta consulta informa de las sesiones activas, incluido el usuario de la sesión y la duración.  
  
 `Select * from $System.discover_locks` /** Esta consulta devuelve una instantánea de los bloqueos usados en un momento específico.  
  
##  <a name="bkmk_syn"></a> Sintaxis de las consultas  
 El motor de consultas para las DMV es el analizador de minería de datos. La sintaxis de consulta DMV se basa en la instrucción [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
 Aunque la sintaxis de las consultas DMV se basan en una instrucción SQL SELECT, no admite la sintaxis completa de una instrucción SELECT. Fundamentalmente, no se admiten JOIN, GROUP BY, LIKE, CAST ni CONVERT.  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
 El siguiente ejemplo de DISCOVER_CALC_DEPENDENCY muestra el uso de la cláusula WHERE para proporcionar un parámetro a la consulta:  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
 O bien, para los conjuntos de filas de esquema que tienen restricciones, la consulta debe incluir la función SYSTEMRESTRICTSCHEMA. El ejemplo siguiente devuelve los metadatos CSDL sobre los modelos tabulares que se ejecutan en un servidor en modo tabular. Observe que CATALOG_NAME distingue entre mayúsculas y minúsculas:  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  
  
##  <a name="bkmk_tools"></a> Herramientas y permisos  
 Debe tener permisos de administrador del sistema en la instancia de Analysis Services para consultar una DMV.  
  
 Puede usar cualquier aplicación cliente que admita consultas DMX o MDX, incluidos SQL Server Management Studio, un informe de Reporting Services o un panel de PerformancePoint.  
  
 Para ejecutar una consulta de DMV Management Studio, conéctese a la instancia que desea consultar y haga clic en **Nueva consulta**. Puede ejecutar una consulta desde una ventana de consulta DMX o MDX.  
  
##  <a name="bkmk_ref"></a> Referencia de DMV  
 No todos los conjuntos de filas de esquema tienen una interfaz DMV. Para obtener una lista de todos los conjuntos de filas de esquema que se pueden consultar mediante DMV, ejecute la consulta siguiente.  
  
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
> [!NOTE]  
>  Si una DMV no está disponible para un conjunto de filas determinado, el servidor devuelve el error siguiente: "El \<schemarowset > el servidor no reconoció el tipo de solicitud". El resto de los errores indica problemas con la sintaxis.  
  
|Conjunto de filas|Descripción|  
|------------|-----------------|  
|[Conjunto de filas DBSCHEMA_CATALOGS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-catalogs-rowset)|Devuelve una lista de bases de datos de Analysis Services en la conexión actual.|  
|[Conjunto de filas DBSCHEMA_COLUMNS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-columns-rowset)|Devuelve una lista de todas las columnas en la base de datos actual. Puede usar esta lista para generar una consulta DMV.|  
|[Conjunto de filas DBSCHEMA_PROVIDER_TYPES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-provider-types-rowset)|Devuelve las propiedades de los tipos de datos base admitidos por el proveedor de datos OLE DB.|  
|[Conjunto de filas DBSCHEMA_TABLES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-tables-rowset)|Devuelve una lista de todas las tablas en la base de datos actual. Puede usar esta lista para generar una consulta DMV.|  
|[DISCOVER_CALC_DEPENDENCY, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset)|Devuelve una lista de las columnas y las tablas usadas en un modelo que tienen dependencias en otras columnas y tablas.|  
|[DISCOVER_COMMAND_OBJECTS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-command-objects-rowset)|Proporciona información sobre el uso de los recursos y la actividad en los objetos que utiliza el comando al que se hace referencia.|  
|[DISCOVER_COMMANDS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-commands-rowset)|Proporciona información de la actividad y el uso de los recursos acerca del comando que se ejecuta actualmente.|  
|[DISCOVER_CONNECTIONS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-connections-rowset)|Proporciona información de la actividad y el uso de los recursos acerca de las conexiones abiertas para Analysis Services.|  
|[Conjunto de filas DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)|Devuelve información sobre un modelo tabular.<br /><br /> Requiere la adición de SYSTEMRESTRICTSCHEMA y parámetros adicionales.|  
|[DISCOVER_DB_CONNECTIONS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-db-connections-rowset)|Proporciona información de la actividad y el uso de los recursos acerca de las conexiones abiertas desde Analysis Services a orígenes de datos externos, por ejemplo, durante el procesamiento o la importación.|  
|[Conjunto de filas DISCOVER_DIMENSION_STAT](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-dimension-stat-rowset)|Devuelve los atributos de una dimensión o las columnas de una tabla, según el tipo de modelo.|  
|[Conjunto de filas DISCOVER_ENUMERATORS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-enumerators-rowset)|Devuelve los metadatos sobre los enumeradores admitidos para un origen de datos concreto.|  
|[Conjunto de filas DISCOVER_INSTANCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/discover-instances-rowset)|Devuelve información relacionada con la instancia especificada.<br /><br /> Requiere la adición de SYSTEMRESTRICTSCHEMA y parámetros adicionales.|  
|[DISCOVER_JOBS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-jobs-rowset)|Devuelve información acerca de los trabajos actuales.|  
|[Conjunto de filas DISCOVER_KEYWORDS &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-keywords-rowset-xmla)|Devuelve la lista de palabras clave reservadas.|  
|[Conjunto de filas DISCOVER_LITERALS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-literals-rowset)|Devuelve la lista de literales, incluidos los tipos de datos y valores, admitidos por el proveedor de XMLA.|  
|[DISCOVER_LOCKS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-locks-rowset)|Devuelve una instantánea de los bloqueos utilizados en un momento concreto.|  
|[Conjunto de filas DISCOVER_MEMORYGRANT](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-memorygrant-rowset)|Devuelve información acerca de la memoria asignada por Analysis Services en el inicio.|  
|[Conjunto de filas DISCOVER_MEMORYUSAGE](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-memoryusage-rowset)|Muestra el uso de memoria de objetos específicos.|  
|[DISCOVER_OBJECT_ACTIVITY, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-object-activity-rowset)|Informa de la actividad de los objetos desde que el servicio se inició por última vez.|  
|[DISCOVER_OBJECT_MEMORY_USAGE, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-object-memory-usage-rowset)|Informes del consumo de memoria del objeto.|  
|[Conjunto de filas DISCOVER_PARTITION_DIMENSION_STAT](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-partition-dimension-stat-rowset)|Proporciona información sobre los atributos de una dimensión.<br /><br /> Requiere la adición de SYSTEMRESTRICTSCHEMA y parámetros adicionales.|  
|[Conjunto de filas DISCOVER_PARTITION_STAT](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-partition-stat-rowset)|Proporciona información sobre las particiones de una dimensión, una tabla o un grupo de medida.<br /><br /> Requiere la adición de SYSTEMRESTRICTSCHEMA y parámetros adicionales.|  
|[Conjunto de filas DISCOVER_PERFORMANCE_COUNTERS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-performance-counters-rowset)|Muestra las columnas usadas en un contador de rendimiento.<br /><br /> Requiere la adición de SYSTEMRESTRICTSCHEMA y parámetros adicionales.|  
|[Conjunto de filas DISCOVER_PROPERTIES](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-properties-rowset)|Devuelve información sobre las propiedades admitidas por XMLA para el origen de datos especificado.|  
|[Conjunto de filas DISCOVER_SCHEMA_ROWSETS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-schema-rowsets-rowset)|Devuelve nombres, restricciones, la descripción y otra información para todos los valores de enumeración admitidos por XMLA.|  
|[DISCOVER_SESSIONS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-sessions-rowset)|Informa de las sesiones activas, incluido el usuario de la sesión y la duración.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-table-column-segments-rowset)|Proporciona información en el nivel de columna y segmento acerca de las tablas de almacenamiento que usa una base de datos de Analysis Services que se ejecuta en modo Tabular o de SharePoint.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-table-columns-rowset)|Permite al cliente determinar la asignación de columnas a las tablas de almacenamiento que usa una base de datos de Analysis Services que se ejecuta en modo Tabular o de SharePoint.|  
|[DISCOVER_STORAGE_TABLES, conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-tables-rowset)|Devuelve información sobre las tablas usadas para el almacenamiento de modelos en una base de datos del modelo Tabular.|  
|[Conjunto de filas DISCOVER_TRACE_COLUMNS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-columns-rowset)|Devuelve una descripción XML de las columnas disponibles en un seguimiento.|  
|[Conjunto de filas DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset)|Devuelve el nombre y la información de versión del proveedor.|  
|[Conjunto de filas DISCOVER_TRACE_EVENT_CATEGORIES](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-event-categories-rowset)|Devuelve una lista de las categorías disponibles.|  
|[Conjunto de filas DISCOVER_TRACES](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-traces-rowset)|Devuelve una lista de los seguimientos que se ejecutan activamente en la conexión actual.|  
|[Conjunto de filas DISCOVER_TRANSACTIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-transactions-rowset)|Devuelve una lista de las transacciones que se ejecutan activamente en la conexión actual.|  
|[Conjunto de filas DISCOVER_XEVENT_TRACE_DEFINITION](../dev-guide/discover-xevent-trace-definition-rowset.md)|Devuelve una lista de los seguimientos xevent que se ejecutan activamente en la conexión actual.|  
|[Conjunto de filas DMSCHEMA_MINING_COLUMNS](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-columns-rowset)|Muestra las columnas individuales de todos los modelos de minería de datos disponibles en la conexión actual.|  
|[Conjunto de filas DMSCHEMA_MINING_FUNCTIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-functions-rowset)|Devuelve una lista de las funciones admitidas por los algoritmos de minería de datos del servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)|Devuelve un conjunto de filas que consta de las columnas que describen el modelo actual.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|Devuelve un conjunto de filas que consta de las columnas que describen el modelo actual en el formato PMML.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_XML](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset)|Devuelve un conjunto de filas que consta de las columnas que describen el modelo actual en el formato PMML.|  
|[Conjunto de filas DMSCHEMA_MINING_MODELS](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-models-rowset)|Devuelve una lista de modelos de minería de datos en la base de datos actual.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset)|Devuelve una lista de los parámetros de los algoritmos en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)|Proporciona una lista de los algoritmos de minería de datos disponibles en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset)|Devuelve una lista de todas las columnas de todos los modelos de minería de datos disponibles en la conexión actual.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-structures-rowset)|Enumera las estructuras de minería de datos disponibles en la conexión actual.|  
|[Conjunto de filas MDSCHEMA_CUBES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-cubes-rowset)|Devuelve información sobre los cubos que están definidos en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_DIMENSIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset)|Devuelve información sobre las dimensiones que están definidas en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_FUNCTIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-functions-rowset)|Devuelve una lista de las funciones que están disponibles para las aplicaciones cliente conectadas a la base de datos.|  
|[Conjunto de filas MDSCHEMA_HIERARCHIES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset)|Devuelve información sobre las jerarquías que están definidas en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_INPUT_DATASOURCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset)|Devuelve información sobre los objetos de origen de datos que están definidos en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_KPIS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-kpis-rowset)|Devuelve información sobre las KPI que están definidas en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_LEVELS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-levels-rowset)|Devuelve información acerca de los niveles de las jerarquías que están definidos en la base de datos actual.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset)|Muestra la dimensión de los grupos de medida.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUPS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset)|Devuelve una lista de los grupos de medida de la conexión actual.|  
|[Conjunto de filas MDSCHEMA_MEASURES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measures-rowset)|Devuelve una lista de las medidas en la conexión actual.|  
|[Conjunto de filas MDSCHEMA_MEMBERS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset)|Devuelve una lista de todos los miembros en la conexión actual, ordenada según la base de datos, el cubo y la dimensión.|  
|[Conjunto de filas MDSCHEMA_PROPERTIES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-properties-rowset)|Devuelve el nombre completo de cada propiedad, junto con el tipo de propiedad, el tipo de datos y otros metadatos.|  
|[Conjunto de filas MDSCHEMA_SETS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-sets-rowset)|Devuelve una lista de los conjuntos definidos en la conexión actual.|  
  
## <a name="see-also"></a>Vea también  
 [Guía de operaciones de SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409)   
 [Nuevo System.Discover_Object_Activity](https://go.microsoft.com/fwlink/?linkid=221322)   
 [Nueva función SYSTEMRESTRICTEDSCHEMA para conjuntos de filas restringidas y DMV](https://go.microsoft.com/fwlink/?LinkId=231885)  
  
  
