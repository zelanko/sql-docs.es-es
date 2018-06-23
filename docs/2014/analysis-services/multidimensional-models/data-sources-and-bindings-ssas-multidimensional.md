---
title: Orígenes de datos y enlaces (SSAS Multidimensional) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d5386a2a09928f8a7dbc04248df74e8112749f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107321"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>Orígenes de datos y enlaces (SSAS multidimensional)
  Es posible enlazar cubos, dimensiones y otros objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un origen de datos. Un origen de datos puede ser uno de los objetos siguientes:  
  
-   Un origen de datos relacional.  
  
-   Una canalización de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que genera un conjunto de filas (o varios conjuntos de filas divididos en segmentos).  
  
 El medio de expresar el origen de datos varía según el tipo de origen de datos. Por ejemplo, un origen de datos relacional se distingue por una cadena de conexión. Para obtener más información acerca de los orígenes de datos, vea [Data Sources in Multidimensional Models](data-sources-in-multidimensional-models.md).  
  
 Sin tener en cuenta el origen de datos usado, la vista del origen de datos (DSV) contiene los metadatos para el origen de datos. Así, los enlaces para un cubo u otros objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se expresan como enlaces a DSV. Estos enlaces pueden incluir enlaces a objetos lógicos, como vistas, columnas calculadas y relaciones que no existen físicamente en el origen de datos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agrega una columna calculada que encapsula la expresión en la DSV y, a continuación, enlaza la medida de OLAP correspondiente a dicha columna de la DSV. Para obtener más información acerca de DSVs, vea [Data Source Views in Multidimensional Models](data-source-views-in-multidimensional-models.md).  
  
 Cada objeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enlaza con el origen de datos a su manera. Además, los enlaces de datos para estos objetos y la definición del origen de datos se pueden proporcionar insertados con la definición del objeto enlazado a datos (por ejemplo, la dimensión) o fuera de línea como un conjunto independiente de definiciones.  
  
## <a name="analysis-services-data-types"></a>Tipos de datos de Analysis Services  
 Los tipos de datos que se utilizan en los enlaces deben coincidir con los tipos de datos admitidos por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los tipos de datos siguientes están definidos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|Tipo de datos de Analysis Services|Descripción|  
|---------------------------------|-----------------|  
|Bigint|Entero de 64 bits con signo. Este tipo de datos se asigna internamente al tipo de datos Int64 en Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_I8 en OLE DB.|  
|Bool|Valor booleano. Este tipo de datos se asigna internamente al tipo de datos Booleano en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_BOOL en OLE DB.|  
|Moneda|Valor de moneda comprendido entre -263 (o -922.337.203.685.477,5808) y 263-1 (o +922.337.203.685.477,5807) con una precisión de una diezmilésima de unidad de moneda. Este tipo de datos se asigna internamente al tipo de datos Decimal en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_CY en OLE DB.|  
|date|Datos de fecha, almacenados como un número de punto flotante de doble precisión. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción del día. Este tipo de datos se asigna internamente al tipo de datos DateTime en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_DATE en OLE DB.|  
|Doble|Número de punto flotante de doble precisión comprendido entre -1,79E +308 y 1,79E +308. Este tipo de datos se asigna internamente al tipo de datos Doble en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_R8 en OLE DB.|  
|Integer|Entero de 32 bits con signo. Este tipo de datos se asigna internamente al tipo de datos Int32 en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_I4 en OLE DB.|  
|Único|Número de punto flotante de precisión simple comprendido entre -3,40E +38 y 3,40E +38. Este tipo de datos se asigna internamente al tipo de datos Single en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_R4 en OLE DB.|  
|SmallInt|Entero de 16 bits con signo. Este tipo de datos se asigna internamente al tipo de datos Int16 en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_I2 en OLE DB.|  
|TinyInt|Entero de 8 bits con signo. Este tipo de datos se asigna internamente al tipo de datos SByte en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_I1 en OLE DB.<br /><br /> Nota: Si un origen de datos contiene campos que son del tipo de datos tinyint y la propiedad Incremento automático está establecida en True, se convertirán en enteros en la vista del origen de datos.|  
|UnsignedBigInt|Entero de 64 bits sin signo. Este tipo de datos se asigna internamente al tipo de datos UInt64 en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_UI8 en OLE DB.|  
|UnsignedInt|Entero de 32 bits sin signo. Este tipo de datos se asigna internamente al tipo de datos UInt32 en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_UI4 en OLE DB.|  
|UnsignedSmallInt|Entero de 16 bits sin signo. Este tipo de datos se asigna internamente al tipo de datos UInt16 en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_UI2 en OLE DB.|  
|WChar|Flujo de caracteres Unicode terminado en NULL. Este tipo de datos se asigna internamente al tipo de datos String en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y al tipo de datos DBTYPE_WSTR en OLE DB.|  
  
 Todos los datos que se reciben del origen de datos se convierten al tipo de [!INCLUDE[ssAS](../../includes/ssas-md.md)] especificado en el enlace (normalmente, durante el procesamiento). Se produce un error si no se puede realizar la conversión (por ejemplo, de String a Int). [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] normalmente establece el tipo de datos del enlace en el que mejor coincide con el tipo de origen del origen de datos. Por ejemplo, los tipos Date, DateTime, SmallDateTime, DateTime2 y DateTimeOffset de SQL se asignan a Date en [!INCLUDE[ssAS](../../includes/ssas-md.md)] , y el tipo Time de SQL se asigna a String.  
  
