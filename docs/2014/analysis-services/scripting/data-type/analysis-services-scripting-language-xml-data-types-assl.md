---
title: Tipos de datos XML de Scripting Language (ASSL) de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Analysis Services Scripting Language XML Data Types
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3420e553b1391fb9645f7e3bffa884e255a90897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197063"
---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>Tipos de datos XML de Analysis Services Scripting Language (ASSL)
  Esta sección de referencia contiene información sobre sintaxis y utilización de cada uno de los elementos que actúan como un tipo en el esquema del lenguaje de scripting de Analysis Services (ASSL).  
  
 Aunque el esquema ASSL solamente contiene elementos XML, desde el punto de vista de un programador, los elementos descritos en esta sección se corresponden con tipos, como por ejemplo `Binding` y `Permission`, que se utilizan para definir los elementos secundarios y las propiedades de otros objetos.  
  
 Los elementos de tipo, como pueden ser los elementos de objetos, nunca son los elementos en el nivel de hoja en el esquema ASSL, pero tienen elementos secundarios y elementos que se corresponden con las propiedades de objetos.  
  
 Sin embargo un elemento de tipo nunca aparece como un elemento en un script que define o describe [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos. En su lugar aparece como el tipo de otros elementos de objeto, normalmente designado con el atributo de `type` del esquema Instancia del esquema XML utilizando `xsi:type` o `xs:type`. Por ejemplo, `<Assembly xsi:type="ClrAssembly">...</Assembly>`.  
  
 En algunos casos, un tipo se deriva de otro tipo. Por ejemplo, el tipo `CubeBinding` se deriva del tipo `Binding` primario.  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Tipo de datos de acción &#40;ASSL&#41;](action-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa una acción en un [cubo](../objects/cube-element-assl.md) elemento o un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de datos AggregationAttribute &#40;ASSL&#41;](aggregationattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa la asociación entre un [agregación](../objects/aggregation-element-assl.md) elemento y un atributo.|  
|[Tipo de datos AggregationDesignAttribute &#40;ASSL&#41;](aggregationdesignattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa la asociación entre un atributo y un [AggregationDesignDimension](dimension-data-type-assl.md) elemento.|  
|[Tipo de datos AggregationDesignDimension &#40;ASSL&#41;](dimension-data-type-assl.md)|Define un tipo de datos primitivo que representa la relación entre una dimensión de cubo y un [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento.|  
|[Tipo de datos AggregationDimension &#40;ASSL&#41;](aggregationdimension-data-type-assl.md)|Define un tipo de datos primitivo que representa la relación entre una dimensión y un [agregación](../objects/aggregation-element-assl.md) elemento.|  
|[Tipo de datos AggregationInstanceAttribute &#40;ASSL&#41;](aggregationinstanceattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre un atributo utilizado en una instancia de agregación.|  
|[Tipo de datos AggregationInstanceCubeDimension &#40;ASSL&#41;](cubedimension-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una dimensión de cubo utilizada en una instancia de agregación.|  
|[Tipo de datos AggregationInstanceMeasure &#40;ASSL&#41;](aggregationinstancemeasure-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una medida utilizada en una instancia de agregación.|  
|[Tipo de datos de ensamblado &#40;ASSL&#41;](assembly-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado o una biblioteca de vínculos dinámicos de COM (DLL) asociada con un [Server](../objects/server-element-assl.md) o [base de datos](../objects/database-element-assl.md) elemento.|  
|[Tipo de datos AttributeBinding &#40;ASSL&#41;](binding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace para un [atributo](../objects/attribute-element-assl.md) elemento.|  
|[Tipo de datos AttributeTranslation &#40;ASSL&#41;](translation-data-type-assl.md)|Define un tipo de datos derivado que representa una traducción asociada con una [atributo](../objects/attribute-element-assl.md) elemento|  
|[Tipo de datos de enlace &#40;ASSL&#41;](binding-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa una relación de dependencia entre dos objetos en los que los datos o metadatos de uno de los objetos dependen de los datos o metadatos de un objeto enlazado.|  
|[Tipo de datos ClrAssembly &#40;ASSL&#41;](clrassembly-data-type-assl.md)|Define un tipo de datos derivado que representa un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado asociado a un [base de datos](../objects/database-element-assl.md) o [Server](../objects/server-element-assl.md) elemento|  
|[Tipo de datos ClrAssemblyFile &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)|Define un tipo de datos primitivo que representa uno de los archivos que componen un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ensamblado ([ClrAssembly](clrassembly-data-type-assl.md) elemento).|  
|[Tipo de datos ColumnBinding &#40;ASSL&#41;](columnbinding-data-type-assl.md)|Define un tipo de datos derivado que representa el enlace de una columna en una vista del origen de datos para un [DataItem](dataitem-data-type-assl.md) elemento.|  
|[Tipo de datos ComAssembly &#40;ASSL&#41;](comassembly-data-type-assl.md)|Define un tipo de datos derivado que representa una biblioteca COM asociada con un [Server](../objects/server-element-assl.md) o [base de datos](../objects/database-element-assl.md) elemento.|  
|[Tipo de datos CubeAttribute &#40;ASSL&#41;](cubeattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa un atributo asociado con un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de datos CubeAttributeBinding &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|Define un tipo de datos derivado que representa el enlace de un atributo en una dimensión de cubo con una acción o con una columna de estructura de minería de datos.|  
|[Tipo de datos CubeBinding &#40;fuera de línea&#41; &#40;ASSL&#41;](cubebinding-data-type-out-of-line-assl.md)|Define un tipo de datos primitivo que representa la relación entre un [cubo](../objects/cube-element-assl.md) elemento y un [DataSource](../objects/datasource-element-assl.md) elemento.|  
|[Tipo de datos CubeDimension &#40;ASSL&#41;](cubedimension-data-type-assl.md)|Define un tipo de datos primitivo que representa la relación existente entre una dimensión y un cubo.|  
|[Tipo de datos CubeDimensionBinding &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|Define un tipo de datos derivado que representa el enlace de un [dimensión](../objects/dimension-element-assl.md), [medida](../objects/measure-element-assl.md), o [MiningModel](../objects/miningmodel-element-assl.md) elemento a una dimensión de cubo.|  
|[Tipo de datos CubeDimensionPermission &#40;ASSL&#41;](permission-data-type-assl.md)|Define un tipo de datos primitivo que representa los permisos para un único rol en una dimensión concreta de un cubo.|  
|[Tipo de datos CubeHierarchy &#40;ASSL&#41;](hierarchy-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre un [jerarquía](../objects/hierarchy-element-assl.md) elemento en un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de datos DataBlock &#40;ASSL&#41;](datablock-data-type-assl.md)|Define un tipo de datos primitivo que representa una colección de bloques de datos que se utiliza para almacenar el contenido binario de un [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) elemento.|  
|[Tipo de datos DataItem &#40;ASSL&#41;](dataitem-data-type-assl.md)|Define un tipo de datos primitivo que representa las características relacionadas con datos de un elemento de datos, como una columna o un atributo.|  
|[Tipo de datos Miningmeasuregroupdimension &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|Define un tipo de datos derivado que representa la relación entre un grupo de medida y una dimensión de minería de datos.|  
|[Tipo de datos de origen de datos &#40;ASSL&#41;](datasource-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa un origen de datos en un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Tipo de datos DataSourceViewBinding &#40;ASSL&#41;](datasourceviewbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace entre una vista del origen de datos y el elemento primario.|  
|[Tipo de datos DegenerateMeasureGroupDimension &#40;ASSL&#41;](degeneratemeasuregroupdimension-data-type-assl.md)|Define un tipo de datos derivado que representa la relación entre una dimensión degenerada (es decir, una dimensión de hechos) y un grupo de medida.|  
|[Tipo de datos de dimensión &#40;ASSL&#41;](dimension-data-type-assl.md)|Define un tipo de datos primitivo que representa una dimensión de base de datos.|  
|[Tipo de datos DimensionAttribute &#40;ASSL&#41;](dimensionattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa un atributo de una dimensión.|  
|[Tipo de datos DimensionBinding &#40;ASSL&#41;](dimensionbinding-data-type-assl.md)|Define un tipo de datos derivado que representa el enlace entre un origen de datos y un [dimensión](../objects/dimension-element-assl.md) elemento.|  
|[Tipo de datos DimensionPermission &#40;ASSL&#41;](permission-data-type-assl.md)|Define un tipo de datos derivado que representa los permisos asignados a una dimensión de la base de datos.|  
|[Tipo de Drillthroughaction &#40;ASSL&#41;](drillthroughaction-data-type-assl.md)|Define un tipo de datos derivado que representa una acción de obtención de detalles.|  
|[Tipo de datos DSVTableBinding &#40;ASSL&#41;](tablebinding-data-type-assl.md)|Define un tipo de datos derivado que representa el enlace entre una tabla y un [DataSourceView](../objects/datasourceview-element-assl.md) elemento.|  
|[Tipo de datos EventColumn &#40;ASSL&#41;](eventcolumn-data-type-assl.md)|Define un tipo de datos primitivo que representa una columna de información que va a capturar para un [eventos](../objects/event-element-assl.md) elemento como parte de un [seguimiento](../objects/trace-element-assl.md) elemento.|  
|[Tipo de datos de jerarquía &#40;ASSL&#41;](hierarchy-data-type-assl.md)|Define un tipo de datos primitivo que representa una jerarquía en una dimensión.|  
|[Tipo de datos ImpersonationInfo &#40;ASSL&#41;](impersonationinfo-data-type-assl.md)|Define un tipo de datos primitivo que representa la información que se utiliza para suplantar a un usuario.|  
|[Tipo de datos IncrementalProcessingNotification &#40;ASSL&#41;](incrementalprocessingnotification-data-type-assl.md)|Define un tipo de datos derivado que representa la información de la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar el progreso del procesamiento incremental.|  
|[Tipo de datos InheritedBinding &#40;ASSL&#41;](inheritedbinding-data-type-assl.md)|Define un tipo de datos derivado que indica que un [MeasureGroupAttribute](measuregroupattribute-data-type-assl.md) elemento hereda sus enlaces del atributo.|  
|[Tipo de datos ManyToManyMeasureGroupDimension &#40;ASSL&#41;](manytomanymeasuregroupdimension-data-type-assl.md)|Define un tipo de datos derivado que representa la relación entre una dimensión varios a varios y un grupo de medida.|  
|[Tipo de datos MeasureBinding &#40;ASSL&#41;](measurebinding-data-type-assl.md)|Define un tipo de datos derivado que representa al enlace de una medida con el elemento primario.|  
|[Tipo de datos MeasureGroupAttribute &#40;ASSL&#41;](measuregroupattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa la relación entre un atributo y un grupo de medida.|  
|[Tipo de datos MeasureGroupBinding &#40;ASSL&#41;](measuregroupbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace a un [MeasureGroup](../objects/group-element-assl.md) elemento.|  
|[Tipo de datos MeasureGroupBinding &#40;fuera de línea&#41; &#40;ASSL&#41;](measuregroupbinding-data-type-out-of-line-assl.md)|Define un tipo de datos primitivo que representa a un enlace con un grupo de medida.|  
|[Tipo de datos MeasureGroupDimension &#40;ASSL&#41;](measuregroupdimension-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa la relación existente entre una dimensión y un grupo de medida.|  
|[Tipo de datos MeasureGroupDimensionBinding &#40;ASSL&#41;](measuregroupdimensionbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace entre una dimensión y un grupo de medida.|  
|[Tipo de datos MeasureGroupHierarchy &#40;ASSL&#41;](measuregrouphierarchy-data-type-assl.md)|Define un tipo de datos primitivo que representa información acerca de una jerarquía de un grupo de medida.|  
|[Tipo de datos MiningModelColumn &#40;ASSL&#41;](miningmodelcolumn-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una columna de un [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Tipo de datos MiningModelingFlag &#40;ASSL&#41;](miningmodelingflag-data-type-assl.md)|Define un tipo de datos primitivo que representa las marcas de modelado disponibles para un [ModelingFlag](../objects/modelingflag-element-assl.md) elemento.|  
|[Tipo de datos MiningStructureColumn &#40;ASSL&#41;](miningstructurecolumn-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa información sobre una columna de un [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Tipo de datos OlapDataSource &#40;ASSL&#41;](olapdatasource-data-type-assl.md)|Define un tipo de datos derivado que representa un multidimensionales [DataSource](../objects/datasource-element-assl.md) elemento.|  
|[Tipo de datos PartitionBinding &#40;ASSL&#41;](partitionbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace a un [partición](../objects/partition-element-assl.md) elemento.|  
|[Tipo de datos Permission &#40;ASSL&#41;](permission-data-type-assl.md)|Define un tipo de datos primitivo abstracto que representa información acerca de un permiso en particular.|  
|[Tipo de datos PerspectiveAction &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una acción en un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de datos PerspectiveAttribute &#40;ASSL&#41;](perspectiveattribute-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre un atributo en un [PerspectiveDimension](perspectivedimension-data-type-assl.md) elemento.|  
|[Tipo de datos PerspectiveCalculation &#40;ASSL&#41;](perspectivecalculation-data-type-assl.md)|Define un tipo de datos primitivo que representa la relación entre un cálculo y un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de datos PerspectiveDimension &#40;ASSL&#41;](perspectivedimension-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una dimensión en una perspectiva.|  
|[Tipo de datos PerspectiveHierarchy &#40;ASSL&#41;](perspectivehierarchy-data-type-assl.md)|Define un tipo de datos primitivo que representa información acerca de una jerarquía en un [PerspectiveDimension](perspectivedimension-data-type-assl.md) elemento.|  
|[Tipo de datos PerspectiveKpi &#40;ASSL&#41;](perspectivekpi-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre un indicador clave de rendimiento (KPI) en un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de datos PerspectiveMeasure &#40;ASSL&#41;](perspectivemeasure-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre una medida en un [PerspectiveMeasureGroup](perspectivemeasuregroup-data-type-assl.md) elemento.|  
|[Tipo de datos PerspectiveMeasureGroup &#40;ASSL&#41;](perspectivemeasuregroup-data-type-assl.md)|Define un tipo de datos primitivo que representa información sobre un grupo de medida en un [perspectiva](../objects/perspective-element-assl.md) elemento.|  
|[Tipo de datos ProactiveCachingBinding &#40;ASSL&#41;](proactivecachingbinding-data-type-assl.md)|Define un tipo de datos derivado abstracto que representa información para el [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre los cambios de origen de datos que requieren volver a generar la memoria caché o sobre el estado del proceso de regeneración.|  
|[Tipo de datos ProactiveCachingIncrementalProcessingBinding &#40;ASSL&#41;](proactivecachingincrementalprocessingbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace a la [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre el estado del proceso de regeneración de la memoria caché.|  
|[Tipo de datos ProactiveCachingInheritedBinding &#40;ASSL&#41;](proactivecachinginheritedbinding-data-type-assl.md)|Define un tipo de datos derivado que representa información para el [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre los cambios de origen de datos en tablas y vistas, identificados a través de enlaces de datos existentes que requieren volver a generar la memoria caché.|  
|[Tipo de datos ProactiveCachingObjectNotificationBinding &#40;ASSL&#41;](proactivecachingobjectnotificationbinding-data-type-assl.md)|Define un tipo de datos derivado abstracto que representa información para el [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento acerca de los cambios de origen de datos, en tablas y vistas especificadas o en las tablas y vistas, identificados a través de enlaces de datos existentes que requieren volver a generar la memoria caché.|  
|[Tipo de datos ProactiveCachingQueryBinding &#40;ASSL&#41;](querybinding-data-type-assl.md)|Define un tipo de datos derivado que representa información para el [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre los cambios de origen de datos en tablas y vistas, identificados a través de la ejecución de las consultas especificadas que requieren volver a generar la memoria caché.|  
|[Tipo de datos ProactiveCachingTablesBinding &#40;ASSL&#41;](proactivecachingtablesbinding-data-type-assl.md)|Define un tipo de datos derivado que representa información para el [ProactiveCaching](../objects/proactivecaching-element-assl.md) elemento sobre los cambios de origen de datos en tablas y vistas que requieren volver a generar la memoria caché especificadas.|  
|[Tipo de datos PushedDataSource &#40;ASSL&#41;](pusheddatasource-data-type-assl.md)|Define un tipo de datos primitivo que representa un origen de datos (como un [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] paquete) utilizado para "Insertar" datos en un [cubo](../objects/cube-element-assl.md) elemento.|  
|[Tipo de datos QueryBinding &#40;ASSL&#41;](querybinding-data-type-assl.md)|Define un tipo de datos derivado que representa la asociación de un [DataSource](../objects/datasource-element-assl.md) elemento con un [QueryDefinition](../properties/querydefinition-element-assl.md) elemento.|  
|[Tipo de datos ReferenceMeasureGroupDimension &#40;ASSL&#41;](referencemeasuregroupdimension-data-type-assl.md)|Define un tipo de datos derivado que representa una dimensión indirectamente relacionada con la tabla de hechos a través de una dimensión intermedia. (Por ejemplo, un grupo de medidas Sales puede hacer referencia a una dimensión Geography, que se relaciona a través de la dimensión Customer).|  
|[Tipo de datos RegularMeasureGroupDimension &#40;ASSL&#41;](regularmeasuregroupdimension-data-type-assl.md)|Define un tipo de datos derivado que representa una relación normal entre una dimensión y un grupo de medida.|  
|[Tipo de datos RelationalDataSource &#40;ASSL&#41;](relationaldatasource-data-type-assl.md)|Define un tipo de datos derivado que representa un [DataSource](../objects/datasource-element-assl.md) elemento basado en un origen de datos relacional.|  
|[Tipo de datos ReportAction &#40;ASSL&#41;](reportaction-data-type-assl.md)|Define un tipo de datos derivado que representa una acción que genera un informe de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Tipo de datos RowBinding &#40;ASSL&#41;](rowbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace a las filas de una tabla en una [DataSourceView](../objects/datasourceview-element-assl.md) elemento.|  
|[Tipo de datos ScalarMiningStructureColumn &#40;ASSL&#41;](scalarminingstructurecolumn-data-type-assl.md)|Define un tipo de datos derivado que representa un [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contiene valores escalares, a diferencia de las tablas anidadas asociadas a la [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md) elemento que contiene tablas anidadas.|  
|[Tipo de datos StandardAction &#40;ASSL&#41;](standardaction-data-type-assl.md)|Define un tipo de datos derivado que representa cualquier [acción](../objects/action-element-assl.md) elemento que no sea un [DrillThroughAction](drillthroughaction-data-type-assl.md) elemento o un [ReportAction](reportaction-data-type-assl.md) elemento.|  
|[Tipo de datos TableBinding &#40;ASSL&#41;](tablebinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace con una tabla.|  
|[Tipo de datos TableMiningStructureColumn &#40;ASSL&#41;](tableminingstructurecolumn-data-type-assl.md)|Define un tipo de datos derivado que representa un [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contiene tablas anidadas, a diferencia de los valores escalares asociados con la [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) elemento contiene los valores escalares.|  
|[Tipo de datos TabularBinding &#40;ASSL&#41;](tabularbinding-data-type-assl.md)|Define un tipo de datos derivado abstracto que representa un enlace con un elemento tabular, como una tabla o una dimensión de cubo.|  
|[Tipo de datos TimeAttributeBinding &#40;ASSL&#41;](timebinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace "marcador de posición" para los elementos de datos generados en una dimensión de tiempo del  servidor, como pueden ser las columnas de clave de un atributo.|  
|[Tipo de datos TimeBinding &#40;ASSL&#41;](timebinding-data-type-assl.md)|Define un tipo de datos derivado que representa un enlace a los periodos de tiempo.|  
|[Tipo de datos Translation &#40;ASSL&#41;](translation-data-type-assl.md)|Define un tipo de datos primitivo que representa una traducción adaptada.|  
|[Tipo de datos UserDefinedGroupBinding &#40;ASSL&#41;](userdefinedgroupbinding-data-type-assl.md)|Define un tipo de datos derivado que representa un agrupamiento definido por el usuario de un atributo.|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía Analysis Services Scripting Language XML elemento &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  