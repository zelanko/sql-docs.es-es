---
title: Propiedades XMLA (XMLA) compatibles con | Documentos de Microsoft
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
topic_type:
- apiref
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
caps.latest.revision: 24
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 89293d101513cb2cec07fe69b2ba22e67f55dd21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201492"
---
# <a name="supported-xmla-properties-xmla"></a>Propiedades XMLA compatibles (XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite las propiedades descritas en la tabla siguiente. Utilice estas propiedades enumeradas en la [propiedades](properties-element-xmla.md) elemento de la [Discover](../xml-elements-methods-discover.md) y [Execute](../xml-elements-methods-execute.md) métodos.  
  
|Nombre|Elemento|  
|----------|-------------|  
|AxisFormat|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Determina el formato usado en un [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) del conjunto de resultados para describir los ejes del conjunto de datos multidimensional. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ClusterFormat*|El `MDDataSet` eje se compone de uno o varios [CrossProduct](crossproduct-element-xmla.md) elementos.|  
|*CustomFormat*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa el *TupleFormat* formato para esta configuración.|  
|*TupleFormat*|(Valor predeterminado) El `MDDataSet` eje contiene uno o varios [tupla](tuple-element-xmla.md) elementos.|  
  
 Esta propiedad se puede utilizar con el método `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|BeginRange|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Contiene un valor entero basado en cero que corresponde a un valor del atributo `CellOrdinal`. (El `CellOrdinal` atributo forma parte de la [celda](cell-element-mddataset-xmla.md) elemento en el [CellData](celldata-element-xmla.md) sección de `MDDataSet`.)<br /><br /> La aplicación cliente puede utilizar esta propiedad, junto con la propiedad `EndRange` para restringir un conjunto de datos OLAP devuelto por un comando a un rango de celdas específico. Si se especifica -1, se devuelven todas las celdas hasta la celda especificada en la propiedad `EndRange`.<br /><br /> El valor predeterminado de esta propiedad es -1.<br /><br /> Esta propiedad se puede utilizar con el método `Execute`.|  
|Catálogo|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Cuando se establece una sesión con una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para enviar un comando XMLA, esta propiedad equivale a la propiedad OLE DB, DBPROP_INIT_CATALOG.<br /><br /> Cuando se establece esta propiedad durante una sesión para cambiar la base de datos actual de la sesión, la propiedad es equivalente a la propiedad OLE DB, DBPROP_CURRENTCATALOG.<br /><br /> El valor predeterminado de esta propiedad es una cadena vacía.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|CatalogLocation|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_CATALOGLOCATION.<br /><br /> El valor predeterminado de esta propiedad es cero (0), que equivale a DBPROPVAL_CL_START.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|ClientProcessID|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Contiene el identificador (id.) del subproceso de la sesión actual.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|CommitTimeout|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina cuánto tiempo, en segundos, espera la fase de confirmación de un comando XMLA que se está ejecutando en ese momento antes de revertirse. La fase de confirmación corresponde a comandos XMLA como [instrucción](../xml-elements-commands/statement-element-xmla.md) o [proceso](../xml-elements-commands/process-element-xmla.md).<br /><br /> El valor cero (0) indica que la instancia esperará indefinidamente.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|Contenido|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Determina el tipo de datos que se devuelve de los métodos `Discover` y `Execute`. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Ninguno*|Permite comprobar la estructura del comando pero no ejecutarlo.|  
|*Esquema*|Devuelve el esquema XML que está relacionado con el comando solicitado. El esquema XML indica columnas y otra información.|  
|*Datos*|Solo devuelve los datos que se solicitaron.|  
|*SchemaData*|(Valor predeterminado) Devuelve la información del esquema y los datos.|  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|Cube|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Contiene el nombre del cubo que establece el contexto para el comando. Si el comando contiene un nombre de cubo, como dentro de la cláusula FROM de expresiones multidimensionales (MDX) [seleccione](/sql/mdx/mdx-data-manipulation-select) instrucción, el valor de esta propiedad se omite.<br /><br /> El valor predeterminado de esta propiedad es una cadena vacía.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DataSourceInfo|*Uso*<br /> Propiedad `String` de lectura/escritura, obligatoria<br /><br /> *Description*<br /> Contiene la información, como el nombre de instancia, necesaria para conectarse al origen de datos.<br /><br /> Las aplicaciones cliente no deberían construir los contenidos de la propiedad `DataSourceInfo` que se han de enviar a una instancia. En su lugar, la aplicación cliente debería buscar los orígenes de datos admitidos por el proveedor utilizando el `Discover` método para recuperar el [DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md) conjunto de filas. La aplicación cliente devuelve a continuación el mismo valor para la propiedad `DataSourceInfo` que el cliente recuperó del conjunto de filas de DISCOVER_DATASOURCES.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropCatalogTerm|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_CATALOGTERM.<br /><br /> El valor predeterminado de esta propiedad es "Database".<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropCatalogUsage|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_CATALOGUSAGE.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropColumnDefinition|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_COLUMNDEFINITION.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropConcatNullBehavior|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_CONCATNULLBEHAVIOR.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a DBPROPVAL_CB_NULL.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropDataSourceReadOnly|*Uso*<br /> Opcional, solo lectura `Boolean` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_DATASOURCEREADONLY.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropGroupBy|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_GROUPBY.<br /><br /> El valor predeterminado de esta propiedad es 2, que equivale a DBPROPVAL_GB_EQUALS_SELECT.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropHeterogeneousTables|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_HETEROGENEOUSTABLES.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropIdentifierCase|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_IDENTIFIERCASE.<br /><br /> El valor predeterminado de esta propiedad es 8, que equivale a DBPROPVAL_IC_MIXED.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropInitMode|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_INIT_MODE.<br /><br /> Los únicos valores admitidos para esta propiedad son DB_MODE_READWRITE y DB_MODE_READ.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMaxIndexSize|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MAXINDEXSIZE.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMaxOpenChapters|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MAXOPENCHAPTERS.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMaxRowSize|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MAXROWSIZE.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMaxRowSizeIncludeBlob|*Uso*<br /> Propiedad `Boolean` de solo lectura, opcional<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MAXROWSIZEINCLUDESBLOB.<br /><br /> El valor predeterminado de esta propiedad es TRUE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMaxTablesInSelect|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MAXTABLESINSELECT.<br /><br /> El valor predeterminado de esta propiedad es 1.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdAutoexists|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina el comportamiento de autoexists. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|Valor predeterminado, igual que 1.|  
|*1*|Se aplica el autoexists profundo para los ejes de la consulta y los conjuntos con nombre. Incluye las cláusulas y subselecciones de WHERE.|  
|*2*|Se aplica el autoexists profundo para los ejes de la consulta y excluya los conjuntos con nombre de autoexists. Incluye las cláusulas y subselecciones de WHERE.|  
|*3*|No se aplica autoexist para los conjuntos con nombre con la cláusula WHERE. Se aplica el autoexist superficial para los ejes de la consulta con la cláusula WHERE. Se aplica el autoexists profundo para los ejes de la consulta con subselecciones y conjuntos con nombre con subselecciones.|  
  
 Cero o vacío son los valores predeterminados para esta propiedad. Esta es una propiedad de sesión que solo se puede establecer cuando se crea la sesión.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdCacheMode|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdCachePolicy|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdCacheRatio|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdCacheRatio2|*Uso*<br /> Opcional, lectura/escritura `Double` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|*Uso*<br /> Propiedad `Integer` de lectura/escritura, opcional<br /><br /> *Description*<br /> Determina la funcionalidad de comparación de cadenas con distinción entre mayúsculas y minúsculas y de criterio de ordenación. Esta propiedad controla cómo se realizan las comparaciones en juegos de caracteres que distinguen entre mayúsculas y minúsculas, como el katakana para el japonés y el hindi. El valor de esta propiedad se establece en la primera conexión del subproceso y afecta a todas las conexiones posteriores de ese subproceso.<br /><br /> Utilice la siguiente tabla para determinar qué marcas ha de utilizar.|  
  
|Nombre|Valor|Descripción|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0 x 00000001*|No se tienen en cuenta mayúsculas y minúsculas.|  
|No aplicable|*0 x 00000002*|Comparación binaria. Se comparan los caracteres basándose en su valor subyacente en el juego de caracteres, no en el orden de su alfabeto específico.|  
|NORM_IGNORENONSPACE|*0 x 00000010*|Los caracteres sin espacio se omiten.|  
|NORM_IGNORESYMBOLS|*0 x 00000100*|Los símbolos se omiten.|  
|NORM_IGNOREKANATYPE|*0 x 00001000*|No se diferencia entre los caracteres hiragana y katakana. Cuando se comparan, los caracteres hiragana y katakana correspondientes se consideran iguales.|  
|NORM_IGNOREWIDTH|*0 x 00010000*|No se diferencia entre las versiones de un byte y de doble byte del mismo carácter.|  
|SORT_STRINGSORT|*0 x 00100000*|La puntuación se trata igual que los símbolos.|  
  
 Para obtener más información sobre la comparación de cadenas en OLE DB, busque "CompareString" en la sección Platform SDK de MSDN Library.  
  
 No existe un valor predeterminado para esta propiedad.  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdCompareCaseSensitiveStringFlags|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina la funcionalidad de comparación de cadenas sin distinción entre mayúsculas y minúsculas y de criterio de ordenación. Esta propiedad controla cómo se realizan las comparaciones en juegos de caracteres que distinguen entre mayúsculas y minúsculas, como el katakana para el japonés y el hindi. El valor de esta propiedad se establece en la primera conexión del subproceso y afecta a todas las conexiones posteriores de ese subproceso.<br /><br /> Utilice la siguiente tabla para determinar qué marcas ha de utilizar.|  
  
|Nombre|Valor|Descripción|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0 x 00000001*|No se tienen en cuenta mayúsculas y minúsculas.|  
|No aplicable|*0 x 00000002*|Comparación binaria. Se comparan los caracteres basándose en su valor subyacente en el juego de caracteres, no en el orden de su alfabeto específico.|  
|NORM_IGNORENONSPACE|*0 x 00000010*|Los caracteres sin espacio se omiten.|  
|NORM_IGNORESYMBOLS|*0 x 00000100*|Los símbolos se omiten.|  
|NORM_IGNOREKANATYPE|*0 x 00001000*|No se diferencia entre los caracteres hiragana y katakana. Cuando se comparan, los caracteres hiragana y katakana correspondientes se consideran iguales.|  
|NORM_IGNOREWIDTH|*0 x 00010000*|No se diferencia entre las versiones de un byte y de doble byte del mismo carácter.|  
|SORT_STRINGSORT|*0 x 00100000*|La puntuación se trata igual que los símbolos.|  
  
 Para obtener más información sobre la comparación de cadenas en OLE DB, busque "CompareString" en la sección Platform SDK de MSDN Library.  
  
 No existe un valor predeterminado para esta propiedad.  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdDebugMode|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdDynamicDebugLimit|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdFlattened2|*Uso*<br /> Opcional, lectura/escritura `Boolean` propiedad<br /><br /> *Description*<br /> Muestra todos los miembros de una jerarquía de elementos primarios y secundarios en una única columna de tabla en el resultado sin información de estructura jerárquica, a menos que la jerarquía de elementos primarios y secundarios se solicite en el Eje 0. No se utiliza la plantilla Nivel para las columnas de salida.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdMDXCompatibility|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina la forma en que se tratan los miembros de marcadores de posición en una jerarquía desigual o desequilibrada. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|Para que haya compatibilidad con versiones anteriores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], este valor equivale a 1|  
|*1*|Las jerarquías de dimensiones realizadoras de roles reciben un título que incluye el nombre de la dimensión y el de la jerarquía. El título tiene el formato siguiente:<br /><br /> [Dimensión].[Jerarquía]<br /><br /> Los miembros de marcadores de posición están visibles.|  
|*2*|Las jerarquías de dimensiones realizadoras de roles reciben un título que incluye el nombre de la dimensión y el de la jerarquía. El título tiene el formato siguiente:<br /><br /> [Dimensión].[Jerarquía]<br /><br /> Los miembros de marcadores de posición no están visibles.|  
|*3*|(Valor predeterminado) Los miembros de marcadores de posición no están visibles.|  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdMDXUniqueNameStyle|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina el algoritmo para generar los nombres únicos de los miembros de una dimensión. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.<br /><br /> El valor predeterminado de esta propiedad es 6.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|Para que haya compatibilidad con versiones anteriores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], este valor equivale a 2.|  
|*1*|Utiliza un algoritmo de ruta de acceso de clave:<br /><br /> [dim].&[clave1].&[clave2]|  
|*2*|Utiliza un algoritmo de ruta de acceso de nombre:<br /><br /> [dim].[nombre1].&[nombre2]|  
|*3*|Utiliza nombres únicos garantizados que son estables a lo largo del tiempo.|  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdSQLCompatibility|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMsmdSubQueries|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Máscara de bits que determina el comportamiento de las subconsultas. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|El valor predeterminado es compatible con las versiones anteriores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Los miembros o conjuntos calculados no se permiten en subselecciones o subcubos.|  
|*1*|Los miembros o conjuntos calculados se permiten en subselecciones o subcubos. Los antecesores del miembro calculado no se incluyen en el espacio de la subselección o del subcubo.|  
|*2*|Los miembros o conjuntos calculados se permiten en subselecciones o subcubos. Los antecesores del miembro calculado se incluyen en el espacio de la subselección o del subcubo.|  
  
 Cero o vacío son los valores predeterminados para esta propiedad.  
  
 Esta es una propiedad de sesión que solo se puede establecer cuando se crea la sesión.  
  
 Vea [miembros calculados en subselecciones y los subcubos](../../multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) para obtener una explicación detallada del comportamiento de los miembros calculados o conjuntos calculados en subselecciones y los subcubos.  
  
|Nombre|Elemento|  
|----------|-------------|  
|DbpropMsmdUseFormulaCache|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropMultiTableUpdate|*Uso*<br /> Opcional, solo lectura `Boolean` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MULTITABLEUPDATE.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropNullCollation|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_NULLCOLLATION.<br /><br /> El valor predeterminado de esta propiedad es 4, que equivale a DBPROPVAL_NC_LOW.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropOrderByColumnsInSelect|*Uso*<br /> Opcional, solo lectura `Boolean` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_ORDERBYCOLUMNSINSELECT.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropOutputParameterAvailable|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_OUTPUTPARAMETERAVAILABILITY.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a DBPROPVAL_OA_NOTSUPPORTED.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropPersistentIdType|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_PERSISTENTIDTYPE.<br /><br /> El valor predeterminado de esta propiedad es 4, que equivale a DBPROPVAL_PT_NAME.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropPrepareAbortBehavior|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_PREPAREABORTBEHAVIOR.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a DBPROPVAL_CB_DELETE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropPrepareCommitBehavior|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_PREPARECOMMITBEHAVIOR.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a DBPROPVAL_CB_DELETE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropProcedureTerm|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_PROCEDURETERM.<br /><br /> El valor predeterminado de esta propiedad es "Calculated member".<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropQuotedIdentifierCase|*Uso*<br /> Propiedad `Integer` de solo lectura, opcional<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_QUOTEDIDENTIFIERCASE.<br /><br /> El valor predeterminado de esta propiedad es 8, que equivale a DBPROPVAL_IC_MIXED.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSchemaUsage|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SCHEMAUSAGE.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSqlSupport|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SQLSUPPORT.<br /><br /> El valor predeterminado de esta propiedad es 512, que equivale a DBPROPVAL_SQL_SUBMINIMUM.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSubqueries|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SUBQUERIES.<br /><br /> **Nota:** Mientras que Extensiones de minería de datos (DMX) admite subconsultas, esta propiedad hace referencia a la compatibilidad de SQL con las subconsultas.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSupportedTxnDdl|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SUPPORTEDTXNDDL.<br /><br /> El valor predeterminado de esta propiedad es cero (0), que equivale a DBPROPVAL_TC_NONE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSupportedTxnIsoLevels|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SUPPORTEDTXNISOLEVELS.<br /><br /> El valor predeterminado de esta propiedad es 4096, que equivale a DBPROPVAL_TI_READCOMMITTED.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropSupportedTxnIsoRetain|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SUPPORTEDTXNISORETAIN.<br /><br /> El valor predeterminado de esta propiedad es 292, que equivale a una combinación de DBPROPVAL_TR_ABORT_NO, DBPROPVAL_TR_COMMIT_NO y DBPROPVAL_TR_NONE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|DbpropTableTerm|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_TABLETERM.<br /><br /> El valor predeterminado de esta propiedad es "Cube".<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|Dialect|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Establece el dialecto utilizado en las siguientes situaciones:<br /><br /> -El dialecto que el proveedor usará la primera vez que el proveedor intenta ejecutar una consulta.<br />-El dialecto utilizado para los errores de ejecución devueltos como resultado de errores de consulta.<br /><br /> Puede usar la propiedad `Dialect` si prevé que la mayoría de las consultas utilizarán un dialecto en concreto más que otro.<br /><br /> La sintaxis de las consultas puede ser similar en el caso de ciertos dialectos, como DMX y SQL. Dado que la sintaxis puede ser similar, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quizá no pueda deducir el dialecto de la sintaxis de la consulta. Si una consulta no se ejecuta en un dialecto, la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] puede intentar ejecutar de nuevo la consulta en un dialecto diferente.<br /><br /> Si está establecida la propiedad `Dialect`, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devuelve errores de ejecución de consultas en el dialecto que tiene precedencia, aunque el proveedor intente volver a ejecutar la consulta en otro dialecto. Por ejemplo, la propiedad `Dialect` está establecida en MDGUID_DM. El proveedor intenta primero ejecutar la consulta como una consulta de minería de datos, pero se produce un error en esta consulta. El proveedor vuelve a ejecutar la consulta como una consulta SQL. Sin embargo, esta consulta SQL también produce errores. Dado que el valor de la propiedad `Dialect` es MDGUID_DM, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devuelve un mensaje de error de minería de datos, no de SQL.<br /><br /> Si no está establecida la propiedad `Dialect`, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devuelve errores de ejecución de consultas en el último dialecto que se utilizó. Por ejemplo, la propiedad `Dialect` no está establecida y se produce un error en una consulta de minería de datos. El proveedor, a continuación, vuelve a enviar la consulta, como SQL. La consulta SQL también produce errores. Dado que la propiedad `Dialect` no está establecida, el proveedor devuelve un mensaje de error de SQL en lugar de un mensaje de error de minería de datos.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> Los dialectos disponibles para esta propiedad se enumeran en la siguiente tabla.|  
  
|Nombre|Valor|Descripción|  
|----------|-----------|-----------------|  
|DBGUID_SQL|*C8B522D7-5CF3-11CE-ADE5-00AA0044773D*|El analizador de SQL tiene precedencia.|  
|MDGUID_DM|*62C58FED-CCA5-44F1-83B6-7B45682B3904*|El analizador de DMX tiene precedencia.|  
|MDGUID_MDX|*A07CCCD0-8148-11D0-87BB-00C04FC33942*|El analizador de MDX tiene precedencia.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|Deshabilitar los hechos de captura previa|*Uso*<br /> Propiedad `Boolean` de lectura/escritura, opcional,<br /><br /> *Description*<br /> Cuando se establece en TRUE, el motor deja de intentar la captura previa de valores mientras dure la sesión.<br /><br /> El valor predeterminado de esta propiedad es `False`.|  
|EffectiveRoles|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|EffectiveUserName|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Especifica el nombre de la cuenta que se va a utilizar para invalidar el nombre de usuario al conectarse a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El valor de la propiedad no es normalizado, ya que el código MDX [nombre de usuario](/sql/mdx/username-mdx) función devuelve el valor literal si se utiliza esta propiedad. Esta propiedad solo la pueden utilizar los administradores del servidor.<br /><br /> Esta propiedad admite los siguientes tipos SID: User, Group, Alias, WellKnownGroup, Computer.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|EndRange|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Especifica un valor entero basado en cero que corresponde a un valor del atributo `CellOrdinal`. (El atributo `CellOrdinal` forma parte del elemento `Cell` en la sección `CellData` de `MDDataSet`).<br /><br /> La aplicación cliente puede utilizar esta propiedad, junto con la propiedad `BeginRange` para restringir un conjunto de datos OLAP devuelto por un comando a un rango de celdas específico. Si se especifica -1, se devuelven todas las celdas desde la celda especificada en la propiedad `BeginRange`.<br /><br /> El valor predeterminado de esta propiedad es -1.<br /><br /> Esta propiedad se puede utilizar con el método `Execute`.|  
|ExecutionMode|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> El valor predeterminado de esta propiedad es *Execute*.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|ForceCommitTimeout|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina cuánto tiempo, en segundos, espera la fase de confirmación del comando XMLA que se está ejecutando en ese momento antes de obligar a que se reviertan los comandos ejecutados previamente. La fase de confirmación corresponde a comandos XMLA como `Statement` o `Process`.<br /><br /> El valor cero (0) indica que la instancia esperará indefinidamente.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|Formato|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Determina el tipo de conjunto de resultados que se devuelve de los métodos `Discover` y `Execute`. Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
 El valor predeterminado de esta propiedad es *nativo*.  
  
 Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Tabular*|Devuelve un conjunto de resultados mediante el [conjunto de filas](../xml-data-types/rowset-data-type-xmla.md) tipo de datos.|  
|*Multidimensionales*|Devuelve un conjunto de filas utilizando la [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de datos.|  
|*Nativo*|No se especifica ningún formato explícitamente. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devuelve el formato adecuado para el comando. El espacio de nombres del resultado identifica el tipo de resultado real.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|ImpactAnalysis|*Uso*<br /> Opcional, solo escritura `Boolean` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|LocaleIdentifier|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Lee o establece el identificador de configuración regional (LCID) que utiliza el método `Discover` o `Execute`. Para obtener la lista hexadecimal completa de identificadores de idioma, busque "Identificadores de idioma" en MSDN Library.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MaximumRows|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropAggregateCellUpdate|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_AGGREGATECELL_UPDATE.<br /><br /> El valor predeterminado de esta propiedad es 4, que equivale a MDPROPVAL_AU_SUPPORTED.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropAxes|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_AXES.<br /><br /> El valor predeterminado de esta propiedad es 2147483647.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropDrillFunctions|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Determina el nivel de soporte técnico para las funciones de detalle en el servidor. Los siguientes valores se usan para compilar una máscara de bits válida:<br /><br /> MDPROPVAL_MDF_BASIC (0x01)<br /><br /> MDPROPVAL_MDF_ASYMMETRIC (0x02)<br /><br /> MDPROPVAL_MDF_CALC_MEMBERS (0x04)<br /><br /> Los valores predeterminados son:<br /><br /> 3 para SQL Server 2008<br /><br /> 7 para SQL Server 2008 R2 y [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropFlatteningSupport|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_FLATTENING_SUPPORT.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a MDPROPVAL_FS_FULL_SUPPORT.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxCaseSupport|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_CASESUPPORT.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxDescFlags|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_DESCFLAGS.<br /><br /> El valor predeterminado de esta propiedad es 7, que equivale a MDPROPVAL_MD_BEFORE, MDPROPVAL_MD_AFTER y MDPROPVAL_MD_SELF.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxFormulas|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_FORMULAS.<br /><br /> El valor predeterminado de esta propiedad es 63, que equivale a una combinación de MDPROPVAL_MF_WITH_CALCMEMBERS, MDPROPVAL_MF_WITH_NAMEDSETS, MDPROPVAL_MF_CREATE_CALCMEMBERS, MDPROPVAL_MF_CREATE_NAMEDSETS, MDPROPVAL_MF_SCOPE_SESSION y MDPROPVAL_MF_SCOPE_GLOBAL.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxJoinCubes|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_JOINCUBES.<br /><br /> El valor predeterminado de esta propiedad es 1, que equivale a MDPROPVAL_MJC_SINGLECUBE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxMemberFunctions|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_MEMBER_FUNCTIONS.<br /><br /> El valor predeterminado de esta propiedad es 15, que equivale a una combinación de todos los valores OLE DB disponibles.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxNamedSets|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Una máscara de bits de los valores enumerados en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0 x 01*|MDPROPVAL_MNS_BASIC.|  
|*0 x 02*|MDPROPVAL_MNS_DYNAMIC.|  
|*0 x 04*|MDPROPVAL_MNS_DISPLAYFOLDER.|  
|*0 x 08*|MDPROPVAL_MNS_CAPTION.|  
  
 El valor predeterminado para esta propiedad es 15.  
  
|Nombre|Elemento|  
|----------|-------------|  
|MdpropMdxNonMeasureExpressions|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_NONMEASURE_EXPRESSIONS.<br /><br /> El valor predeterminado de esta propiedad es cero (0), que equivale a MDPROPVAL_NME_ALLDIMENSIONS.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxNumericFunctions|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_NUMERIC_FUNCTIONS.<br /><br /> El valor predeterminado de esta propiedad es 2047, que equivale a una combinación de MDPROPVAL_MNF_MEDIAN, MDPROPVAL_MNF_VAR, MDPROPVAL_MNF_STDDEV, MDPROPVAL_MNF_RANK, MDPROPVAL_MNF_AGGREGATE, MDPROPVAL_MNF_COVARIANCE, MDPROPVAL_MNF_CORRELATION, MDPROPVAL_MNF_LINREGSLOPE, MDPROPVAL_MNF_LINREGVARIANCE, MDPROPVAL_MNF_LINREG2 y MDPROPVAL_MNF_LINREGPOINT.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxObjQualification|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_OBJQUALIFICATION.<br /><br /> El valor predeterminado de esta propiedad es 496, que equivale a una combinación de MDPROPVAL_MOQ_DIM_HIER, MDPROPVAL_MOQ_DIMHIER_LEVEL, MDPROPVAL_MOQ_DIMHIER_MEMBER, MDPROPVAL_MOQ_LEVEL_MEMBER y MDPROPVAL_MOQ_MEMBER_MEMBER.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxOuterReference|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_OUTERREFERENCE.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxQueryByProperty|*Uso*<br /> Opcional, solo lectura `Boolean` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_QUERYBYPROPERTY.<br /><br /> El valor predeterminado de esta propiedad es TRUE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxRangeRowset|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_RANGEROWSET.<br /><br /> El valor predeterminado de esta propiedad es 4, que equivale a MDPROPVAL_RR_UPDATE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxSetFunctions|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_SET_FUNCTIONS.<br /><br /> El valor predeterminado de esta propiedad es 524287, que equivale a una combinación de MDPROPVAL_MSF_TOPPERCENT, MDPROPVAL_MSF_BOTTOMPERCENT, MDPROPVAL_MSF_TOPSUM, MDPROPVAL_MSF_BOTTOMSUM, MDPROPVAL_MSF_PERIODSTODATE, MDPROPVAL_MSF_LASTPERIODS, MDPROPVAL_MSF_YTD, MDPROPVAL_MSF_QTD, MDPROPVAL_MSF_MTD, MDPROPVAL_MSF_WTD, MDPROPVAL_MSF_DRILLDOWNMEMBER, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNMEMBERTOP, MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNLEVELTOP, MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM, MDPROPVAL_MSF_DRILLUPMEMBER, MDPROPVAL_MSF_DRILLUPLEVEL y MDPROPVAL_MSF_TOGGLEDRILLSTATE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxSlicer|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_SLICER.<br /><br /> El valor predeterminado de esta propiedad es 2, que equivale a MDPROPVAL_MS_SINGLETUPLE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxStringCompop|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_MDX_STRING_COMPOP.<br /><br /> El valor predeterminado de esta propiedad es 15, que equivale a una combinación de MDPROPVAL_MSC_LESSTHAN, MDPROPVAL_MSC_GREATERTHAN, MDPROPVAL_MSC_LESSTHANEQUAL y MDPROPVAL_MSC_GREATERTHANEQUAL.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdpropMdxSubQueries|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> El valor predeterminado para esta propiedad es 63 en SQL Server 2014.<br /><br /> 31 es el valor predeterminado para esta propiedad en SQL Server 2008 R2 y [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> El valor predeterminado para esta propiedad es 15 en SQL Server 2008<br /><br /> Indica el nivel de compatibilidad para las subconsultas en MDX. Una máscara de bits de los valores enumerados en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0 x 01*|MDPROPVAL_MSQ_BASIC.|  
|*0 x 02*|MDPROPVAL_MSQ_ARBITRARYSHAPE.|  
|*0 x 04*|MDPROPVAL_MSQ_NONVISUAL.|  
|*0 x 08*|MDPROPVAL_MSQ_CALCMEMBERS.|  
  
|||  
|-|-|  
|*0 x 10*|MDPROPVAL_MSQ_CALCMEMBERS2|  
  
|Nombre|Elemento|  
|----------|-------------|  
|MdpropNamedLevels|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_NAMED_LEVELS.<br /><br /> El valor predeterminado de esta propiedad es 3, que equivale a una combinación de MDPROPVAL_NL_NAMEDLEVELS y MDPROPVAL_NL_NUMBEREDLEVELS.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|MdxMissingMemberMode|*Uso*<br /> Opcional, solo escritura `String` propiedad<br /><br /> *Description*<br /> Indica si los miembros que faltan se omiten en las instrucciones MDX.<br /><br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_MDX_MISSING_MEMBER_MODE.<br /><br /> El valor predeterminado de esta propiedad es *predeterminado*.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Valor de DB-Library*|Utilice el valor generado por la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Error*|Genere un error.|  
|*Pasar por alto*|Omita siempre los miembros que faltan.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|MDXSupport|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Especifica una enumeración que describe el grado de compatibilidad con MDX.<br /><br /> `Value` = *Core* MDX todas las opciones son compatibles.<br /><br /> Actualmente, el único valor que contiene la enumeración es *Core*. En versiones futuras se definirán otros valores para esta enumeración.<br /><br /> El valor predeterminado de esta propiedad es *Core*.<br /><br /> Esta propiedad se puede utilizar con el método `Discover`.|  
|NonEmptyThreshold|*Uso*<br /> Propiedad `Integer` de lectura/escritura, opcional<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|Contraseña|**Ya no se admite esta propiedad.**<br /><br /> *Uso*<br /> Propiedad `String` de solo escritura, opcional<br /><br /> *Description*<br /> Para que no haya problemas de compatibilidad con versiones anteriores, esta propiedad se omite sin generar ningún error cuando se usa con el método `Execute` o `Discover`.|  
|ProviderName|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_DBMSNAME.<br /><br /> El valor predeterminado para esta propiedad es "OLAP Server".<br /><br /> Esta propiedad se puede utilizar con el método `Discover`.|  
|ProviderType|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_DATASOURCE_TYPE.<br /><br /> El valor predeterminado de esta propiedad es 6.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|ProviderVersion|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_DBMSVER.<br /><br /> El valor predeterminado de esta propiedad es la versión de la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Esta propiedad se puede utilizar con el método `Discover`.|  
|ReadOnlySession|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|RealTimeOlap|*Uso*<br /> Opcional, lectura/escritura `Boolean` propiedad<br /><br /> *Description*<br /> Cuando está establecido en TRUE, indica que se consultarán en tiempo real todas las particiones que escuchan las notificaciones de tabla, sin necesidad de almacenarlas en la caché. Esta propiedad equivale a la propiedad OLE DB, DBPROP_MSMD_REAL_TIME_OLAP.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|ReturnCellProperties|*Uso*<br /> Opcional, lectura/escritura `Boolean` propiedad<br /><br /> *Description*<br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|Roles|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Especifica una cadena delimitada por comas de los nombres de rol con los que una aplicación cliente se conecta a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Esta propiedad permite al usuario conectarse utilizando un rol distinto del que está utilizando en ese momento. Por ejemplo, es posible que un administrador del servidor quiera conectarse a un cubo como miembro de un rol para probar los permisos concedidos a ese rol. Este usuario debe ser un miembro del rol especificado para conectarse utilizando esa propiedad.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> **Nota:** Los nombres de función distinguen entre mayúsculas y minúsculas. **No utilice** espacios en blanco entre los nombres de función delimitada por comas. De lo contrario, las consultas a conjuntos de celdas protegidas podrían devolver errores y resultados imprevistos.|  
|SafetyOptions|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Determina si las aplicaciones cliente pueden registrar y cargar bibliotecas no seguras.<br /><br /> El valor de esta propiedad determina también si la palabra clave PASSTHROUGH está permitida en los cubos locales. En las situaciones siguientes se produce un error:<br /><br /> -Si una aplicación cliente intenta crear un cubo local con una instrucción INSERT INTO que contiene la palabra clave PASSTHROUGH.<br />-Si una aplicación cliente intenta actualizar un cubo local que contiene una instrucción INSERT INTO que utiliza la palabra clave PASSTHROUGH.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Nombre|Valor|Descripción|  
|----------|-----------|-----------------|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT|*0*|Este valor se trata como DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE.<br /><br /> En el caso de las conexiones a un cubo local, este valor depende de si se utiliza la propiedad de cadena de conexión CREATECUBE. Si se utiliza la propiedad de cadena de conexión CREATECUBE, este valor es el mismo que DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL. De lo contrario, este valor es igual que DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL|*1*|Este valor habilita todas las bibliotecas de funciones definidas por el usuario sin comprobar si son seguras para inicialización y scripting. Para las conexiones a cubos locales, este valor habilita el uso de procedimientos almacenados y de la palabra clave PASSTHROUGH en instrucciones INSERT INTO.<br /><br /> **No se recomienda esta opción**.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE|*2*|Este valor garantiza que se comprueba que todas las clases de una biblioteca de funciones definidas por el usuario son seguras para inicialización y scripting. Para las conexiones a cubos locales, este valor evita el uso de la palabra clave PASSTHROUGH en instrucciones INSERT INTO y de procedimientos almacenados donde la propiedad PermissionSet no está establecida en Safe.<br /><br /> Este valor también quita las acciones en el [MDSCHEMA_ACTIONS](../../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) de filas de esquema que tiene un valor de HTML o comando en la columna ACTION_TYPE o tienen un valor de dirección URL en la columna ACTION_TYPE y un valor en la columna de contenido que no lo hace comenzar con "http://" o "https://".|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE|*3*|Este valor impide que se usen funciones definidas por el usuario durante la sesión. En las conexiones a cubos locales, este valor impide el uso de todos los procedimientos almacenados y de la palabra clave PASSTHROUGH en instrucciones INSERT INTO.<br /><br /> Este valor quita también todas las acciones del conjunto de filas de esquema MDSCHEMA_ACTIONS.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|SecuredCellValue|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Especifica el código de error y los valores de las propiedades de celda `Value` y `Formatted Value` que se devuelven cuando intenta obtener acceso a una celda protegida.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*0*|(Valor predeterminado) Por compatibilidad con versiones anteriores, este valor es igual a *1*. El significado de este valor predeterminado podría cambiar en versiones futuras.|  
|*1*|Devuelve: HRESULT = NO_ERROR<br /><br /> La propiedad `Value` de la celda contiene el resultado como un tipo de datos Variant. En la propiedad `Formatted Value` se devuelve la cadena "#N/A".|  
|*2*|Devuelve un error como valor de HRESULT.|  
|*3*|Devuelve NULL en las dos propiedades `Value` y `Formatted Value`.|  
|*4*|Devuelve un valor numérico cero (0) en la propiedad `Value` y un cero formateado en la propiedad `Formatted Value`. Por ejemplo, se devuelve 0.00 en la propiedad `Formatted Value` para una celda cuya propiedad `Format` es "#. ##."|  
|*5*|Devuelve la cadena "#SEC" en las dos propiedades `Value` y `Formatted Value`.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|ServerName|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, DBPROP_SERVERNAME.<br /><br /> El valor predeterminado de esta propiedad es el nombre de la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|ShowHiddenCubes|*Uso*<br /> Opcional, lectura/escritura `Boolean` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> El valor predeterminado de esta propiedad es FALSE.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|SQLQueryMode|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Determina si se incluyen cálculos en las consultas SQL.<br /><br /> El valor predeterminado de esta propiedad es *calculado*.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.<br /><br /> Esta propiedad puede tener uno de los valores descritos en la tabla siguiente.|  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Datos*|No se incluyen cálculos.|  
|*Calcula*|Se devuelven cálculos.|  
|*IncludeEmpty*|Se devuelven cálculos y filas vacías.|  
  
|Nombre|Elemento|  
|----------|-------------|  
|SQLSupport|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> El valor predeterminado de esta propiedad es 512.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|SspropInitAppName|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Contiene el nombre de la aplicación cliente.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|SspropInitPacketsize|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Contiene el identificador de la aplicación cliente.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|SspropInitWsid|*Uso*<br /> Opcional, lectura/escritura `String` propiedad<br /><br /> *Description*<br /> Contiene el identificador de la estación de trabajo cliente.<br /><br /> No existe un valor predeterminado para esta propiedad.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|StateSupport|*Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Especifica en qué medida se admite la disponibilidad de estados.<br /><br /> *Ninguno* = <br />                        No se admite la disponibilidad de estados.<br /><br /> *Las sesiones* = estados se proporcionan a través de la compatibilidad de la sesión.<br /><br /> Para obtener más información acerca de la disponibilidad de Estados y la compatibilidad con sesiones, consulte [administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).<br /><br /> El valor predeterminado de esta propiedad es *sesiones*.<br /><br /> Esta propiedad se puede utilizar con el método `Discover`.|  
|Timeout|*Uso*<br /> Opcional, lectura/escritura `Integer` propiedad<br /><br /> *Description*<br /> Especifica, en segundos, el tiempo máximo que debería esperar la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para que se realice una solicitud correctamente antes de devolver un error. Esta propiedad determina también el tiempo máximo que debería esperar la instancia a que se realice correctamente una actualización de una tabla de reescritura antes de devolver un error; es equivalente a la propiedad de cadena de conexión, Writeback Timeout.<br /><br /> El valor predeterminado de esta propiedad es cero (0).<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|TransactionDDL|*Uso*<br /> Opcional, solo lectura `Integer` propiedad<br /><br /> *Description*<br /> Reservado para uso futuro.<br /><br /> El valor predeterminado de esta propiedad es 0.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
|UserName|Este propiedad ya no se admite.<br /><br /> *Uso*<br /> Opcional, solo lectura `String` propiedad<br /><br /> *Description*<br /> Especifica una cadena que devuelve el nombre de usuario que asocia la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con el comando. Para que no haya problemas de compatibilidad con versiones anteriores, esta propiedad se omite sin generar ningún error cuando se usa con el método `Execute` o `Discover`. Esta propiedad equivale a la propiedad OLE DB, DBPROP_USERNAME.<br /><br /> El valor predeterminado para esta propiedad es el nombre de usuario con el que se inició la sesión o la conexión actual.<br /><br /> Esta propiedad se puede utilizar con el método `Execute`.|  
|VisualMode|*Uso*<br /> Opcional, solo escritura `Integer` propiedad<br /><br /> *Description*<br /> Esta propiedad equivale a la propiedad OLE DB, MDPROP_VISUALMODE.<br /><br /> El valor predeterminado de esta propiedad es cero (0), que equivale a DBPROPVAL_VISUAL_MODE_DEFAULT.<br /><br /> Esta propiedad se puede utilizar con los métodos `Discover` y `Execute`.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento PropertyList &#40;XMLA&#41;](propertylist-element-xmla.md)  
  
  
