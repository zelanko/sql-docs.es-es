---
title: Objetos (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 302ad689a3e54a7a9937929b9c20f975fc3cd98f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079615"
---
# <a name="objects-assl"></a>Objetos (ASSL)
  Esta sección de referencia contiene información sobre sintaxis y utilización de cada uno de los elementos que actúan como un objeto en el esquema del Lenguaje de scripting de Analysis Services (ASSL).  
  
 Aunque el esquema ASSL solamente contiene elementos XML, desde el punto de vista del desarrollador, los elementos descritos en esta sección se corresponden a objetos, como `Database`, `Cube`, y `Dimension` objetos, en la jerarquía de objetos contenida en un instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Los objetos nunca son los elementos en el nivel de hoja en el esquema ASSL, pero tienen elementos secundarios y elementos que se corresponden con las propiedades de objetos.  
  
 En algunos casos, un elemento en el nivel de hoja en el esquema que pueda parecer una propiedad se clasifica como objeto, porque el tipo del elemento es un tipo de objeto. Por ejemplo, el `Source` de un objeto `Dimension` el de tipo `DimensionBinding`.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento de la cuenta &#40;ASSL&#41;](account-element-assl.md)|Contiene información detallada sobre un tipo de cuenta dentro de un [base de datos](database-element-assl.md) elemento.|  
|[Elemento action &#40;ASSL&#41;](action-element-assl.md)|Contiene información sobre una acción disponible en un [cubo](cube-element-assl.md) elemento o un [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento aggregation &#40;ASSL&#41;](aggregation-element-assl.md)|Define una agregación única para un [partición](partition-element-assl.md) elemento.|  
|[Elemento AggregationDesign &#40;ASSL&#41;](aggregationdesign-element-assl.md)|Define un conjunto de definiciones de agregación que se pueden compartir en varias particiones de una base de datos.|  
|[Elemento AggregationInstance &#40;ASSL&#41;](aggregationinstance-element-assl.md)|Define una instancia de agregación para una partición.|  
|[Elemento AlgorithmParameter &#40;ASSL&#41;](algorithmparameter-element-assl.md)|Define un parámetro para el algoritmo utilizado por un [MiningModel](miningmodel-element-assl.md) elemento.|  
|[Elemento AllMemberTranslation &#40;ASSL&#41;](translation-element-assl.md)|Contiene una traducción para el título del miembro All de un [jerarquía](hierarchy-element-assl.md) elemento.|  
|[Elemento Annotation &#40;ASSL&#41;](annotation-element-assl.md)|Contiene elementos que se utilizan para extender el esquema ASSL.|  
|[Elemento Assembly &#40;ASSL&#41;](assembly-element-assl.md)|Representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado o una biblioteca de vínculos dinámicos COM (DLL) asociada con un [Server](server-element-assl.md) elemento o un [base de datos](database-element-assl.md) elemento.|  
|[Atributo de elemento &#40;ASSL&#41;](attribute-element-assl.md)|Contiene la descripción de un atributo.|  
|[Elemento AttributeAllMemberTranslation &#40;ASSL&#41;](attributeallmembertranslation-element-assl.md)|Contiene una traducción para el título del miembro All de un [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) elemento.|  
|[Elemento Attributepermissions &#40;ASSL&#41;](attributepermission-element-assl.md)|Define los permisos que los miembros de un [rol](role-element-assl.md) elemento tiene los atributos de una dimensión concreta en un [cubo](cube-element-assl.md) elemento.|  
|[Elemento AttributeRelationship &#40;ASSL&#41;](attributerelationship-element-assl.md)|Proporciona detalles sobre la relación entre dos atributos.|  
|[Bloquear elemento &#40;ASSL&#41;](block-element-assl.md)|Contiene todo o parte del contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento Calculation &#40;ASSL&#41;](calculation-element-assl.md)|Asocia un cálculo con a una [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento CalculationProperty &#40;ASSL&#41;](calculationproperty-element-assl.md)|Contiene una colección de propiedades de la interfaz de usuario para un cálculo utilizado en un [MdxScript](mdxscript-element-assl.md) elemento.|  
|[Elemento CaptionColumn &#40;ASSL&#41;](column-element-assl.md)|Define la columna que proporciona el título para el atributo.|  
|[Elemento CellPermission &#40;ASSL&#41;](cellpermission-element-assl.md)|Describe los permisos que los miembros de un [rol](role-element-assl.md) elemento tienen en celdas individuales dentro de un [cubo](cube-element-assl.md) elemento.|  
|[Elemento Column &#40;ASSL&#41;](column-element-assl.md)|Describe una columna en la colección de columnas asociada al elemento principal.|  
|[Elemento de comando &#40;ASSL&#41;](command-element-assl.md)|Define un comando que está disponible para su uso dentro del contexto del elemento principal de la colección Commands.|  
|[Elemento de cubo &#40;ASSL&#41;](cube-element-assl.md)|Define un cubo normal, virtual o vinculado en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [base de datos](database-element-assl.md) elemento.|  
|[Elemento CubePermission &#40;ASSL&#41;](cubepermission-element-assl.md)|Define los permisos de los miembros de un determinado [rol](role-element-assl.md) elemento en un determinado [cubo](cube-element-assl.md) elemento.|  
|[Elemento CustomRollupColumn &#40;ASSL&#41;](customrollupcolumn-element-assl.md)|Define los detalles de la columna que proporciona una fórmula de resumen personalizada.|  
|[Elemento CustomRollupPropertiesColumn &#40;ASSL&#41;](customrolluppropertiescolumn-element-assl.md)|Define los detalles de una columna que proporciona las propiedades de una fórmula de resumen personalizado.|  
|[Elemento de datos &#40;ASSL&#41;](data-element-assl.md)|Contiene (en la colección del elemento secundario `Block` elementos) el contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.|  
|[Elemento de la base de datos &#40;ASSL&#41;](database-element-assl.md)|Define una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento DatabasePermission &#40;ASSL&#41;](databasepermission-element-assl.md)|Define los permisos predeterminados en un [base de datos](database-element-assl.md) (elemento) para un determinado [rol](role-element-assl.md) elemento.|  
|[Elemento DataSource &#40;ASSL&#41;](datasource-element-assl.md)|Define un origen de datos en un [base de datos](database-element-assl.md) elemento.|  
|[Elemento DataSourcePermission &#40;ASSL&#41;](datasourcepermission-element-assl.md)|Define los permisos predeterminados en un [DataSource](../data-type/datasource-data-type-assl.md) tipo de datos para un determinado [rol](role-element-assl.md) elemento.|  
|[Elemento DataSourceView &#40;ASSL&#41;](datasourceview-element-assl.md)|Define una vista del origen de datos utilizada por un [base de datos](database-element-assl.md) elemento.|  
|[Elemento de dimensión &#40;ASSL&#41;](dimension-element-assl.md)|Define una dimensión.|  
|[Elemento DimensionPermission &#40;ASSL&#41;](dimensionpermission-element-assl.md)|Define los permisos que pertenecen a un determinado [rol](role-element-assl.md) (elemento) para una dimensión de base de datos específica o una dimensión de cubo.|  
|[Elemento ErrorConfiguration &#40;ASSL&#41;](errorconfiguration-element-assl.md)|Especifica los valores para administrar errores que se pueden producir cuando se procesa el elemento primario.|  
|[Elemento de evento &#40;ASSL&#41;](event-element-assl.md)|Define un evento que va a capturar como parte de un [seguimiento](trace-element-assl.md) elemento.|  
|[Elemento file &#40;ASSL&#41;](file-element-assl.md)|Define uno de los archivos que componen un [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.|  
|[Elemento ForeignKeyColumn &#40;ASSL&#41;](keycolumn-element-assl.md)|Identifica la unión a una tabla primaria para un origen de datos relacional.|  
|[Elemento group &#40;ASSL&#41;](group-element-assl.md)|Define un grupo de miembros enlazados a un atributo.|  
|[Elemento Hierarchy &#40;ASSL&#41;](hierarchy-element-assl.md)|Define una jerarquía en una dimensión|  
|[Elemento IncrementalProcessingNotification &#40;ASSL&#41;](incrementalprocessingnotification-element-assl.md)|Contiene información para el [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar el progreso del procesamiento incremental.|  
|[Elemento KeyColumn &#40;ASSL&#41;](keycolumn-element-assl.md)|Contiene la definición de una columna que es o forma parte de la clave para un atributo.|  
|[Elemento KPI &#40;ASSL&#41;](kpi-element-assl.md)|Define un indicador clave de rendimiento (KPI) dentro de un [cubo](cube-element-assl.md) elemento o un [perspectiva](perspective-element-assl.md) elemento.|  
|[Elemento de nivel &#40;ASSL&#41;](level-element-assl.md)|Define un nivel en un [jerarquía](hierarchy-element-assl.md) elemento.|  
|[Elemento MdxScript &#40;ASSL&#41;](mdxscript-element-assl.md)|Contiene información sobre un script de expresiones multidimensionales (MDX) que está asociado con un [cubo](cube-element-assl.md) elemento.|  
|[Elemento de medida &#40;ASSL&#41;](measure-element-assl.md)|Define una medida.|  
|[Elemento MeasureGroup &#40;ASSL&#41;](measuregroup-element-assl.md)|Define un conjunto de medidas en el mismo nivel de granularidad.|  
|[Elemento Member &#40;ASSL&#41;](member-element-assl.md)|Contiene el nombre de un miembro de un elemento [Group](group-element-assl.md) o de un elemento [Role](role-element-assl.md) .|  
|[Elemento MiningModel &#40;ASSL&#41;](miningmodel-element-assl.md)|Define un único modelo de minería de datos.|  
|[Elemento MiningModelPermission &#40;ASSL&#41;](miningmodelpermission-element-assl.md)|Define los miembros de los permisos de un [rol](role-element-assl.md) tiene elemento individual [MiningModel](miningmodel-element-assl.md) elemento.|  
|[Elemento MiningStructure &#40;ASSL&#41;](miningstructure-element-assl.md)|Define la estructura de un conjunto de modelos de minería de datos.|  
|[Elemento Miningstructurepermissions &#40;ASSL&#41;](miningstructurepermission-element-assl.md)|Define los permisos que los miembros de un [rol](role-element-assl.md) tiene elemento individual [MiningStructure](miningstructure-element-assl.md) elemento.|  
|[Elemento ModelingFlag &#40;ASSL&#41;](modelingflag-element-assl.md)|Contiene una marca de modelado para una columna de una estructura de minería de datos o un modelo de minería.|  
|[Elemento NameColumn &#40;ASSL&#41;](namecolumn-element-assl.md)|Identifica la columna que proporciona el nombre del elemento primario.|  
|[Elemento NamingTemplateTranslation &#40;ASSL&#41;](namingtemplatetranslation-element-assl.md)|Proporciona una traducción adaptada de la `NamingTemplate` (elemento) para un elemento primario [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) tipo de datos.|  
|[Elemento de la partición &#40;ASSL&#41;](partition-element-assl.md)|Define una partición de un [MeasureGroup](measuregroup-element-assl.md) elemento o una partición que enlaza un fuera de línea [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)elemento.|  
|[Elemento Perspective &#40;ASSL&#41;](perspective-element-assl.md)|Define los detalles de una perspectiva de un [cubo](cube-element-assl.md) elemento.|  
|[Elemento ProactiveCaching &#40;ASSL&#41;](proactivecaching-element-assl.md)|Define la configuración de almacenamiento en caché automático para el elemento primario.|  
|[Elemento QueryNotification &#40;ASSL&#41;](querynotification-element-assl.md)|Contiene información para el [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar si se ha modificado un origen de datos.|  
|[Elemento ReportFormatParameter &#40;ASSL&#41;](reportformatparameter-element-asl.md)|Contiene el nombre y valor de un parámetro que especifica cómo un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se da formato al informe en tiempo de ejecución.|  
|[Elemento ReportParameter &#40;ASSL&#41;](reportparameter-element-assl.md)|Contiene el nombre y el valor de un parámetro que se pasa en tiempo de ejecución a un informe de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Elemento role &#40;ASSL&#41;](role-element-assl.md)|Contiene información sobre un rol de seguridad.|  
|[Elemento Server &#40;ASSL&#41;](server-element-assl.md)|Describe a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento ServerProperty &#40;ASSL&#41;](serverproperty-element-assl.md)|Define una propiedad del servidor asociada con un [Server](server-element-assl.md) elemento.|  
|[Elemento SkippedLevelsColumn &#40;ASSL&#41;](skippedlevelscolumn-element-assl.md)|Proporciona los detalles de una columna que almacena el número de niveles omitidos (vacíos) entre cada miembro y su elemento primario.|  
|[Elemento SourceMeasureGroup &#40;ASSL&#41;](sourcemeasuregroup-element-assl.md)|Identifica el grupo de medida que actúa como origen de datos para una columna de estructura de minería de datos.|  
|[Elemento TableNotification &#40;ASSL&#41;](tablenotification-element-assl.md)|Contiene información para el [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre una tabla o vista en un origen de datos que se ha modificado.|  
|[Elemento Trace &#40;ASSL&#41;](trace-element-assl.md)|Define un seguimiento que se puede consultar.|  
|[Elemento Translation &#40;ASSL&#41;](translation-element-assl.md)|Proporciona una traducción adaptada para el elemento primario de la colección [Translations](../collections/translations-element-assl.md) .|  
|[Elemento UnaryOperatorColumn &#40;ASSL&#41;](unaryoperatorcolumn-element-assl.md)|Define los detalles de una columna que proporciona un operador unario.|  
|[Elemento UnknownMemberTranslation &#40;ASSL&#41;](unknownmembertranslation-element-assl.md)|Contiene una traducción para el título de la [UnknownMember](../properties/unknownmember-element-assl.md) (elemento) para un [dimensión](dimension-element-assl.md) elemento.|  
|[Elemento ValueColumn &#40;ASSL&#41;](valuecolumn-element-assl.md)|Identifica la columna que proporciona el valor del elemento primario.|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de elementos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