## <a name="bindings-for-dimensions"></a>Enlaces para dimensiones  
 Cada atributo de una dimensión se enlaza a una columna en una DSV. Todos los atributos de una dimensión deben proceder de un origen de datos único. Sin embargo, los atributos se pueden enlazar a columnas en tablas diferentes. Las relaciones entre las tablas se definen en DSV. En el caso en el que existe más de un conjunto de relaciones para la misma tabla, podría ser necesario introducir una consulta con nombre en la DSV que actúe como 'alias' de tabla. Las expresiones y los filtros se definen en la DSV usando cálculos con nombre y consultas con nombre.  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>Enlaces para grupos de medidas, medidas y particiones  
 Cada grupo de medidas tiene los enlaces predeterminados siguientes:  
  
-   El grupo de medidas se enlaza a una tabla en una DSV (por ejemplo, `MeasureGroup.Source`).  
  
-   Cada medida está enlazada a una columna de la tabla (por ejemplo, `Measure.ValueColumn.Source`).  
  
-   Cada dimensión de grupo de medidas tiene un conjunto de *atributos de granularidad* que definen la granularidad del grupo de medidas. Cada uno de estos atributos se debe enlazar a la columna o columnas de la tabla de hechos que contienen la clave de atributo. (Para obtener más información sobre los atributos de granularidad, vea Atributos de granularidad de grupo de medidas posteriormente en este tema.)  
  
 Estos enlaces predeterminados se pueden invalidar de manera selectiva por partición. Cada partición puede especificar un origen de datos, tabla o nombre de consulta, o expresión de filtro diferentes. La estrategia de partición más común es invalidar la tabla por partición, usando el mismo origen de datos. Las alternativas incluyen la aplicación de un filtro diferente por partición o el cambio del origen de datos.  
  
 El origen de datos predeterminado se debe definir en la DSV, proporcionando por tanto la información del esquema, incluyendo los detalles de las relaciones. Cualquier consulta o tabla adicional especificada en el nivel de partición no se tiene que mostrar en la DSV, pero deben tener el mismo esquema que la tabla predeterminada definida para el grupo de medidas o, al menos, deben contener todas las columnas usadas por las medidas o los atributos de granularidad. Los enlaces detallados por medida y atributo de granularidad no se pueden invalidar en el nivel de partición y se supone que son para las mismas columnas como se define para el grupo de medidas. Por lo tanto, si la partición usa un origen de datos que tiene de hecho un esquema diferente, el `TableDefinition` consulta definida para la partición debe producir el mismo esquema que el esquema utilizado por el grupo de medida.  
  
### <a name="measuregroup-granularity-attributes"></a>Atributos de granularidad de grupo de medidas  
 Cuando la granularidad de un grupo de medidas coincide con la granularidad conocida en la base de datos, y hay una relación directa de la tabla de hechos a la tabla de dimensiones, el atributo de granularidad solamente tiene que enlazarse con la columna o columnas de clave externa adecuadas de la tabla de hechos. Por ejemplo, piense en el hecho siguiente y en las tablas de dimensiones:  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 Si analiza por el producto pedido, para el producto pedido en el rol de dimensión de ventas, el atributo de granularidad de producto se enlazaría a Sales.OrderedProductID.  
  
 Sin embargo, puede haber ocasiones en las que los `GranularityAttributes` no podrían existir como columnas en la tabla de hechos. Por ejemplo, el `GranularityAttributes` no podrían existir como columnas en las siguientes circunstancias:  
  
-   La granularidad de OLAP es más amplia que la granularidad en el origen.  
  
-   Una tabla intermedia se interpone entre la tabla de hechos y la tabla de dimensiones.  
  
