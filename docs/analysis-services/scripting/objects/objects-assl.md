---
title: Objetos (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d45d482ecb50e0215b9d0ad5d57f537e8899d5c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="objects-assl"></a>Objetos (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Esta sección de referencia contiene información sobre sintaxis y utilización de cada uno de los elementos que actúan como un objeto en el esquema del Lenguaje de scripting de Analysis Services (ASSL).  
  
 Aunque el esquema ASSL solamente contiene elementos XML, desde el punto de vista de un programador, los elementos descritos en esta sección se corresponden a objetos, como por ejemplo **base de datos**, **cubo**, y  **Dimensión** objetos, en la jerarquía de objetos contenida en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Los objetos nunca son los elementos en el nivel de hoja en el esquema ASSL, pero tienen elementos secundarios y elementos que se corresponden con las propiedades de objetos.  
  
 En algunos casos, un elemento en el nivel de hoja en el esquema que pueda parecer una propiedad se clasifica como objeto, porque el tipo del elemento es un tipo de objeto. Por ejemplo, el **origen** de un **dimensión** objeto es de tipo **DimensionBinding**.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento de la cuenta &#40;ASSL&#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|Contiene información detallada sobre un tipo de cuenta dentro de un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento action &#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|Contiene información sobre una acción disponible en un elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) o un elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .|  
|[Elemento aggregation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|Define una agregación única para una [partición](../../../analysis-services/scripting/objects/partition-element-assl.md) elemento.|  
|[Elemento AggregationDesign &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|Define un conjunto de definiciones de agregación que se pueden compartir en varias particiones de una base de datos.|  
|[Elemento AggregationInstance &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|Define una instancia de agregación para una partición.|  
|[Elemento AlgorithmParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Define un parámetro para el algoritmo usado por un [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento AllMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|Contiene una traducción para el título del miembro All de un [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento de anotación &#40;ASSL&#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|Contiene elementos que se utilizan para extender el esquema ASSL.|  
|[Assembly (elemento) &#40;ASSL&#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|Representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado o una biblioteca de vínculos dinámicos de COM (DLL) asociada con un [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento o un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Atributo de elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|Contiene la descripción de un atributo.|  
|[Elemento AttributeAllMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|Contiene una traducción para el título del miembro All de un [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) elemento.|  
|[Elemento Attributepermissions &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|Define los permisos que los miembros de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tiene los atributos de una dimensión concreta en un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationship &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|Proporciona detalles sobre la relación entre dos atributos.|  
|[Bloquear elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|Contiene todo o parte del contenido binario de un [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento Calculation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|Asocia un cálculo con un [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento.|  
|[Elemento CalculationProperty &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|Contiene una colección de propiedades de la interfaz de usuario para un cálculo utilizado en un [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) elemento.|  
|[Elemento CaptionColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|Define la columna que proporciona el título para el atributo.|  
|[Elemento CellPermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|Se describen los permisos que los miembros de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tienen en celdas individuales dentro de un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento de columna &#40;ASSL&#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|Describe una columna en la colección de columnas asociada al elemento principal.|  
|[Elemento de comando &#40;ASSL&#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|Define un comando que está disponible para su uso dentro del contexto del elemento principal de la colección Commands.|  
|[Elemento de cubo &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|Define un cubo normal, virtual o vinculado en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento CubePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|Define los permisos de los miembros de una determinada [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento en un determinado [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento CustomRollupColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|Define los detalles de la columna que proporciona una fórmula de resumen personalizada.|  
|[Elemento CustomRollupPropertiesColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|Define los detalles de una columna que proporciona las propiedades de una fórmula de resumen personalizado.|  
|[Elemento de datos &#40;ASSL&#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|Contiene (en la colección del elemento secundario **bloque** elementos) el contenido binario de un [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento de la base de datos &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|Define una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento DatabasePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|Define los permisos predeterminados en un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) (elemento) para un determinado [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.|  
|[Elemento DataSource &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|Define un origen de datos en un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento DataSourcePermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|Define los permisos predeterminados en un [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de datos para un determinado [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.|  
|[Elemento DataSourceView &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|Define una vista del origen de datos utilizada por un [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.|  
|[Elemento de dimensión &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Define una dimensión.|  
|[Dimensionpermission, elemento &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|Define los permisos que pertenecen a un determinado [rol](../../../analysis-services/scripting/objects/role-element-assl.md) , elemento de una dimensión de base de datos específica o una dimensión de cubo.|  
|[Elemento ErrorConfiguration &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|Especifica los valores para administrar errores que se pueden producir cuando se procesa el elemento primario.|  
|[Elemento Event &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|Define un evento que va a capturar como parte de un [seguimiento](../../../analysis-services/scripting/objects/trace-element-assl.md) elemento.|  
|[Elemento file &#40;ASSL&#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|Define uno de los archivos que componen un [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|Identifica la unión a una tabla primaria para un origen de datos relacional.|  
|[Elemento group &#40;ASSL&#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|Define un grupo de miembros enlazados a un atributo.|  
|[Elemento de la jerarquía &#40;ASSL&#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|Define una jerarquía en una dimensión|  
|[Elemento IncrementalProcessingNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|Contiene información para la [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar el progreso del procesamiento incremental.|  
|[Elemento KeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|Contiene la definición de una columna que es o forma parte de la clave de un atributo.|  
|[Elemento KPI &#40;ASSL&#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|Define un indicador de rendimiento clave (KPI) dentro de un elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) o un elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .|  
|[Elemento nivel &#40;ASSL&#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|Define un nivel en un [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|Contiene información sobre un script de expresiones multidimensionales (MDX) que está asociado con un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento de medida &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|Define una medida.|  
|[Elemento MeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Define un conjunto de medidas en el mismo nivel de granularidad.|  
|[Elemento Member &#40;ASSL&#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|Contiene el nombre de un miembro de un elemento [Group](../../../analysis-services/scripting/objects/group-element-assl.md) o de un elemento [Role](../../../analysis-services/scripting/objects/role-element-assl.md) .|  
|[Elemento MiningModel &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|Define un único modelo de minería de datos.|  
|[Elemento MiningModelPermission &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|Define los miembros de los permisos de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tiene en un individuo [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.|  
|[Elemento MiningStructure &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|Define la estructura de un conjunto de modelos de minería de datos.|  
|[Elemento Miningstructurepermissions &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|Define los permisos que los miembros de un [rol](../../../analysis-services/scripting/objects/role-element-assl.md) elemento tiene en un individuo [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento.|  
|[Elemento ModelingFlag &#40;ASSL&#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|Contiene una marca de modelado para una columna de una estructura de minería de datos o un modelo de minería.|  
|[Elemento NameColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|Identifica la columna que proporciona el nombre del elemento primario.|  
|[Elemento NamingTemplateTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|Proporciona una traducción adaptada de la **NamingTemplate** (elemento) para un elemento primario [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) tipo de datos.|  
|[Elemento de la partición &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|Define una partición de un [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) elemento o una partición que enlaza un fuera de línea [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspective &#40;ASSL&#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|Define los detalles de una perspectiva de un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.|  
|[Elemento ProactiveCaching &#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|Define la configuración de almacenamiento en caché automático para el elemento primario.|  
|[Elemento QueryNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|Contiene información para la [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar si se ha modificado un origen de datos.|  
|[Elemento ReportFormatParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|Contiene el nombre y el valor de un parámetro que especifica cómo un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se da formato al informe en tiempo de ejecución.|  
|[Elemento ReportParameter &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|Contiene el nombre y el valor de un parámetro que se pasa en tiempo de ejecución a un informe de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Elemento role &#40;ASSL&#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|Contiene información sobre un rol de seguridad.|  
|[Elemento Server &#40;ASSL&#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|Describe a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ServerProperty &#40;ASSL&#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Define una propiedad del servidor asociada con un [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|[Elemento SkippedLevelsColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|Proporciona los detalles de una columna que almacena el número de niveles omitidos (vacíos) entre cada miembro y su elemento primario.|  
|[Elemento SourceMeasureGroup &#40;ASSL&#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Identifica el grupo de medida que actúa como origen de datos para una columna de estructura de minería de datos.|  
|[Elemento TableNotification &#40;ASSL&#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|Contiene información para la [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) elemento acerca de una tabla o vista en un origen de datos que se ha modificado.|  
|[Elemento Trace &#40;ASSL&#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|Define un seguimiento que se puede consultar.|  
|[Elemento Translation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|Proporciona una traducción adaptada para el elemento primario de la colección [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) .|  
|[Elemento UnaryOperatorColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|Define los detalles de una columna que proporciona un operador unario.|  
|[Elemento UnknownMemberTranslation &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|Contiene una traducción para el título de la [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) (elemento) para un [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md) elemento.|  
|[Elemento ValueColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|Identifica la columna que proporciona el valor del elemento primario.|  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language jerarquía de elementos XML & #40; ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
