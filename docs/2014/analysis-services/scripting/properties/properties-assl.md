---
title: Propiedades (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6371a751cdd5a4d647b781373ab74629103e0c44
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061405"
---
# <a name="properties-assl"></a>Propiedades (ASSL)
  Esta sección de referencia contiene información sobre sintaxis y utilización de cada uno de los elementos que actúan como una propiedad de objeto en el esquema del lenguaje de scripting de Analysis Services (ASSL).  
  
 Aunque el esquema ASSL solamente contiene elementos XML, del punto de vista de un programador, los elementos descritos en esta sección se corresponden con las propiedades que describen objetos.  
  
 Las propiedades son elementos en el nivel de hoja en el esquema ASSL, pero no tienen elementos secundarios o elementos que se correspondan con propiedades suyas.  
  
 En algunos casos, un elemento en el nivel de hoja en el esquema que pueda parecer una propiedad se clasifica como objeto, porque el tipo del elemento es un tipo de objeto. Por ejemplo, el `Source` de un objeto `Dimension` el de tipo `DimensionBinding`.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Obtener acceso a elemento &#40;ASSL&#41;](access-element-assl.md)|Indica el nivel de acceso dado a un [CellPermission](../objects/cellpermission-element-assl.md) elemento.|  
|[Elemento de la cuenta &#40;ImpersonationInfo&#41; &#40;ASSL&#41;](account-element-impersonationinfo-assl.md)|Contiene el nombre de la cuenta de usuario para el [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) tipo de datos.|  
|[Elemento AccountType &#40;ASSL&#41;](accounttype-element-assl.md)|Contiene el nombre de un tipo de cuenta definido en un [base de datos](../objects/database-element-assl.md) elemento.|  
|[Elemento ActionID &#40;ASSL&#41;](id-element-assl.md)|Contiene el nombre de un [acción](../objects/action-element-assl.md) elemento definido en un [cubo](../objects/cube-element-assl.md) elemento que está disponible en un [perspectiva](../objects/perspective-element-assl.md) elemento como un [PerspectiveAction](../data-type/action-data-type-assl.md) elemento.|  
|[Elemento Administer &#40;ASSL&#41;](administer-element-assl.md)|Indica si el permiso asociado incluye el derecho a administrar un elemento `Database`.|  
|[Elemento AggregateFunction &#40;ASSL&#41;](aggregatefunction-element-assl.md)|Define el tipo de función de agregado utilizado por un [medida](../objects/measure-element-assl.md) elemento.|  
|[Elemento AggregationDesignID &#40;ASSL&#41;](aggregationdesignid-element-assl.md)|Identifica el [AggregationDesign](../objects/aggregationdesign-element-assl.md) elemento asociado con el [partición](../objects/partition-element-assl.md) elemento.|  
|[Elemento AggregationFunction &#40;ASSL&#41;](aggregationfunction-element-assl.md)|Contiene la función de agregación que se usará para el tipo de cuenta.|  
|[Elemento AggregationID &#40;ASSL&#41;](aggregationid-element-assl.md)|Identifica la definición de agregación del elemento `AggregationDesign` utilizada para crear la instancia de agregación.|  
|[Elemento AggregationInstanceSource &#40;ASSL&#41;](aggregationinstancesource-element-assl.md)|Identifica el origen de datos para las instancias de agregación definidas por el usuario enlazadas a un elemento  `Partition`.|  
|[Elemento AggregationPrefix &#40;ASSL&#41;](aggregationprefix-element-assl.md)|Define el prefijo común que se va a utilizar para los nombres de la agregación en el elemento primario asociado.|  
|[Elemento AggregationStorage &#40;ASSL&#41;](aggregationstorage-element-assl.md)|Identifica el método de almacenamiento para las agregaciones.|  
|[Elemento AggregationType &#40;ASSL&#41;](aggregationtype-element-assl.md)|Define el tipo de agregación almacenado por el elemento `Partition`.|  
|[Elemento AggregationUsage &#40;ASSL&#41;](aggregationusage-element-assl.md)|Controles de cómo el Diseñador de agregaciones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diseña las agregaciones.|  
|[Elemento Algorithm &#40;ASSL&#41;](algorithm-element-assl.md)|Define el algoritmo utilizado por un [MiningModel](../objects/miningmodel-element-assl.md) elemento.|  
|[Elemento alias &#40;ASSL&#41;](alias-element-assl.md)|Define un alias para un [cuenta](../objects/account-element-assl.md) elemento.|  
|[Elemento AllMemberAggregationUsage &#40;ASSL&#41;](allmemberaggregationusage-element-assl.md)|Controla cómo diseña las agregaciones el Diseñador de agregaciones de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento AllMemberName &#40;ASSL&#41;](name-element-assl.md)|Contiene el título en el idioma predeterminado para el miembro All de un [jerarquía](../objects/hierarchy-element-assl.md) elemento.|  
|[Elemento AllowBrowsing &#40;ASSL&#41;](allowbrowsing-element-assl.md)|Define si los miembros de un [rol](../objects/role-element-assl.md) elemento tiene el permiso de exploración en un `MiningModel` elemento.|  
|[Elemento AllowDrillThrough &#40;ASSL&#41;](allowdrillthrough-element-assl.md)|Determina si se permite la obtención de detalles para el elemento primario.|  
|[Elemento AllowDuplicateNames &#40;ASSL&#41;](allowduplicatenames-element-assl.md)|Determina si se permiten nombres duplicados en un elemento `Hierarchy`.|  
|[Elemento AllowedSet &#40;ASSL&#41;](allowedset-element-assl.md)|Contiene una expresión de conjunto que define el conjunto de permisos concedidos para un elemento `Role` en un atributo.|  
|[Elemento de la aplicación &#40;ASSL&#41;](application-element-assl.md)|Identifica a la aplicación asociada con un elemento `Action`.|  
|[Elemento AssociatedMeasureGroupID &#40;ASSL&#41;](measuregroupid-element-assl.md)|Contiene el identificador (ID) de la [MeasureGroup](../objects/group-element-assl.md) elemento asociado con un [CalculationProperty](../objects/calculationproperty-element-assl.md) elemento o un [Kpi](../objects/kpi-element-assl.md) elemento.|  
|[Elemento AttributeAllMemberName &#40;ASSL&#41;](attributeallmembername-element-assl.md)|Contiene el título en el idioma predeterminado para el miembro All de la dimensión.|  
|[Elemento AttributeHierarchyDisplayFolder &#40;ASSL&#41;](displayfolder-element-assl.md)|Identifica la carpeta en la que se va a mostrar la jerarquía de atributos asociada.|  
|[Elemento AttributeHierarchyEnabled &#40;ASSL&#41;](enabled-element-assl.md)|Determina si una jerarquía de atributos está habilitada para el atributo.|  
|[Elemento AttributeHierarchyOptimizedState &#40;ASSL&#41;](state-element-assl.md)|Determina el nivel de optimización aplicado a la jerarquía de atributos.|  
|[Elemento AttributeHierarchyOrdered &#40;ASSL&#41;](attributehierarchyordered-element-assl.md)|Determina si la jerarquía de atributos asociada está ordenada.|  
|[Elemento AttributeHierarchyVisible &#40;ASSL&#41;](visible-element-assl.md)|Determina si la jerarquía de atributos es visible para las aplicaciones cliente.|  
|[Elemento AttributeID &#40;ASSL&#41;](attributeid-element-assl.md)|Contiene el Id. del atributo asociado al elemento primario.|  
|[Elemento de auditoría &#40;ASSL&#41;](audit-element-assl.md)|Especifica que un [seguimiento](../objects/trace-element-assl.md) elemento no puede quitar cualquier evento, aún cuando esto produce una reducción del rendimiento en el servidor.|  
|[Elemento AutoRestart &#40;ASSL&#41;](autorestart-element-assl.md)|Determina si un elemento `Trace` se debería reiniciar automáticamente si el servicio [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se detiene y se reinicia.|  
|[Elemento BackColor &#40;ASSL&#41;](backcolor-element-assl.md)|Describe las características de presentación del elemento principal relacionadas con el color.|  
|[Elemento CacheMode &#40;ASSL&#41;](cachemode-element-assl.md)|Determina el mecanismo de almacenamiento en caché utilizado para los datos de aprendizaje recuperados al procesar una estructura de minería de datos.|  
|[Elemento CalculationReference &#40;ASSL&#41;](calculationreference-element-assl.md)|Contiene el nombre del conjunto con nombre o de la celda calculada al que hace referencia el elemento `CalculationProperty`.|  
|[Elemento CalculationType &#40;ASSL&#41;](calculationtype-element-assl.md)|Describe el tipo de cálculo definido en el elemento `CalculationProperty` asociado.|  
|[Elemento CalendarEndDate &#40;ASSL&#41;](calendarenddate-element-assl.md)|Define la fecha de finalización del período del calendario para un [TimeBinding](../data-type/binding-data-type-assl.md) elemento.|  
|[Elemento CalendarLanguage &#40;ASSL&#41;](language-element-assl.md)|Define el lenguaje del calendario utilizado para el elemento `TimeBinding`.|  
|[Elemento CalendarStartDate &#40;ASSL&#41;](calendarstartdate-element-assl.md)|Define la fecha de inicio del período del calendario para el elemento `TimeBinding`.|  
|[Elemento de leyenda &#40;ASSL&#41;](caption-element-assl.md)|Contiene el título del elemento primario asociado.|  
|[Elemento CaptionIsMdx &#40;ASSL&#41;](captionismdx-element-assl.md)|Define si el título para del elemento `Action` es una expresión del tipo Expresiones multidimensionales (MDX).|  
|[Elemento Cardinality &#40;ASSL&#41;](cardinality-element-assl.md)|Indica la cardinalidad de la relación descrita por un [AttributeRelationship](../objects/attributerelationship-element-assl.md) o [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md).|  
|[Elemento CaseCubeDimensionID &#40;ASSL&#41;](dimensionid-element-assl.md)|Contiene el Id. de la dimensión de cubo que relaciona la dimensión de la minería de datos con el grupo de medida.|  
|[Elemento ClassifiedColumnID &#40;ASSL&#41;](classifiedcolumnid-element-assl.md)|Contiene el identificador de una columna relacionada clasificada por el [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Elemento Collation &#40;ASSL&#41;](collation-element-assl.md)|Determina la intercalación utilizada por el elemento primario.|  
|[Elemento ColumnID &#40;ColumnBinding&#41; &#40;ASSL&#41;](columnid-element-columnbinding-assl.md)|Contiene el Id. de la columna de la tabla a la que se enlaza el elemento de datos.|  
|[Elemento ColumnID &#40;EventColumn&#41; &#40;ASSL&#41;](columnid-element-eventcolumn-assl.md)|Contiene el Id. de la columna de información que se va a capturar para un evento como parte de un elemento `Trace`.|  
|[Elemento de condición &#40;ASSL&#41;](condition-element-assl.md)|Contiene una expresión MDX que determina si el elemento primario `Action` se aplica al destino.|  
|[Elemento ConnectionString &#40;ASSL&#41;](connectionstring-element-assl.md)|Contiene la cadena de conexión cifrada para un [DataSource](../objects/datasource-element-assl.md) elemento.|  
|[Elemento ConnectionStringSecurity &#40;ASSL&#41;](connectionstringsecurity-element-assl.md)|Especifica si la contraseña del usuario se extrae de la cadena de conexión a un origen de datos por temas de seguridad.|  
|[Elemento de contenido &#40;ASSL&#41;](content-element-assl.md)|Describe el contenido de la columna en la [MiningStructure](../objects/miningstructure-element-assl.md) elemento.|  
|[Elemento CreatedTimestamp &#40;ASSL&#41;](createdtimestamp-element-assl.md)|Contiene la marca de tiempo de creación de solo lectura del elemento primario.|  
|[Elemento CubeDimensionID &#40;ASSL&#41;](cubedimensionid-element-assl.md)|Identifica el [CubeDimension](../data-type/cubedimension-data-type-assl.md) asociado con el elemento primario del elemento.|  
|[Elemento CubeID &#40;ASSL&#41;](cubeid-element-assl.md)|Identifica el `Cube` elemento asociado con un [enlace](../data-type/binding-data-type-assl.md) elemento.|  
|[Elemento CurrentStorageMode &#40;ASSL&#41;](storagemode-element-assl.md)|Determina el modo de almacenamiento actual para el elemento primario.|  
|[Elemento CurrentTimeMember &#40;ASSL&#41;](../objects/member-element-assl.md)|Define el miembro actual de una dimensión de tiempo asociada a un elemento `Kpi`.|  
|[Elemento DataAggregation &#40;ASSL&#41;](../objects/aggregation-element-assl.md)|Determina si la instancia puede agregar datos persistentes o datos almacenados en caché para el `MeasureGroup`.|  
|[Elemento DatabaseID &#40;ASSL&#41;](databaseid-element-assl.md)|Identifica el elemento `Database` asociado con un elemento fuera de línea `Binding`.|  
|[Elemento DataSize &#40;ASSL&#41;](datasize-element-assl.md)|Contiene el tamaño en bytes de un [DataItem](../data-type/dataitem-data-type-assl.md) elemento.|  
|[Elemento DataSourceID &#40;ASSL&#41;](datasourceid-element-assl.md)|Identifica el elemento `DataSource` asociado con el elemento primario.|  
|[Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)|Contiene información utilizada para determinar el comportamiento de la suplantación al conectarse con el origen de datos para un elemento `Database`.|  
|[Elemento DataSourceViewID &#40;ASSL&#41;](datasourceviewid-element-assl.md)|Identifica el [DataSourceView](../objects/datasourceview-element-assl.md) elemento asociado con el `Binding` elemento primario.|  
|[Elemento DataType &#40;ASSL&#41;](datatype-element-assl.md)|Define el tipo de datos del elemento asociado.|  
|[Elemento DbSchemaName &#40;ASSL&#41;](dbschemaname-element-assl.md)|Contiene el nombre del esquema utilizado por el elemento primario de la tabla identificada por el [DbTableName](dbtablename-element-assl.md) elemento.|  
|[Elemento DbTableName &#40;ASSL&#41;](dbtablename-element-assl.md)|Contiene el nombre de la tabla a la que se enlaza el elemento primario.|  
|[Default elemento &#40;ASSL&#41;](default-element-assl.md)|Determina si `DrillThroughAction` es la acción de obtención de detalles predeterminada.|  
|[Elemento DefaultMeasure &#40;ASSL&#41;](defaultmeasure-element-assl.md)|Contiene una expresión de lenguaje MDX que define la medida predeterminada para el elemento `Cube` o `Perspective`.|  
|[Elemento DefaultMember &#40;ASSL&#41;](defaultmember-element-assl.md)|Contiene una expresión MDX que identifica al miembro predeterminado del elemento primario.|  
|[Elemento DefaultScript &#40;ASSL&#41;](defaultscript-element-assl.md)|Identifica el valor predeterminado [MdxScript](../objects/mdxscript-element-assl.md) elemento en el [MdxScripts](../collections/mdxscripts-element-assl.md) colección.|  
|[Elemento DefaultValue &#40;ASSL&#41;](value-element-assl.md)|Contiene el valor predeterminado de solo lectura de asociado [ServerProperty](../objects/serverproperty-element-assl.md) elemento.|  
|[Elemento DeniedSet &#40;ASSL&#41;](deniedset-element-assl.md)|Contiene una expresión de conjunto que define la lista de permisos que se deniegan en el atributo asociado.|  
|[Elemento DependsOnDimensionID &#40;ASSL&#41;](dependsondimensionid-element-assl.md)|Contiene el Id. de otra dimensión de la que depende la dimensión primaria.|  
|[Elemento Description &#40;ASSL&#41;](description-element-assl.md)|Contiene la descripción del elemento primario.|  
|[Elemento DimensionID &#40;ASSL&#41;](dimensionid-element-assl.md)|Contiene el Id. de la dimensión.|  
|[Elemento DiscretizationBucketCount &#40;ASSL&#41;](discretizationbucketcount-element-assl.md)|Contiene el número de depósitos en los que discretizar.|  
|[Elemento DiscretizationMethod &#40;ASSL&#41;](discretizationmethod-element-assl.md)|Define el método que se va a utilizar para la discretización.|  
|[Elemento DisplayFlag &#40;ASSL&#41;](displayflag-element-assl.md)|Contiene una sugerencia de solo lectura que indica si los componentes de la interfaz de usuario deben mostrar el elemento `ServerProperty` asociado.|  
|[Elemento DisplayFolder &#40;ASSL&#41;](displayfolder-element-assl.md)|Especifica la carpeta en la que se enumerará el elemento primario. Las aplicaciones para desarrolladores y administradores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pueden admitir el uso de carpetas para mostrar con el fin de categorizar visualmente múltiples elementos.|  
|[Elemento Distribution &#40;ASSL&#41;](distribution-element-assl.md)|Contiene un valor específico del proveedor que describe cómo los valores escalares se distribuyen dentro de una columna de un elemento `MiningStructure`.|  
|[Elemento Edition &#40;ASSL&#41;](edition-element-assl.md)|Contiene la edición de solo lectura de la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] representado por la [Server](../objects/server-element-assl.md) elemento.|  
|[Habilita el elemento &#40;ASSL&#41;](enabled-element-assl.md)|Indica si el elemento primario está habilitado.|  
|[Elemento EndOfData &#40;ASSL&#41;](../objects/data-element-assl.md)|Indica el final de los datos recibidos desde un [PushedDataSource](../data-type/datasource-data-type-assl.md) elemento.|  
|[Elemento EstimatedCount &#40;ASSL&#41;](estimatedcount-element-assl.md)|Contiene el número estimado de miembros para un atributo.|  
|[Elemento EstimatedPerformanceGain &#40;ASSL&#41;](estimatedperformancegain-element-assl.md)|Contiene el porcentaje, de solo lectura, de ganancia de rendimiento estimada para la partición.|  
|[Elemento EstimatedRows &#40;ASSL&#41;](estimatedrows-element-assl.md)|Contiene el número estimado de filas representadas por el elemento primario.|  
|[Elemento EstimatedSize &#40;ASSL&#41;](estimatedsize-element-assl.md)|Contiene el tamaño estimado de solo lectura, en bytes, del elemento principal.|  
|[Elemento EventID &#40;ASSL&#41;](eventid-element-assl.md)|Identifica de forma única un [eventos](../objects/event-element-assl.md) elemento que se debe capturar como parte de un `Trace` elemento.|  
|[Elemento de expresión &#40;ASSL&#41;](expression-element-assl.md)|Contiene una expresión MDX que define el contenido del elemento primario.|  
|[Elemento Filter &#40;enlace&#41; &#40;ASSL&#41;](filter-element-binding-assl.md)|Contiene una expresión MDX que filtra el contenido del elemento primario.|  
|[Elemento Filter &#40;seguimiento&#41; &#40;ASSL&#41;](filter-element-trace-assl.md)|Contiene un fragmento del documento XML que describe al filtro `Trace`.|  
|[Elemento FirstDayOfWeek &#40;ASSL&#41;](firstdayofweek-element-assl.md)|Define el primer día de la semana para un elemento `TimeBinding`.|  
|[Elemento FiscalFirstDayOfMonth &#40;ASSL&#41;](fiscalfirstdayofmonth-element-assl.md)|Define el primer día del mes fiscal para un elemento `TimeBinding`.|  
|[Elemento FiscalFirstMonth &#40;ASSL&#41;](fiscalfirstmonth-element-assl.md)|Define el primer mes del periodo fiscal para un elemento `TimeBinding`.|  
|[Elemento FiscalYearName &#40;ASSL&#41;](fiscalyearname-element-assl.md)|Define la convención de nomenclatura del nombre del año fiscal para un elemento `TimeBinding`.|  
|[Elemento FontFlags &#40;ASSL&#41;](fontflags-element-assl.md)|Describe las características de presentación del elemento principal `CalculationProperty` o `Measure` relacionadas con la fuente.|  
|[Elemento FontName &#40;ASSL&#41;](fontname-element-assl.md)|Describe las características de presentación del elemento principal `CalculationProperty` o `Measure` relacionadas con la fuente.|  
|[Elemento FontSize &#40;ASSL&#41;](fontsize-element-assl.md)|Describe las características de presentación del elemento principal `CalculationProperty` o `Measure` relacionadas con la fuente.|  
|[Elemento ForceRebuildInterval &#40;ASSL&#41;](forcerebuildinterval-element-assl.md)|Determina la cantidad de tiempo, a partir del momento en que una nueva imagen OLAP multidimensional (MOLAP) queda disponible, tras el que la creación de imágenes MOLAP se inicia incondicionalmente.|  
|[Elemento ForeColor &#40;ASSL&#41;](forecolor-element-assl.md)|Describe las características de presentación del elemento principal `CalculationProperty` o `Measure` relacionadas con el color.|  
|[Elemento de formato &#40;ASSL&#41;](format-element-assl.md)|Contiene el formato requerido del elemento `DataItem`.|  
|[Elemento FormatString &#40;ASSL&#41;](formatstring-element-assl.md)|Describe el formato de presentación para un elemento `CalculationProperty` o un elemento `Measure`.|  
|[Elemento goal &#40;ASSL&#41;](goal-element-assl.md)|Identifica el objetivo deseado en un elemento `Kpi`.|  
|[Elemento GranularityAttributeID &#40;ASSL&#41;](granularityattributeid-element-assl.md)|Contiene el identificador del atributo asociado al elemento primario [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md) tipo de datos.|  
|[Elemento HideMemberIf &#40;ASSL&#41;](hidememberif-element-assl.md)|Indica si un miembro en un nivel debe ocultarse de las aplicaciones cliente y cuándo.|  
|[Elemento HierarchyID &#40;ASSL&#41;](hierarchyid-element-assl.md)|Contiene el identificador para un [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md), o [PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md) elemento.|  
|[Elemento HierarchyUniqueNameStyle &#40;ASSL&#41;](hierarchyuniquenamestyle-element-assl.md)|Determina cómo se generan los nombres únicos para las jerarquías contenidas en la `CubeDimension`.|  
|[Id. de elemento &#40;ASSL&#41;](id-element-assl.md)|Contiene el Id. único del elemento primario.|  
|[Elemento IgnoreUnrelatedDimensions &#40;ASSL&#41;](../collections/dimensions-element-assl.md)|Determina si las dimensiones no relacionadas están forzadas a su nivel superior cuando los miembros de las dimensiones que no están relacionadas con el grupo de medida se incluyen en una consulta.|  
|[Elemento ImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)|Contiene la información que se utiliza para determinar el comportamiento de suplantación al obtener acceso un ensamblado, o al ejecutarlo.|  
|[Elemento ImpersonationInfoSecurity &#40;ASSL&#41;](impersonationinfosecurity-element-assl.md)|Contiene un valor de solo lectura que indica si se realizó cualquier cambio en las credenciales de seguridad que se proporcionan en el tipo de datos `ImpersonationInfo`.|  
|[Elemento ImpersonationMode &#40;ASSL&#41;](impersonationmode-element-assl.md)|Contiene un valor que indica el método de suplantación para los elementos que se derivan del tipo de datos `ImpersonationInfo`.|  
|[Elemento InstanceSelection &#40;ASSL&#41;](instanceselection-element-assl.md)|Proporciona una sugerencia a las aplicaciones cliente acerca de cómo se debe mostrar una lista de elementos, según el número estimado de elementos de la lista.|  
|[Elemento IntermediateCubeDimensionID &#40;ASSL&#41;](intermediatecubedimensionid-element-assl.md)|Contiene el Id. de la dimensión que relaciona una dimensión de referencia con un grupo de medida.|  
|[Elemento IntermediateGranularityAttributeID &#40;ASSL&#41;](intermediategranularityattributeid-element-assl.md)|Contiene el Id. del atributo de granularidad en la dimensión del cubo intermedia que se utiliza para relacionar una dimensión de referencia con una dimensión intermedia.|  
|[Elemento InvalidXmlCharacters &#40;ASSL&#41;](invalidxmlcharacters-element-assl.md)|Especifica el método de control para los caracteres XML de los datos de origen que no son válidos.|  
|[Elemento Invocation &#40;ASSL&#41;](invocation-element-assl.md)|Especifica cómo se debería invocar una `Action`.|  
|[Elemento IsAggregatable &#40;ASSL&#41;](isaggregatable-element-assl.md)|Especifica si los valores de la [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md) se puede agregar el elemento.|  
|[Elemento IsKey &#40;ASSL&#41;](iskey-element-assl.md)|Indica si la columna proporciona la clave para el caso en un elemento `MiningStructure`.|  
|[Elemento Isolation &#40;ASSL&#41;](isolation-element-assl.md)|Indica el nivel de aislamiento para un elemento que se deriva el [DataSource](../data-type/datasource-data-type-assl.md) tipo de datos.|  
|[Elemento KeyDuplicate &#40;ASSL&#41;](keyduplicate-element-assl.md)|Determina cómo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] administra un error de clave duplicada en caso de encontrarla durante el procesamiento.|  
|[Elemento KeyErrorAction &#40;ASSL&#41;](keyerroraction-element-assl.md)|Especifica la acción que llevará a cabo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cuando se produzca un error en una clave.|  
|[Elemento KeyErrorLimit &#40;ASSL&#41;](keyerrorlimit-element-assl.md)|Contiene el número de errores aceptable durante el procesamiento.|  
|[Elemento KeyErrorLimitAction &#40;ASSL&#41;](keyerrorlimitaction-element-assl.md)|Especifica la acción que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] lleva a cabo cuando el recuento de los errores de clave que se especifica en el [KeyErrorLimit](keyerrorlimit-element-assl.md) alcanza el elemento.|  
|[Elemento KeyErrorLogFile &#40;ASSL&#41;](../objects/file-element-assl.md)|Contiene el nombre de archivo para registrar los errores de procesamiento.|  
|[Elemento KeyNotFound &#40;ASSL&#41;](keynotfound-element-assl.md)|Especifica cómo responde [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cuando encuentra un error de integridad referencial.|  
|[Elemento KeyUniquenessGuarantee &#40;ASSL&#41;](keyuniquenessguarantee-element-assl.md)|Indica si se garantiza la validez de la relación entre la clave de atributo y su nombre y la relación con los atributos relacionados.|  
|[Elemento KpiID &#40;ASSL&#41;](kpiid-element-assl.md)|Contiene un Id. que asocia un elemento `Kpi` con un elemento `Perspective`.|  
|[Elemento de lenguaje &#40;ASSL&#41;](language-element-assl.md)|Contiene el identificador de lenguaje del elemento primario.|  
|[Elemento LastProcessed &#40;ASSL&#41;](lastprocessed-element-assl.md)|Contiene la marca de tiempo de solo lectura que indica cuándo se procesó por última vez la base de datos que contiene el elemento primario.|  
|[Elemento LastSchemaUpdate &#40;ASSL&#41;](lastschemaupdate-element-assl.md)|Contiene los metadatos de la marca de tiempo de actualización de solo lectura del elemento primario.|  
|[Elemento LastUpdate &#40;ASSL&#41;](lastupdate-element-assl.md)|Contiene una marca de tiempo de solo lectura que indica la última vez que se modificaron la `Database` asociada o cualquiera de los objetos principales que la base de datos contiene.|  
|[Elemento latency &#40;ASSL&#41;](latency-element-assl.md)|Define el "período de gracia" entre la notificación más antigua y el momento en el que se destruyen las imágenes MOLAP.|  
|[Elemento LogFileAppend &#40;ASSL&#41;](logfileappend-element-assl.md)|Determina si el elemento `Trace` anexa la salida de su registro al archivo de registro existente, o lo sobrescribe.|  
|[Elemento LogFileName &#40;ASSL&#41;](logfilename-element-assl.md)|Contiene el nombre del archivo de registro para el elemento `Trace`.|  
|[Elemento LogFileRollover &#40;ASSL&#41;](logfilerollover-element-assl.md)|Especifica si el registro de `Trace` salida debería escribirse en un archivo nuevo o debería detenerse en el archivo de registro máximo tamaño especificado en [LogFileSize](logfilesize-element-assl.md) se alcanza.|  
|[Elemento LogFileSize &#40;ASSL&#41;](logfilesize-element-assl.md)|Especifica el tamaño máximo del archivo de registro, en megabytes.|  
|[Elemento ManagedProvider &#40;ASSL&#41;](managedprovider-element-assl.md)|Contiene el nombre del proveedor administrado que utiliza un elemento que se deriva del tipo de datos `DataSource`.|  
|[Elemento ManufacturingExtraMonthQuarter &#40;ASSL&#41;](manufacturingextramonthquarter-element-assl.md)|Define el mes del período de fabricación al que se asigna un mes adicional para un elemento `TimeBinding`.|  
|[Elemento ManufacturingFirstMonth &#40;ASSL&#41;](manufacturingfirstmonth-element-assl.md)|Define el primer mes de fabricación para un elemento `TimeBinding`.|  
|[Elemento ManufacturingFirstWeekOfMonth &#40;ASSL&#41;](manufacturingfirstweekofmonth-element-assl.md)|Define la primera semana del mes de fabricación para un elemento `TimeBinding`.|  
|[Elemento MasterDatasourceID &#40;ASSL&#41;](masterdatasourceid-element-assl.md)|Contiene el Id. de origen de datos maestro para un elemento `Database`.|  
|[Elemento Materialization &#40;ASSL&#41;](materialization-element-assl.md)|Indica el tipo de relación entre el grupo de medida y la dimensión de referencia.|  
|[Elemento MaxActiveConnections &#40;ASSL&#41;](maxactiveconnections-element-assl.md)|Contiene el número máximo de conexiones simultáneas permitidas por un elemento que se deriva del tipo de datos `DataSource`.|  
|[Elemento MdxMissingMemberMode &#40;ASSL&#41;](mdxmissingmembermode-element-assl.md)|Determina cómo se gestionan los miembros que faltan en instrucciones MDX.|  
|[Elemento MeasureExpression &#40;ASSL&#41;](measureexpression-element-assl.md)|Contiene la expresión MDX que define una medida.|  
|[Elemento MeasureGroupID &#40;ASSL&#41;](measuregroupid-element-assl.md)|Asocia un `MeasureGroup` con el elemento primario, el enlace o el enlace fuera de línea|  
|[Elemento MeasureID &#40;ASSL&#41;](measureid-element-assl.md)|Asocia un elemento `Measure` con el elemento primario.|  
|[Elemento MeasureQualificaton &#40;ASSL&#41;](measurequalificaton-element-assl.md)|Determina si un prefijo se aplica a las medidas del `MeasureGroup`.|  
|[Elemento MemberNamesUnique &#40;ASSL&#41;](membernamesunique-element-assl.md)|Determina si los nombres de los miembros situados por debajo del elemento primario deben ser únicos.|  
|[Elemento MemberUniqueNameStyle &#40;ASSL&#41;](memberuniquenamestyle-element-assl.md)|Determina cómo se generan los nombres únicos para los miembros de las jerarquías contenidas en el elemento `CubeDimension`.|  
|[Elemento MembersWithData &#40;ASSL&#41;](memberswithdata-element-assl.md)|Determina si se van a mostrar los miembros de datos para los miembros no hoja del atributo primario.|  
|[Elemento MembersWithDataCaption &#40;ASSL&#41;](memberswithdatacaption-element-assl.md)|Proporciona una cadena de plantilla utilizada para crear títulos para los miembros de datos generados por el sistema.|  
|[Elemento MimeType &#40;ASSL&#41;](mimetype-element-assl.md)|Contiene el tipo Extensiones multipropósito de correo Internet (MIME), si es aplicable, de los datos representados por el elemento primario `DataItem`.|  
|[Elemento MiningModelID &#40;ASSL&#41;](miningmodelid-element-assl.md)|Asocia un modelo de minería a una dimensión de la minería de datos.|  
|[Nombre de elemento &#40;ASSL&#41;](name-element-assl.md)|Contiene el nombre del elemento primario.|  
|[Elemento NamingTemplate &#40;ASSL&#41;](namingtemplate-element-assl.md)|Define cómo se denominan los niveles en una jerarquía de elementos primarios y secundarios construida a partir del elemento primario `DimensionAttribute`.|  
|[Elemento NonEmptyBehavior &#40;ASSL&#41;](nonemptybehavior-element-assl.md)|Determina el comportamiento de no vacío asociado al elemento primario del elemento `CalculationProperty`.|  
|[Elemento NotificationTechnique &#40;ASSL&#41;](notificationtechnique-element-assl.md)|Especifica si [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o una aplicación cliente externa procesará las notificaciones.|  
|[Elemento NullKeyConvertedToUnknown &#40;ASSL&#41;](nullkeyconvertedtounknown-element-assl.md)|Especifica la acción que se ha de llevar a cabo si se encuentra un error de conversión nulo.|  
|[Elemento NullKeyNotAllowed &#40;ASSL&#41;](nullkeynotallowed-element-assl.md)|Determina cómo gestiona el motor de procesamiento de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] un error clave nula encontrado durante el procesamiento.|  
|[Elemento NullProcessing &#40;ASSL&#41;](nullprocessing-element-assl.md)|Define cómo se procesan los valores nulos.|  
|[Elemento OnlineMode &#40;ASSL&#41;](onlinemode-element-assl.md)|Especifica si la base de datos se devuelve inmediatamente en línea cuando se inicia la nueva generación de la memoria caché o solo cuando esta se haya completado.|  
|[Elemento OptimizedState &#40;ASSL&#41;](state-element-assl.md)|Determina el nivel de optimización que se aplica a la jerarquía.|  
|[Elemento optionality &#40;ASSL&#41;](optionality-element-assl.md)|Indica si los miembros para un elemento `AttributeRelationship` son opcionales o no.|  
|[Elemento OrderBy &#40;ASSL&#41;](orderby-element-assl.md)|Describe cómo ordenar los miembros incluidos en el atributo.|  
|[Elemento OrderByAttributeID &#40;ASSL&#41;](orderbyattributeid-element-assl.md)|Identifica otro atributo por el que se va a ordenar los miembros de la [dimensión](../data-type/dimensionattribute-data-type-assl.md) atributo.|  
|[Elemento ordinal &#40;ASSL&#41;](ordinal-element-assl.md)|Indica el número ordinal al que enlazar en las colecciones, como pueden ser claves y traducciones.|  
|[Elemento OverrideBehavior &#40;ASSL&#41;](overridebehavior-element-assl.md)|Indica el comportamiento de invalidación de la relación descrita por un elemento `AttributeRelationship`.|  
|[Elemento PartitionID &#40;ASSL&#41;](partitionid-element-assl.md)|Asocia un elemento `Partition` con un elemento primario, enlace o enlace fuera de línea|  
|[Elemento de contraseña &#40;ASSL&#41;](password-element-assl.md)|Contiene la contraseña de la cuenta de usuario para el elemento `ImpersonationInfo`.|  
|[Elemento path &#40;ASSL&#41;](path-element-assl.md)|Contiene la ruta de acceso, según lo proporcionado por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], de un informe utilizado por el [ReportAction](../data-type/reportaction-data-type-assl.md) elemento.|  
|[Elemento PendingValue &#40;ASSL&#41;](pendingvalue-element-assl.md)|Contiene el valor pendiente de solo lectura del elemento `ServerProperty` asociado.|  
|[Elemento PermissionSet &#40;ASSL&#41;](permissionset-element-assl.md)|Identifica el conjunto de permisos asociado con un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ensamblado de .NET Framework.|  
|[Elemento Persistence &#40;ASSL&#41;](persistence-element-assl.md)|Determina qué partes de los datos de origen enlazados son dinámicos y se comprueban para las actualizaciones con la frecuencia especificada por el [RefreshPolicy](refreshpolicy-element-assl.md) elemento.|  
|[Procesar el elemento &#40;ASSL&#41;](process-element-assl.md)|Determina si un usuario puede procesar al propietario del elemento primario.|  
|[Elemento ProcessingMode &#40;ASSL&#41;](processingmode-element-assl.md)|Indica si la instancia debe indizar y agregar durante o después del procesamiento.|  
|[Elemento ProcessingPriority &#40;ASSL&#41;](processingpriority-element-assl.md)|Determina la prioridad de procesamiento del objeto primario durante las operaciones en segundo plano, como por ejemplo, la agregación diferida, la indización o la agrupación en clústeres.|  
|[Elemento ProcessingQuery &#40;ASSL&#41;](query-element-assl.md)|Contiene el texto parametrizado de la consulta que se debe ejecutar para la notificación del estado de procesamiento incremental.|  
|[Elemento ProductName &#40;ASSL&#41;](productname-element-assl.md)|Contiene el nombre del producto de solo lectura de la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que está asociada a un elemento `Server`.|  
|[Elemento query &#40;ASSL&#41;](query-element-assl.md)|Contiene el texto de la consulta a ejecutar para la notificación.|  
|[Elemento QueryDefinition &#40;ASSL&#41;](querydefinition-element-assl.md)|Contiene una expresión opaca para una consulta asociada con un `DataSource` elemento en un [QueryBinding](../data-type/querybinding-data-type-assl.md) elemento.|  
|[Leer elemento &#40;ASSL&#41;](read-element-assl.md)|Determina si se pueden leer datos o metadatos para un determinado [CubeDimensionPermission](../data-type/permission-data-type-assl.md) o [permiso](../data-type/permission-data-type-assl.md) elemento.|  
|[Elemento ReadDefinition &#40;ASSL&#41;](readdefinition-element-assl.md)|Determina si los miembros pueden leer la definición de la base de datos o la definición de objetos de la base de datos.|  
|[Elemento ReadSourceData &#40;ASSL&#41;](readsourcedata-element-assl.md)|Determina cómo se generan los nombres únicos para las jerarquías contenidas en la `CubePermission`.|  
|[Elemento RefreshInterval &#40;ASSL&#41;](refreshinterval-element-assl.md)|Especifica el intervalo de tiempo en el que se actualizarán los datos enlazados asociados con el elemento primario.|  
|[Elemento RefreshPolicy &#40;ASSL&#41;](refreshpolicy-element-assl.md)|Determina la frecuencia con la parte dinámica de la dimensión o grupo de medida (según lo especificado por el [persistencia](persistence-element-assl.md) elemento) está activada para los cambios.|  
|[Elemento RelationshipType &#40;ASSL&#41;](relationshiptype-element-assl.md)|Indica si se pueden cambiar las relaciones de miembros para un `AttributeRelationship`.|  
|[Elemento RemoteDatasourceID &#40;ASSL&#41;](remotedatasourceid-element-assl.md)|Especifica el Id. del origen de datos OLAP que señala a la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que almacena la partición remota.|  
|[Elemento ReportingFirstMonth &#40;ASSL&#41;](reportingfirstmonth-element-assl.md)|Define el primer mes de informes para el elemento `TimeBinding`.|  
|[Elemento ReportingFirstWeekOfMonth &#40;ASSL&#41;](reportingfirstweekofmonth-element-assl.md)|Define la primera semana del mes de informes para el elemento `TimeBinding`.|  
|[Elemento ReportingWeekToMonthPattern &#40;ASSL&#41;](reportingweektomonthpattern-element-assl.md)|Define el patrón de semana y mes de los informes para el elemento `TimeBinding`.|  
|[Elemento ReportServer &#40;ASSL&#41;](reportserver-element-assl.md)|Contiene el nombre de la instancia de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que utiliza la `ReportAction`.|  
|[Elemento RequiresRestart &#40;ASSL&#41;](requiresrestart-element-assl.md)|Contiene un valor de solo lectura asociado a un elemento `ServerProperty` que determina si es necesario reiniciar la instancia para que los cambios realizados en la propiedad del servidor surtan efecto.|  
|[Elemento RoleID &#40;ASSL&#41;](roleid-element-assl.md)|Identifica el rol para el que se definen los permisos.|  
|[Elemento raíz &#40;ASSL&#41;](root-element-assl.md)|Contiene los datos (conjunto de filas) para un origen de datos.|  
|[Elemento RootMemberIf &#40;ASSL&#41;](rootmemberif-element-assl.md)|Determina cómo se identifican los miembros raíz de un atributo primario.|  
|[Elemento de esquema &#40;ASSL&#41;](schema-element-assl.md)|Contiene el esquema de la vista del origen de datos.|  
|[Elemento ScriptCacheProcessingMode &#40;ASSL&#41;](scriptcacheprocessingmode-element-assl.md)|Indica el servidor debería generar la caché de script durante o después del procesamiento.|  
|[Elemento SilenceInterval &#40;ASSL&#41;](silenceinterval-element-assl.md)|Define la cantidad mínima de tiempo que entrará en pausa la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] antes de iniciar el procesamiento de imágenes MOLAP.|  
|[Elemento SilenceOverrideInterval &#40;ASSL&#41;](silenceoverrideinterval-element-assl.md)|Define la cantidad de tiempo que deberá transcurrir tras recibir la notificación inicial y antes de que se inicie incondicionalmente la creación de imágenes MOLAP.|  
|[Segmentar el elemento &#40;ASSL&#41;](slice-element-assl.md)|Contiene una expresión MDX que define el segmento contenido en una partición.|  
|[Elemento SolveOrder &#40;ASSL&#41;](solveorder-element-assl.md)|Indica el orden de resolución en el que se aplica el elemento `CalculationProperty` a un miembro calculado o a una definición de celda calculada.|  
|[Elemento Source &#40;enlace&#41; &#40;ASSL&#41;](source-element-binding-assl.md)|Identifica el origen de datos al que está enlazado el elemento primario.|  
|[Elemento Source &#40;ComAssembly&#41; &#40;ASSL&#41;](source-element-comassembly-assl.md)|Contiene el nombre de archivo o identificador de programación (ProgID) para un componente del Modelo de objetos componentes (COM).|  
|[Elemento Source &#40;medida&#41; &#40;ASSL&#41;](source-element-measure-assl.md)|Contiene los detalles del origen que contiene al valor del elemento `Measure` asociado.|  
|[Elemento SourceAttributeID &#40;ASSL&#41;](sourceattributeid-element-assl.md)|Contiene el identificador del atributo de origen en el que el [nivel](../objects/level-element-assl.md) se basa el elemento.|  
|[Elemento SourceColumnID &#40;ASSL&#41;](sourcecolumnid-element-assl.md)|Contiene el Id. de la columna de estructura de minería de datos de origen en el elemento antecesor `MiningStructure`.|  
|[Elemento de estado &#40;ASSL&#41;](state-element-assl.md)|Contiene un valor de solo lectura que describe el estado de procesamiento actual del elemento primario.|  
|[Elemento Status &#40;ASSL&#41;](status-element-assl.md)|Contiene una expresión MDX que devuelve un indicador de estado para un elemento `Kpi`.|  
|[Elemento StatusGraphic &#40;ASSL&#41;](statusgraphic-element-assl.md)|Contiene la representación gráfica recomendada del estado del elemento `Kpi`.|  
|[Elemento StopTime &#40;ASSL&#41;](stoptime-element-assl.md)|Especifica la fecha y hora en la que debería detenerse un elemento `Trace`.|  
|[Elemento StorageLocation &#40;ASSL&#41;](storagelocation-element-assl.md)|Contiene la ubicación del sistema de almacenamiento de archivos para el contenido del elemento primario.|  
|[Elemento StorageMode &#40;ASSL&#41;](storagemode-element-assl.md)|Determina el modo de almacenamiento para el elemento primario.|  
|[Elemento TableID &#40;ASSL&#41;](tableid-element-assl.md)|Contiene el Id. de la tabla (a partir del elemento `DataSourceView`) asociada al elemento primario.|  
|[Elemento Target &#40;ASSL&#41;](target-element-assl.md)|Identifica el destino del elemento `Action`.|  
|[Elemento TargetType &#40;ASSL&#41;](targettype-element-assl.md)|Identifica el tipo de elemento del elemento identificado en el [destino](target-element-assl.md) elemento.|  
|[Elemento de texto &#40;ASSL&#41;](text-element-assl.md)|Contiene el texto de un [comando](../objects/command-element-assl.md) elemento.|  
|[Elemento timeout &#40;ASSL&#41;](timeout-element-assl.md)|Especifica el tiempo, en segundos, después del cual se producirá un error de tiempo de espera si se intentan recuperar los datos.|  
|[Elemento de tendencia &#40;ASSL&#41;](trend-element-assl.md)|Contiene una expresión MDX que devuelve un indicador de tendencia para un elemento `Kpi`.|  
|[Elemento TrendGraphic &#40;ASSL&#41;](trendgraphic-element-assl.md)|Contiene la representación gráfica recomendada de la tendencia del elemento `Kpi`.|  
|[Elemento Trimming &#40;ASSL&#41;](trimming-element-assl.md)|Especifica cómo se recortan los datos del origen de datos.|  
|[Tipo de elemento &#40;acción&#41; &#40;ASSL&#41;](type-element-action-assl.md)|Contiene el tipo del elemento `Action`.|  
|[Tipo de elemento &#40;enlace&#41; &#40;ASSL&#41;](type-element-binding-assl.md)|Contiene el tipo del enlace de atributo.|  
|[Tipo de elemento &#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](type-element-clrassemblyfile-assl.md)|Especifica el tipo de archivo de uno de los archivos que pertenecen a un ensamblado de .NET Framework.|  
|[Tipo de elemento &#40;dimensión&#41; &#40;ASSL&#41;](type-element-dimension-assl.md)|Proporciona información acerca del contenido de la dimensión.|  
|[Tipo de elemento &#40;DimensionAttribute&#41; &#40;ASSL&#41;](type-element-dimensionattribute-assl.md)|Contiene el tipo del atributo.|  
|[Tipo de elemento &#40;MeasureGroup&#41; &#40;ASSL&#41;](type-element-measuregroup-assl.md)|Especifica el tipo del `MeasureGroup`.|  
|[Tipo de elemento &#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](type-element-measuregroupattribute-assl.md)|Contiene el tipo de un [MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md) elemento.|  
|[Tipo de elemento &#40;MiningStructureColumn&#41; &#40;ASSL&#41;](type-element-miningstructurecolumn-assl.md)|Contiene el tipo de la [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.|  
|[Tipo de elemento &#40;partición&#41; &#40;ASSL&#41;](type-element-partition-assl.md)|Contiene el tipo del elemento `Partition`.|  
|[Tipo de elemento &#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](type-element-perspectivecalculation-assl.md)|Indica el tipo de la [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elemento.|  
|[Elemento UnknownMember &#40;ASSL&#41;](unknownmember-element-assl.md)|Indica si el miembro desconocido está visible.|  
|[Elemento UnknownMemberName &#40;ASSL&#41;](unknownmembername-element-assl.md)|Contiene el título, en el idioma predeterminado de la dimensión, del miembro desconocido de la dimensión.|  
|[Elemento Usage &#40;DimensionAttribute&#41; &#40;ASSL&#41;](usage-element-dimensionattribute-assl.md)|Describe cómo se utiliza un atributo.|  
|[Elemento Usage &#40;MiningModelColumn&#41; &#40;ASSL&#41;](usage-element-miningmodelcolumn-assl.md)|Describe cómo se utiliza la columna asociada en la `MiningStructure` primaria.|  
|[Valor de elemento &#40;ASSL&#41;](value-element-assl.md)|Contiene el valor del elemento primario.|  
|[Elemento Version &#40;ASSL&#41;](version-element-assl.md)|Contiene el número de versión de solo lectura de la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] representada por el elemento `Server`.|  
|[Elemento Visibility &#40;ASSL&#41;](visibility-element-assl.md)|Define la visibilidad de un [anotación](../objects/annotation-element-assl.md) elemento.|  
|[Elemento visible &#40;ASSL&#41;](visible-element-assl.md)|Determina la visibilidad del elemento primario.|  
|[Elemento VisualTotals &#40;ASSL&#41;](visualtotals-element-assl.md)|Contiene una expresión MDX que determina si los totales visuales se muestran para los miembros de este atributo.|  
|[Escribir elemento &#40;ASSL&#41;](write-element-assl.md)|Determina si los datos o los metadatos se pueden escribir para un elemento `CubeDimensionPermission` o `Permission` determinado.|  
|[Elemento WriteEnabled &#40;ASSL&#41;](writeenabled-element-assl.md)|Indica si las reescrituras de dimensión están disponibles (sujetas a permisos de seguridad).|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de elementos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