-   La clave de dimensión no es igual que la clave principal de la tabla de dimensiones.  
  
 En todos estos casos, la DSV se debe definir para que existan GranularityAttributes en la tabla de hechos. Por ejemplo, se puede introducir una consulta con nombre o una columna calculada.  
  
 Por ejemplo, en las mismas tablas de ejemplo que las anteriores, si la granularidad era por Categoría, se podría introducir una vista de las ventas:  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 En este caso, la categoría GranularityAttribute se enlaza a SalesWithCategory.OrderedProductCategory.  
  
### <a name="migrating-from-decision-support-objects"></a>Migrar desde Objetos de ayuda para la toma de decisiones  
 Objetos de ayuda para la toma de decisiones (DSO) 8.0 permiten que `PartitionMeasures` se vuelvan a enlazar. Por consiguiente, la estrategia de migración en estos casos es construir la consulta adecuada.  
  
 De igual forma, no es posible volver a enlazar los atributos de dimensión dentro de una partición, aunque DSO 8.0 permite además este reenlace. La estrategia de migración en estos casos es definir las consultas con nombre necesarias en DSV de manera que existan las mismas tablas y columnas en la DSV para la partición, conforme se usan tablas y columnas para la dimensión. Estos casos pueden requerir la adopción de la migración simple, en la que la cláusula de/combinación/filtro está asignada a una consulta con nombre única en lugar de a un conjunto estructurado de tablas relacionadas. Al igual que DSO 8.0 permite a PartitionDimensions volverse a enlazar cuando la partición está usando el mismo origen de datos, la migración también puede requerir varias DSV para el mismo origen de datos.  
  
 En DSO 8.0, los enlaces correspondientes se pueden expresar de dos maneras diferentes, dependiendo de si se emplean esquemas optimizados, enlazando a la clave principal de la tabla de dimensiones o a la clave externa de la tabla de hechos. En ASSL, no se distinguen los dos formularios diferentes.  
  
 El mismo enfoque a los enlaces se aplica incluso para una partición con un origen de datos que no contiene tablas de dimensiones, ya que el enlace se realiza a la columna de clave externa de la tabla de hechos, no a la columna de clave principal de la tabla de dimensiones.  
  
## <a name="bindings-for-mining-models"></a>Enlaces para modelos de minería de datos  
 Un modelo de minería de datos es relacional u OLAP. Los enlaces de datos para un modelo de minería de datos relacional son considerablemente diferentes a los enlaces para un modelo de minería de datos de OLAP.  
  
### <a name="bindings-for-a-relational-mining-model"></a>Enlaces para un modelo de minería de datos relacional  
 Un modelo de minería de datos relacional depende de las relaciones definidas en la DSV para resolver cualquier ambigüedad respecto a qué columnas se enlazan a determinados orígenes de datos. En un modelo de minería de datos relacional, los enlaces de datos siguen estas reglas:  
  
-   Cada columna de tabla no anidada se enlaza a una columna de la tabla de casos o a una tabla relacionada con la tabla de casos (siguiendo una relación de varios a uno o de uno a uno). La DSV define las relaciones entre las tablas.  
  
-   Cada columna de tabla anidada se enlaza a una tabla de origen. Las columnas que son propiedad de la columna de tabla anidada se enlazan a continuación a las columnas de dicha tabla de origen o una tabla relacionada con la tabla de origen. (De nuevo, el enlace sigue una relación de varios a uno o de uno a uno.) Los enlaces del modelo de minería de datos no proporcionan la ruta de acceso de combinación a la tabla anidada. En su lugar, las relaciones definidas en la DSV proporcionan esta información.  
  
### <a name="bindings-for-an-olap-mining-model"></a>Enlaces para un modelo de minería de datos OLAP  
 Los modelos de minería de datos de OLAP no tienen el equivalente de una DSV. Por consiguiente, los enlaces de datos deben proporcionar cualquier anulación de ambigüedad entre columnas y orígenes de datos. Por ejemplo, un modelo de minería de datos puede basarse en el cubo Ventas y las columnas se pueden basar en Qty, Amount y Product Name. Alternativamente, un modelo de minería de datos puede estar basado en producto y las columnas se pueden basar en nombre de producto, color de producto y una tabla anidada con cantidad de ventas.  
  
 En un modelo de minería de datos OLAP, los enlaces de datos siguen estas reglas:  
  
-   Cada columna de tabla no anidada se enlaza a una medida en un cubo, a un atributo en una dimensión de cubo (especificando el `CubeDimension` para eliminar la ambigüedad en el caso de los roles de dimensión), o a un atributo en una dimensión.  
  
