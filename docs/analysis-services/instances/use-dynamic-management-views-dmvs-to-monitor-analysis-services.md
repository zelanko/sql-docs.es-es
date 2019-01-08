---
title: Usar vistas de administración dinámica (DMV) de Analysis Services | Microsoft Docs
ms.date: 09/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24dd1bce8d7433f55ba64eecb1e7a08396b9e548
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2018
ms.locfileid: "52984106"
---
# <a name="dynamic-management-views-dmvs"></a>Vistas de administración dinámica (DMV) 

[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

Vistas de administración dinámica (DMV) de Analysis Services son consultas que devuelven información acerca de los objetos del modelo, las operaciones del servidor y el estado del servidor. La consulta, basada en SQL, es una interfaz para *conjuntos de filas de esquema*. Conjuntos de filas de esquema son tablas predescribed que contienen información sobre los objetos de Analysis Services y el estado del servidor, incluido el esquema de base de datos, las sesiones activas, conexiones, comandos y trabajos que se ejecutan en el servidor.

Las consultas DMV son una alternativa a la ejecución de comandos de detección XML/A. Para la mayoría de los administradores, escribir una consulta DMV es más sencillo porque la sintaxis se basa en SQL. Además, se devuelve el resultado en un formato de tabla que es más fácil de leer y copiar. 
  
La mayoría de DMV consultas utilizan un **seleccione** instrucción y el **$System** esquema con un conjunto de filas de esquema XML/A, por ejemplo:  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 Las consultas DMV devuelven información acerca del estado de servidor y el objeto en el momento en que se ejecuta la consulta. Para supervisar las operaciones en tiempo real, utilice seguimiento en su lugar. Para obtener más información acerca de en tiempo real mediante seguimientos, vea supervisión [Use SQL Server Profiler para supervisar Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
## <a name="query-syntax"></a>sintaxis de consulta

El motor de consultas para las DMV es el analizador de minería de datos. La sintaxis de consulta DMV se basa en la selección &#40;DMX&#41; instrucción. Aunque la sintaxis de las consultas DMV se basan en una instrucción SQL SELECT, no admite la sintaxis completa de una instrucción SELECT. Fundamentalmente, no se admiten JOIN, GROUP BY, LIKE, CAST ni CONVERT.  
  
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
  
Los conjuntos de filas de esquema que tienen restricciones, la consulta debe incluir la función SYSTEMRESTRICTSCHEMA. El ejemplo siguiente devuelve los metadatos CSDL 1103 unos modelos tabulares nivel de compatibilidad. Observe que CATALOG_NAME distingue entre mayúsculas y minúsculas:  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  

## <a name="examples-and-scenarios"></a>Ejemplos y escenarios

Una consulta DMV puede ayudarle a responder preguntas sobre las sesiones activas y las conexiones, y qué objetos están utilizando la mayoría de la CPU o de la memoria en un momento concreto. Por ejemplo:
  
 `Select * from $System.discover_object_activity`  
Esta consulta informa de actividad de los objetos desde que el servicio se inició por última vez. 
  
 `Select * from $System.discover_object_memory_usage`  
Esta consulta informa sobre el consumo de memoria por objeto.  
  
 `Select * from $System.discover_sessions`  
Esta consulta informa de las sesiones activas, incluida la duración y el usuario de la sesión.  
  
 `Select * from $System.discover_locks`   
Esta consulta devuelve una instantánea de los bloqueos usados en un momento concreto en el tiempo.  


## <a name="tools-and-permissions"></a>Herramientas y permisos

Puede usar cualquier aplicación cliente que admita consultas MDX o DMX. En la mayoría de los casos, es mejor usar SQL Server Management Studio. Debe tener permisos de administrador del servidor en la instancia para consultar una DMV.  
  
 **Para ejecutar una consulta DMV en SQL Server Management Studio**

1. Conectar con el servidor y el objeto de modelo que desea consultar. 
2. Haga clic en el objeto de servidor o base de datos > **nueva consulta** > **MDX**.
3. Escriba la consulta y, a continuación, haga clic en **Execute**, o presione F5.
  
## <a name="schema-rowsets"></a>Conjuntos de filas de esquema

No todos los conjuntos de filas de esquema tienen una interfaz DMV. Para obtener una lista de todos los conjuntos de filas de esquema que se pueden consultar mediante DMV, ejecute la consulta siguiente.  
 
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
Si una DMV no está disponible para un conjunto de filas determinado, el servidor devuelve el error: `The <schemarowset> request type was not recognized by the server.` Todos los demás errores indican problemas con la sintaxis.  

Conjuntos de filas de esquema se describen en los dos protocolos de SQL Server Analysis Services:   

[[MS-SSAS-T]: SQL Server Analysis Services Tabular protocolo](https://msdn.microsoft.com/library/mt719260) -describe los conjuntos de filas de esquema para los modelos tabulares en los niveles de compatibilidad 1200 y superior.

[[MS-SSAS]: Protocolo de SQL Server Analysis Services](https://msdn.microsoft.com/library/ee320606) -describe los conjuntos de filas de esquema para los modelos multidimensionales y modelos tabulares en los niveles de compatibilidad 1100 y 1103.

### <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>Conjuntos de filas que se describe en [MS-SSAS-T]: Protocolo Tabular de SQL Server Analysis Services

|Conjunto de filas  |Descripción  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|Proporciona información sobre los objetos de anotación en el modelo.|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   Proporciona información sobre los objetos AttributeHierarchy para una columna.      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  Proporciona información sobre los objetos de columna en cada tabla.       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|Proporciona información acerca de los objetos ColumnPermission en cada tabla de permisos.|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|Proporciona información sobre los objetos de referencia cultural en el modelo.|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   Proporciona información sobre los objetos de origen de datos en el modelo.      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|Proporciona información acerca de los objetos DetailRowsDefinition en el modelo.|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|Proporciona información sobre los objetos de expresión en el modelo.|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|Proporciona información sobre los objetos ExtendedProperty en el modelo.|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    Proporciona información sobre los objetos de la jerarquía de cada tabla.     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    Proporciona información sobre los objetos KPI en el modelo.     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   Proporciona información sobre los objetos de nivel de cada jerarquía.      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|Proporciona información sobre los sinónimos de los objetos del modelo para una determinada referencia cultural|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    Proporciona información sobre los objetos de la medida de cada tabla.     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  Especifica un objeto de modelo en la base de datos.       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|Proporciona información acerca de las traducciones de objetos diferentes para una referencia cultural.|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     Proporciona información sobre los objetos de partición de cada tabla.    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   Proporciona información acerca de los objetos PerspectiveColumn en cada objeto PerspectiveTable.      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  Proporciona información acerca de los objetos PerspectiveHierarchy en cada objeto PerspectiveTable.       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    Proporciona información sobre los objetos PerspectiveMeasure en cada objeto PerspectiveTable.     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    Proporciona información sobre los objetos de tabla en una perspectiva.     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     Proporciona información sobre los objetos de perspectiva en el modelo.    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    Proporciona información sobre los objetos de relación en el modelo.     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  Proporciona información acerca de los objetos RoleMembership en cada rol.      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   Proporciona información sobre los objetos de rol en el modelo.      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    Proporciona información acerca de los objetos TablePermission en cada rol.     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   Proporciona información sobre los objetos de tabla en el modelo.      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|Proporciona información sobre los objetos de la variación en cada columna.|

### <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>Conjuntos de filas que se describe en [MS-SSAS]: Protocolo SQL Server Analysis Services

|Conjunto de filas|Descripción|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|Describe los catálogos que son accesibles en el servidor.|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|Devuelve una fila para cada medida, cada atributo de dimensión de cubo y cada columna del conjunto de filas de esquema, expuesta como una columna.|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|Identifica los tipos de datos (base) admitidos por el servidor.|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|Devuelve las dimensiones, grupos de medida o expuestos como tablas de conjuntos de filas de esquema.|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| Devuelve información acerca de la dependencia de cálculo para un objeto que se especifica en una base de datos Tabular o en una consulta DAX que se ejecuta en una base de datos Tabular. |  
|[Conjunto de filas DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|Proporciona información sobre el uso de los recursos y la actividad en los objetos que utiliza el comando al que se hace referencia.|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|Proporciona información de la actividad y el uso de recursos sobre los comandos que se están ejecutando actualmente o los que se ejecutaron los últimos en las conexiones abiertas en el servidor.|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente en el servidor.|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|Devuelve información acerca de los metadatos de la base de datos para bases de datos en memoria.|  
|[DISCOVER_DATASOURCES](https://msdn.microsoft.com/library/ee320285)|Devuelve una lista de los orígenes de datos que están disponibles en el servidor.|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente desde el servidor a una base de datos.|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|Devuelve estadísticas sobre la dimensión especificada.|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|Devuelve una lista de nombres, tipos de datos y valores de enumeración de enumeradores admitidos por el proveedor de XMLA para un origen de datos concreto.|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|Describe las instancias en el servidor.|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|Proporciona información sobre los trabajos activos que se ejecutan en el servidor. Un trabajo forma una parte de un comando que ejecuta una tarea concreta en nombre del comando.|  
|[DISCOVER_KEYWORDS &AMP;#40;XMLA&AMP;#41;](https://msdn.microsoft.com/library/ee301719)|Devuelve información sobre las palabras clave reservadas por el servidor XMLA.|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|Devuelve información sobre los literales admitidos por el servidor.|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|Devuelve información sobre el contenido de un archivo de copia de seguridad. |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|Proporciona información sobre los bloqueos pendientes actuales en el servidor.|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|Devuelve la clave de cifrado maestra del servidor.|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|Devuelve una lista de concesiones de cuota de memoria interna utilizadas por los trabajos que se están ejecutando actualmente en el servidor.|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|Devuelve las estadísticas de DISCOVER_MEMORYUSAGE para diversos objetos asignados por el servidor.|  
|[Conjunto de filas DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|Proporciona el uso de recursos por objeto desde el inicio del servicio.|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|Devuelve las estadísticas de DISCOVER_MEMORYUSAGE para diversos objetos asignados por el servidor.|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|Devuelve estadísticas sobre la dimensión que está asociada a una partición.|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|Devuelve estadísticas sobre agregaciones de una partición determinada.|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|Devuelve el valor de uno o varios contadores de rendimiento especificados. |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|Devuelve una lista de información y valores de las propiedades que son compatibles con el servidor de origen de datos especificado.|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|Devuelve información acerca de los búferes de anillo de XEvent actuales en el servidor.|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|Devuelve los nombres, restricciones, descripción y otra información para todas las solicitudes de detección.|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|Proporciona información sobre el uso de los recursos y la actividad en las sesiones abiertas actualmente en el servidor.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|Devuelve información acerca de los segmentos de columna utilizado para almacenar datos de las tablas en memoria.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|Contiene información acerca de las columnas que se usa para representar las columnas de una tabla en memoria.|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|Devuelve estadísticas acerca de las tablas en memoria disponibles en el servidor.|  
|[DISCOVER_TRACE_COLUMNS](https://msdn.microsoft.com/library/ee301342)||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|Contiene el conjunto de filas de esquema DISCOVER_TRACE_COLUMNS.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|Contiene el conjunto de filas de esquema DISCOVER_TRACE_EVENT_CATEGORIES.|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|Contiene el conjunto de filas de esquema DISCOVER_TRACES.|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|Devuelve el conjunto actual de transacciones pendientes en el sistema.|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|Proporciona información sobre los seguimientos XEvent que están actualmente activas en el servidor.|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|Proporciona información sobre los paquetes de XEvent que se describen en el servidor.|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|Proporciona información sobre los objetos de XEvent que se describen en el servidor.|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|Proporciona información sobre el esquema de objetos de XEvent que se describen en el servidor.|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|Proporciona información sobre las sesiones de XEvent actuales en el servidor.|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|Proporciona información sobre los destinos de sesión de XEvent actuales en el servidor.|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|Devuelve un conjunto de filas con una fila y una columna. |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|Describe las columnas individuales de todos los modelos de minería de datos descrita que se implementan en el servidor.|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|Describe las funciones de minería de datos que son compatibles con los algoritmos de minería de datos que están disponibles en un servidor que ejecuta Analysis Services.|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|Permite que la aplicación cliente examinar el contenido de un modelo de minería de datos entrenado.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|Devuelve la estructura XML del modelo de minería de datos. El formato de la cadena XML sigue el estándar PMML 2.1.|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|Devuelve la estructura XML del modelo de minería de datos. El formato de la cadena XML sigue el estándar PMML 2.1.|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|Enumera los modelos de minería de datos implementados en el servidor.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|Proporciona una lista de los parámetros que se pueden utilizar para configurar el comportamiento de cada algoritmo de minería de datos que está instalado en el servidor.|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|Proporciona información acerca de cada algoritmo de minería de datos que admite el servidor.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|Describe las columnas individuales de todas las estructuras de minería de datos que se implementan en el servidor.|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|Enumera información sobre las estructuras de minería de datos del catálogo actual.|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|Describe las acciones que pueden estar disponibles para la aplicación cliente.|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|Describe la estructura de cubos dentro de una base de datos. También se devuelven perspectivas en este esquema.|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|Describe las dimensiones dentro de una base de datos.|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|Devuelve información sobre las funciones que están actualmente disponibles para su uso en los idiomas DAX y MDX.|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|Describe cada jerarquía dentro de una dimensión determinada.|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|Describe los objetos de origen de datos se describe dentro de la base de datos.|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|Describe los KPI dentro de una base de datos.|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|Describe cada nivel dentro de una jerarquía determinada.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|Enumera las dimensiones de grupos de medida.|  
|[MDSCHEMA_MEASUREGROUPS](https://msdn.microsoft.com/library/ee320601)|Describe los grupos de medida dentro de una base de datos.|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|Describe cada medida.|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|Describe los miembros incluidos en una base de datos.|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|Describe las propiedades de miembros y propiedades de celda.|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|Describe los conjuntos que actualmente se describen en una base de datos, incluidos los conjuntos de ámbito de sesión.|  

> [!NOTE]
> ALMACENAMIENTOS DMV no tiene un conjunto de filas de esquema que se describe en el protocolo.