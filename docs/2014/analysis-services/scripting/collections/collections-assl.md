---
title: Colecciones (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2ba3025c75d392ed1d3e818c932a6edcdba0f801
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107109"
---
# <a name="collections-assl"></a>Colecciones (ASSL)
  Esta sección de referencia contiene información sobre sintaxis y uso de cada uno de los elementos que actúan como una colección en el esquema del Lenguaje de scripting de Analysis Services (ASSL).  
  
 Aunque el esquema ASSL solamente contiene elementos XML, desde el punto de vista de un programador, los elementos descritos en esta sección se corresponden con colecciones de objetos, como por ejemplo, las colecciones `Dimensions` y `Cubes`.  
  
 Las colecciones son principalmente colecciones de elementos de objeto, en los que un nombre plural designa la colección (por ejemplo, `Cubes`) y la colección contiene elementos designados por el mismo nombre en singular (por ejemplo, `Cube`).  
  
 En algunos casos, el esquema no se adhiere a esta regla general. Por ejemplo, la colección `ClassifiedColumns` contiene elementos `ClassifiedColumnID`.  
  
 En otros casos, una colección contiene elementos que se corresponden con propiedades de objetos, no a los objetos. Por ejemplo, la colección `Aliases` contiene propiedades `Alias`, cada una de las cuales es un valor de cadena simple.  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Cuentas de elemento &#40;ASSL&#41;](accounts-element-assl.md)|Contiene la colección de tipos de cuenta que se definen en un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento Actions &#40;ASSL&#41;](actions-element-assl.md)|Contiene la colección de acciones para un [cubo](../objects/cube-element-assl.md) o [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Elemento AggregationDesigns &#40;ASSL&#41;](aggregationdesigns-element-assl.md)|Contiene la colección de diseños de agregaciones que se pueden compartir en varias particiones de una base de datos.|  
|[Elemento AggregationInstances &#40;ASSL&#41;](aggregationinstances-element-assl.md)|Contiene la colección de instancias de agregación que se definen en un [partición](../objects/partition-element-assl.md) elemento.|  
|[Elemento Aggregations &#40;ASSL&#41;](aggregations-element-assl.md)|Contiene la colección de agregaciones definida para un [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento.|  
|[Elemento AlgorithmParameters &#40;ASSL&#41;](algorithmparameters-element-assl.md)|Contiene la colección de parámetros para el algoritmo usado por un [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento aliases &#40;ASSL&#41;](aliases-element-assl.md)|Contiene la colección de [Alias](../properties/alias-element-assl.md) elementos asociados a un [cuenta](../objects/account-element-assl.md) elemento|  
|[Elemento AllMemberTranslations &#40;ASSL&#41;](translations-element-assl.md)|Contiene la colección de [traducción](../objects/translation-element-assl.md) elementos para el título del miembro All de un [jerarquía](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento Annotations &#40;ASSL&#41;](annotations-element-assl.md)|Contiene la colección de [anotación](../objects/annotation-element-assl.md) elementos asociados con el elemento primario.|  
|[Elemento Assemblies &#40;ASSL&#41;](assemblies-element-assl.md)|Contiene la colección de [ensamblado](../objects/assembly-element-assl.md) elementos asociados a un [Server](../objects/server-element-assl.md) elemento o un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento AttributeAllMemberTranslations &#40;ASSL&#41;](attributeallmembertranslations-element-assl.md)|Contiene la colección de traducciones para el título del miembro All de la dimensión.|  
|[Elemento AttributePermissions &#40;ASSL&#41;](attributepermissions-element-assl.md)|Contiene la colección de permisos de atributo para las personas [rol](../objects/role-element-assl.md) elemento en una dimensión concreta de un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationships &#40;ASSL&#41;](relationships-element-assl.md)|Contiene la colección de [AttributeRelationship](../objects/attributerelationship-element-assl.md) elementos para el atributo.|  
|[Atributos de elemento &#40;ASSL&#41;](attributes-element-assl.md)|Contiene la colección de atributos de la dimensión asociada.|  
|[Bloquea el elemento &#40;ASSL&#41;](blocks-element-assl.md)|Contiene la colección de bloques de datos binarios que representan el contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento CalculationProperties &#40;ASSL&#41;](calculationproperties-element-assl.md)|Contiene la colección de [CalculationProperty](../objects/calculationproperty-element-assl.md) elementos asociados a un [MdxScript](../objects/mdxscript-element-assl.md) elemento.|  
|[Elemento calculations &#40;ASSL&#41;](calculations-element-assl.md)|Contiene la colección de [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elementos asociados a un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Elemento CellPermissions &#40;ASSL&#41;](cellpermissions-element-assl.md)|Contiene la colección de permisos para las celdas en el asociado [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento ClassifiedColumns &#40;ASSL&#41;](columns-element-assl.md)|Contiene la colección de columnas relacionadas clasificadas por el [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento Columns &#40;ASSL&#41;](columns-element-assl.md)|Contiene la colección de columnas asociada al elemento primario.|  
|[Comandos de elemento &#40;ASSL&#41;](commands-element-assl.md)|Contiene la colección de elementos [Command](../objects/command-element-assl.md) asociada a un elemento [MdxScript](../objects/mdxscript-element-assl.md) .|  
|[Elemento CubePermissions &#40;ASSL&#41;](cubepermissions-element-assl.md)|Contiene la colección de permisos aplicable a una [cubo](../objects/cube-element-assl.md) elemento.|  
|[Cubos elemento &#40;ASSL&#41;](cubes-element-assl.md)|Contiene la colección de [cubo](../objects/cube-element-assl.md) elementos asociados a un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento DatabasePermissions &#40;ASSL&#41;](databasepermissions-element-assl.md)|Contiene la colección de [DatabasePermission](../objects/databasepermission-element-assl.md) elementos asociados a un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento Databases &#40;ASSL&#41;](databases-element-assl.md)|Contiene la colección de [base de datos](../objects/database-element-assl.md) elementos asociados a un [Server](../objects/server-element-assl.md) elemento.|  
|[Elemento DataSources &#40;ASSL&#41;](datasources-element-assl.md)|Contiene la colección de [DataSourcePermission](../objects/datasourcepermission-element-assl.md) elementos asociados a un [DataSource](../data-type/datasource-data-type-assl.md) tipo de datos.|  
|[Elemento DataSourcePermissions &#40;ASSL&#41;](datasourcepermissions-element-assl.md)|Contiene la colección de [DataSource](../objects/datasource-element-assl.md) elementos asociados a un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elementos Datasourceviews &#40;ASSL&#41;](datasourceviews-element-assl.md)|Contiene la colección de [DataSourceView](../objects/datasourceview-element-assl.md) elementos asociados a un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento DimensionPermissions &#40;ASSL&#41;](dimensionpermissions-element-assl.md)|Contiene la colección de permisos aplicable a una [dimensión](../objects/dimension-element-assl.md) elemento o un [CubePermission](../objects/cubepermission-element-assl.md) elemento.|  
|[Dimensiones elemento &#40;ASSL&#41;](dimensions-element-assl.md)|Contiene la colección de dimensiones asociada al elemento primario.|  
|[Elemento Events &#40;ASSL&#41;](events-element-assl.md)|Define la colección de elementos de evento que va a capturar un [seguimiento](../objects/trace-element-assl.md).|  
|[Archivos elemento &#40;ASSL&#41;](files-element-assl.md)|Contiene la colección de [archivo](../objects/file-element-assl.md) elementos que componen un [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumns &#40;ASSL&#41;](keycolumns-element-assl.md)|Contiene la colección de columnas que identifican la unión a la tabla primaria para un origen de datos relacional.|  
|[Elemento Groups &#40;ASSL&#41;](groups-element-assl.md)|Contiene la colección de grupos de miembros enlazados a un atributo.|  
|[Elemento Hierarchies &#40;ASSL&#41;](hierarchies-element-assl.md)|Contiene la colección de [jerarquía](../objects/hierarchy-element-assl.md) elementos asociados con el elemento primario.|  
|[Elemento IncrementalProcessingNotifications &#40;ASSL&#41;](incrementalprocessingnotifications-element-assl.md)|Contiene la colección de [IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md) elementos que proporcionan información para la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento acerca de las consultas que se ejecutan para determinar el progreso del procesamiento incremental.|  
|[Elemento KeyColumns &#40;ASSL&#41;](keycolumns-element-assl.md)|Contiene la colección de [KeyColumn](../objects/column-element-assl.md) definiciones de elementos para un objeto primario.|  
|[Elemento KPIs &#40;ASSL&#41;](kpis-element-assl.md)|Contiene la colección de [Kpi](../objects/kpi-element-assl.md) elementos asociados con el elemento primario.|  
|[Un nivel de elemento &#40;ASSL&#41;](levels-element-assl.md)|Contiene la colección de [nivel](../objects/level-element-assl.md) elementos en una [jerarquía](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScripts &#40;ASSL&#41;](mdxscripts-element-assl.md)|Contiene la colección de [MdxScript](../objects/mdxscript-element-assl.md) elementos asociados a un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento MeasureGroups &#40;ASSL&#41;](measuregroups-element-assl.md)|Contiene la colección de [MeasureGroup](../objects/group-element-assl.md) elementos asociados con el elemento primario.|  
|[Mide el elemento &#40;ASSL&#41;](measures-element-assl.md)|Contiene la colección de [medida](../objects/measure-element-assl.md) elementos asociados con el elemento primario.|  
|[Elemento Members &#40;ASSL&#41;](members-element-assl.md)|Contiene la colección de elementos [Member](../objects/member-element-assl.md) asociada al elemento primario.|  
|[Elemento MiningModelPermissions &#40;ASSL&#41;](miningmodelpermissions-element-assl.md)|Contiene la colección de permisos para un [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento MiningModels &#40;ASSL&#41;](miningmodels-element-assl.md)|Contiene la colección de [MiningModel](../objects/miningmodel-element-assl.md) elementos asociados a un [MiningStructure](../objects/miningstructure-element-assl.md).|  
|[Elemento MiningStructurePermissions &#40;ASSL&#41;](miningstructurepermissions-element-assl.md)|Contiene la colección de permisos en un [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Elemento MiningStructures &#40;ASSL&#41;](miningstructures-element-assl.md)|Contiene la colección de [MiningStructure](../objects/miningstructure-element-assl.md) elementos en una [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento ModelingFlags &#40;ASSL&#41;](modelingflags-element-assl.md)|Contiene la colección de [ModelingFlag](../objects/modelingflag-element-assl.md) elementos para una columna en una [MiningStructure](../objects/miningstructure-element-assl.md) o un [MiningModel](../objects/miningmodel-element-assl.md).|  
|[Elemento NamingTemplateTranslations &#40;ASSL&#41;](namingtemplatetranslations-element-assl.md)|Proporciona una colección de traducciones adaptadas para el [NamingTemplate](../properties/namingtemplate-element-assl.md) elemento del elemento primario [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md).|  
|[Particiones elemento &#40;ASSL&#41;](partitions-element-assl.md)|Contiene la colección de [partición](../objects/partition-element-assl.md) elementos utilizados por un [MeasureGroup](../objects/group-element-assl.md) elemento o la colección de enlaces de partición que constituyen un fuera de línea [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspectives &#40;ASSL&#41;](perspectives-element-assl.md)|Contiene la colección de [perspectiva](../objects/perspective-element-assl.md) elementos asociados a un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Elemento QueryNotifications &#40;ASSL&#41;](querynotifications-element-assl.md)|Contiene la colección de [QueryNotification](../objects/querynotification-element-assl.md) elementos que proporcionan información para la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento acerca de las consultas que se ejecutan para determinar si se ha modificado un origen de datos.|  
|[Elemento ReportFormatParameters &#40;ASSL&#41;](reportformatparameters-element-assl.md)|Contiene la colección de los elementos [ReportFormatParameter](../objects/reportformatparameter-element-asl.md) para un elemento [ReportAction](../data-type/action-data-type-assl.md) .|  
|[Elemento ReportParameters &#40;ASSL&#41;](reportparameters-element-assl.md)|Contiene la colección de [ReportParameter](../objects/reportparameter-element-assl.md) elementos de un [ReportAction](../data-type/action-data-type-assl.md) elemento.|  
|[Elemento roles &#40;ASSL&#41;](roles-element-assl.md)|Contiene la colección de elementos [Role](../objects/role-element-assl.md) definida bajo el elemento primario.|  
|[Elemento ServerProperties &#40;ASSL&#41;](serverproperties-element-assl.md)|Contiene la colección de [ServerProperty](../objects/serverproperty-element-assl.md) elementos asociados a un [Server](../objects/server-element-assl.md) elemento.|  
|[Elemento TableNotifications &#40;ASSL&#41;](tablenotifications-element-assl.md)|Contiene la colección de [TableNotification](../objects/tablenotification-element-assl.md) elementos que proporcionan información para la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre las tablas o vistas en un origen de datos que se han modificado.|  
|[Realiza un seguimiento de elemento &#40;ASSL&#41;](traces-element-assl.md)|Contiene la colección de elementos [Trace](../objects/trace-element-assl.md) asociados a un elemento [Server](../objects/server-element-assl.md) .|  
|[Elemento Translations &#40;ASSL&#41;](translations-element-assl.md)|Contiene la colección de [traducción](../objects/translation-element-assl.md) elementos asociados con el elemento primario.|  
|[Elemento UnknownMemberTranslations &#40;ASSL&#41;](unknownmembertranslations-element-assl.md)|Contiene la colección de traducciones para el título de la [UnknownMember](../properties/unknownmember-element-assl.md) elemento de una dimensión.|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía Analysis Services Scripting Language XML elemento &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  