-   Cada columna de tabla anidada se enlaza a una `CubeDimension`. Es decir, define cómo navegar desde una dimensión a un cubo relacionado o, en el caso menos común de tablas anidadas, desde un cubo a una de sus dimensiones.  
  
## <a name="out-of-line-bindings"></a>enlaces fuera de línea  
 Los enlaces fuera de línea permiten cambiar temporalmente los enlaces de datos existentes mientras dura un comando. Los enlaces fuera de línea hacen referencia a los enlaces incluidos en un comando y que no se conservan. Los enlaces fuera de línea solo se aplican mientras se ejecuta dicho comando concreto. En contraste, los enlaces insertados están contenidos en la definición de objeto de ASSL y se conservan con la definición de objeto dentro de los metadatos del servidor.  
  
 ASSL permite especificar cualquiera de los enlaces de fuera de línea un `Process` comando, si no está en un lote o en un `Batch` comando. Si los enlaces fuera de línea se especifican en el comando `Batch`, todos los enlaces especificados en el comando `Batch` crean un nuevo contexto de enlace en el que se ejecutan todos los comandos `Process` del lote. Este nuevo contexto de enlace incluye objetos que se procesan indirectamente debido al comando `Process`.  
  
 Cuando los enlaces fuera de línea se especifican en un comando, invalidan los enlaces insertados contenidos en la DDL almacenada. Estos objetos procesados pueden incluir el objeto directamente nombrado en el `Process` comando, o pueden incluir otros objetos cuyo procesamiento se inicie automáticamente como parte del procesamiento.  
  
 Los enlaces fuera de línea se especifican incluyendo el objeto de colección opcional `Bindings` con el comando de procesamiento. Opcional `Bindings` colección contiene los elementos siguientes.  
  
|Property|Cardinalidad|Tipo|Descripción|  
|--------------|-----------------|----------|-----------------|  
|`Binding`|0-n|`Binding`|Proporciona una colección de nuevos enlaces.|  
|`DataSource`|0-1|`DataSource`|Reemplaza `DataSource` del servidor que se habría usado.|  
|`DataSourceView`|0-1|`DataSourceView`|Reemplaza la `DataSourceView` del<br /><br /> servidor que se habría usado.|  
  
 Todos los elementos que se relacionan con los enlaces fuera de línea son opcionales. Para cualquier elemento no especificado, ASSL usa la especificación contenida en el DDL del objeto almacenado. La especificación de `DataSource` o `DataSourceView` en el comando `Process` es opcional. Si se especifican `DataSource` o `DataSourceView`, no se crean instancias de los mismos y no se almacenan después de que el comando `Process` se haya completado.  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>Definición del tipo de enlace fuera de línea  
 Dentro de la colección `Bindings` fuera de línea, ASSL permite una colección de enlaces para varios objetos, cada uno de ellos `Binding`. Cada `Binding` tiene una referencia de objeto extendida, similar a la referencia a objeto, pero que también puede hacer referencia a objetos secundarios (por ejemplo, atributos de dimensión y atributos de grupo de medidas). Este objeto toma la forma plana típica de la `Object` elemento `Process` comandos, excepto en que la \< *objeto*>\<*/objeto*> etiquetas no están presentes.  
  
 Cada objeto para el que se especifica el enlace se identifica por un elemento XML del formulario \< *objeto*> ID (por ejemplo, `DimensionID`). Después de haber identificado el objeto de manera tan específica como sea posible con el formulario \< *objeto*> ID, a continuación, identifica el elemento para el que se especifica el enlace, que suele ser `Source`. Un caso común a tener en cuenta es en qué `Source` es una propiedad de la `DataItem`, que es el caso para enlaces de columna en un atributo. En este caso, no especifica la etiqueta `DataItem`; en su lugar, simplemente especifica la propiedad `Source`, como si estuviera directamente en la columna que se va a enlazar.  
  
 `KeyColumns` se identifican por su orden dentro de la colección `KeyColumns`. Allí no es posible especificar, por ejemplo, solo la primera y la tercera columna de clave de un atributo, porque no hay manera de indicar que se va a omitir la segunda columna de clave. Todas las columnas de clave deben encontrarse en el enlace fuera de línea para un atributo de dimensión.  
  
 `Translations`, aunque no tienen ningún Id., se identifican semánticamente por su idioma. Por consiguiente, `Translations` dentro de un enlace `Binding` tienen que incluir su identificador de idioma.  
  
 Un elemento adicional permitido dentro de un `Binding` que no existe directamente en el DDL es `ParentColumnID`, que se usa para las tablas anidadas para la minería de datos. En este caso, es necesario identificar la columna primaria en la tabla anidada para la que se proporciona el enlace.  
  
  