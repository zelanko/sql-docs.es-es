---
description: Propiedades personalizadas de transformación
title: Propiedades personalizadas de transformación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1219bf8b502d7e91194b3413910aa7ae16ec09c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425697"
---
# <a name="transformation-custom-properties"></a>Propiedades personalizadas de transformación

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Además de las propiedades que son comunes a la mayoría de los objetos de flujo de datos en el modelo de objetos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], muchos objetos de flujo de datos tienen propiedades personalizadas que son específicas del objeto. Estas propiedades personalizadas solo están disponibles en tiempo de ejecución y no se incluyen en la documentación de referencia de la programación administrada de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
 En este tema se enumeran y describen las propiedades personalizadas de las diversas transformaciones de flujo de datos. Para obtener información sobre las propiedades comunes a la mayor parte de los objetos de flujo de datos, vea [Propiedades comunes](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Algunas propiedades de transformaciones se pueden establecer mediante expresiones de propiedad. Para obtener más información, vea [Propiedades de flujo de datos que se pueden establecer utilizando expresiones](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8).  
  
## <a name="transformations-with-custom-properties"></a>Transformaciones con propiedades personalizadas  

:::row:::
    :::column:::
        [Agregada](#aggregate)  
        [Auditoría](#audit)  
        [Transformación de caché](#cachetransform)  
        [Mapa de caracteres](#charmap)  
        [División condicional](#condsplit)  
        [Copiar columna](#copymap)  
        [Conversión de datos](#dataconv)  
        [Consulta de minería de datos](#dmquery)  
        [Columna derivada](#derived)  
    :::column-end:::
    :::column:::
        [Exportar columna](#extract)  
        [agrupación aproximada](#fgroup)  
        [Búsqueda aproximada](#flookup)  
        [Importar columna](#insert)  
        [Lookup](#lookup)  
        [Merge Join](#mjoin)  
        [Comando de OLE DB](#oledbcmd)  
        [Muestreo de porcentaje](#percent)  
        [Dinamización](#pivot)  
    :::column-end:::
    :::column:::
        [Recuento de filas](#rowcount)  
        [Muestreo de fila](#rowsamp)  
        [Componente de script](#script)  
        [Dimensión de variación lenta](#scd)  
        [Sort](#sort)  
        [Extracción de términos](#textract)  
        [Búsqueda de términos](#tlookup)  
        [Anulación de dinamización](#unpivot)  
    :::column-end:::
:::row-end:::

### <a name="transformations-without-custom-properties"></a>Transformaciones sin propiedades personalizadas  
 Las transformaciones siguientes no tienen ninguna propiedad personalizada en los niveles de componente, entrada o salida: [Transformación Mezclar](../../../integration-services/data-flow/transformations/merge-transformation.md), [Transformación Multidifusión](../../../integration-services/data-flow/transformations/multicast-transformation.md), y [Transformación Unión de todo](../../../integration-services/data-flow/transformations/union-all-transformation.md). Utilizan solo las propiedades comunes a todos los componentes de flujo de datos.  
  
##  <a name="aggregate-transformation-custom-properties"></a><a name="aggregate"></a> Propiedades personalizadas de la transformación Agregado  
 La transformación Agregado tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Agregado. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Entero|Valor comprendido entre 1 y 100 que especifica el porcentaje en el que se puede ampliar la memoria durante la agregación. El valor predeterminado de esta propiedad es **25**.|  
|CountDistinctKeys|Entero|Valor que especifica el número exacto de recuentos distintos que la agregación puede escribir. Si se especifica un valor de CountDistinctScale, el valor de CountDistinctKeys tiene precedencia.|  
|CountDistinctScale|Integer (enumeración)|Valor que describe el número aproximado de valores distintos en una columna que la agregación puede contar. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Bajo** (1): indica hasta 500 000 valores de clave.<br /><br /> **Medio** (2): indica hasta cinco millones de valores de clave.<br /><br /> **Alto** (3): indica más de 25 millones de valores de clave.<br /><br /> **No especificado** (0): indica que no se usa ningún valor de CountDistinctScale. El uso de la opción **No especificado** (0) puede afectar al rendimiento en conjuntos de datos grandes.|  
|Claves|Entero|Valor que especifica el número exacto de claves Group By que la agregación escribe. Si se especifica un valor de KeyScale, el valor de Keys tiene precedencia.|  
|KeyScale|Integer (enumeración)|Valor que describe aproximadamente cuántos valores de clave Group By puede escribir el agregado. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Bajo** (1): indica hasta 500 000 valores de clave.<br /><br /> **Medio** (2): indica hasta cinco millones de valores de clave.<br /><br /> **Alto** (3): indica más de 25 millones de valores de clave.<br /><br /> **No especificado** (0): indica que no se usa ningún valor de KeyScale.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de la salida de transformación Agregado. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Claves|Entero|Valor que especifica el número exacto de las claves Group By que la agregación puede escribir. Si se especifica un valor de KeyScale, el valor de Keys tiene precedencia.|  
|KeyScale|Integer (enumeración)|Valor que describe aproximadamente cuántos valores de clave Group By puede escribir el agregado. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Bajo** (1): indica hasta 500 000 valores de clave.<br /><br /> **Medio** (2): indica hasta cinco millones de valores de clave.<br /><br /> **Alto** (3): indica más de 25 millones de valores de clave.<br /><br /> **No especificado** (0): indica que no se usa ningún valor de KeyScale.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Agregado. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Entero|**LineageID** de una columna que participa en las funciones de agregado o GROUP BY.|  
|AggregationComparisonFlags|Entero|Valor que especifica cómo compara la transformación Agregado los datos de cadena de una columna. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|AggregationType|Integer (enumeración)|Valor que especifica la operación de la agregación que se va a realizar en la columna. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Agrupar por** (0)<br /><br /> **Recuento** (1)<br /><br /> **Contar todos** (2)<br /><br /> **CountDistinct** (3)<br /><br /> **Suma** (4)<br /><br /> **Promedio** (5)<br /><br /> **Máximo** (7)<br /><br /> **Mínimo** (6)|  
|CountDistinctKeys|Entero|Cuando el tipo de agregación es **Count distinct**, valor que especifica el número exacto de claves que la agregación puede escribir. Si se especifica un valor de CountDistinctScale, el valor de CountDistinctKeys tiene precedencia.|  
|CountDistinctScale|Integer (enumeración)|Cuando el tipo de agregación es **Count distinct**, un valor que describe aproximadamente cuántos valores de clave puede escribir la agregación. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Bajo** (1): indica hasta 500 000 valores de clave.<br /><br /> **Medio** (2): indica hasta cinco millones de valores de clave.<br /><br /> **Alto** (3): indica más de 25 millones de valores de clave.<br /><br /> **No especificado** (0): indica que no se usa ningún valor de CountDistinctScale.|  
|IsBig|Boolean|Valor que indica si la columna contiene un valor mayor que cuatro mil millones o un valor con más precisión que un valor de coma flotante de precisión doble. El valor puede ser 0 o 1. 0 indica que IsBig es **False** y la columna no contiene un valor grande o preciso. El valor predeterminado de esta propiedad es 1.|  
  
 La entrada y las columnas de entrada de la transformación Agregado no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
##  <a name="audit-transformation-custom-properties"></a><a name="audit"></a> Propiedades personalizadas de la transformación Auditar  
 La transformación Auditar tiene solo las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Auditar. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Integer (enumeración)|Elemento de auditoría seleccionado para la salida. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **GUID de instancia de ejecución** (0)<br /><br /> **Hora de inicio de ejecución** (4)<br /><br /> **Nombre de la máquina** (5)<br /><br /> **Identificador del paquete** (1)<br /><br /> **Nombre del paquete** (2)<br /><br /> **Identificador de tarea** (8)<br /><br /> **Nombre de tarea** (7)<br /><br /> **Nombre de usuario** (6)<br /><br /> **Identificador de versión** (3)|  
  
 La entrada, las columnas de entrada y la salida de transformación Auditar no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, consulte [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md).  
  
##  <a name="cache-transform-transformation-custom-properties"></a><a name="cachetransform"></a> Propiedades personalizadas de la transformación Transformación de caché  
 La transformación Transformación de caché tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades de la transformación Transformación de caché. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Connectionmanager|String|Especifica el nombre del administrador de conexiones.|  
|ValidateExternalMetadata|Boolean|Indica si la Transformación de caché se valida con los orígenes de datos externos en tiempo de diseño. Si la propiedad está establecida en **False**, la validación en los orígenes de datos externos se produce en tiempo de ejecución.<br /><br /> El valor predeterminado es **True**.|  
|AvailableInputColumns|String|Lista de columnas de entrada disponibles.|  
|InputColumns|String|Lista de las columnas de entrada seleccionadas.|  
|CacheColumnName|String|Especifica el nombre de la columna que está asignada a una columna de entrada seleccionada.<br /><br /> El nombre de la columna en la propiedad CacheColumnName debe coincidir con el nombre de la columna correspondiente que se muestra en la página **Columnas** del **Editor del administrador de conexiones de caché**.<br /><br /> Para obtener más información, vea [Editor del administrador de conexiones de caché](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).|  
  
##  <a name="character-map-transformation-custom-properties"></a><a name="charmap"></a> Propiedades personalizadas de la transformación Mapa de caracteres  
 La transformación Mapa de caracteres tiene solo las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Mapa de caracteres. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Entero|Valor que especifica el valor de **LineageID** de la columna de entrada que es el origen de la columna de salida.|  
|MapFlags|Integer (enumeración)|Valor que especifica las operaciones de cadena que la transformación Mapa de caracteres realiza en la columna. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Inversión de byte** (2)<br /><br /> **Formato completo** (6)<br /><br /> **Formato medio** (5)<br /><br /> **Hiragana** (3)<br /><br /> **Katakana** (4)<br /><br /> **Utilización lingüística de mayúsculas y minúsculas** (7)<br /><br /> **Minúsculas** (0)<br /><br /> **Chino simplificado** (8)<br /><br /> **Chino tradicional**(9)<br /><br /> **Mayúsculas** (1)|  
  
 La entrada, las columnas de entrada y la salida de transformación Mapa de caracteres no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Mapa de caracteres](../../../integration-services/data-flow/transformations/character-map-transformation.md).  
  
##  <a name="conditional-split-transformation-custom-properties"></a><a name="condsplit"></a> Propiedades personalizadas de la transformación División condicional  
 La transformación División condicional tiene solo las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación División condicional. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Entero|Valor que especifica la posición de una condición, asociada a una salida, en la lista de condiciones que la transformación División condicional evalúa. Las condiciones se evalúan en orden, del mínimo al máximo.|  
|Expression|String|Expresión que representa la condición que la transformación División condicional evalúa. Las columnas se representan mediante identificadores de linaje.|  
|FriendlyExpression|String|Expresión que representa la condición que la transformación División condicional evalúa. Las columnas se representan mediante su nombre.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|IsDefaultOut|Boolean|Valor que indica si la salida es la salida predeterminada.|  
  
 La entrada, las columnas de entrada y de salida de transformación División condicional no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
##  <a name="copy-column-transformation-custom-properties"></a><a name="copymap"></a> Propiedades personalizadas de la transformación Copiar columna  
 La transformación Copiar columna solo tiene las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Copiar columna. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|copyColumnId|Entero|**LineageID** de la columna de entrada de la que se copia la columna de salida.|  
  
 La entrada, las columnas de entrada y la salida de transformación Copiar columna no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Copiar columna](../../../integration-services/data-flow/transformations/copy-column-transformation.md).  
  
##  <a name="data-conversion-transformation-custom-properties"></a><a name="dataconv"></a> Propiedades personalizadas de la transformación Conversión de datos  
 La transformación Conversión de datos tiene solo las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Conversión de datos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|Valor que indica si la columna usa las rutinas de análisis más rápidas que no distinguen la configuración regional y permiten un análisis rápido que [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona, o las rutinas de análisis estándar, que sí distinguen la configuración regional. El valor predeterminado de esta propiedad es **False**. Para obtener más información, consulte [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) y [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013). .<br /><br /> Nota: Esta propiedad no está disponible en **Editor de transformación Conversión de datos**, pero se puede definir con el **Editor avanzado**.|  
|SourceInputColumnLineageId|Entero|**LineageID** de la columna de entrada que es el origen de la columna de salida.|  
  
 La entrada, las columnas de entrada y la salida de transformación Conversión de datos no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
##  <a name="data-mining-query-transformation-custom-properties"></a><a name="dmquery"></a> Propiedades personalizadas de la transformación Consulta de minería de datos  
 La transformación Consulta de minería de datos tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Consulta de minería de datos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|El identificador único del objeto de conexión.|  
|ASConnectionString|String|Cadena de conexión a un proyecto de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|CatalogName|String|Nombre de una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|ModelName|String|Nombre del modelo de minería de datos.|  
|ModelStructureName|String|Nombre de la estructura de minería de datos.|  
|ObjectRef|String|Etiqueta XML que identifica la estructura de minería de datos que la transformación usa:|  
|QueryText|String|Instrucción de consulta de predicción que la transformación utiliza.|  
  
 La entrada, las columnas de entrada y la salida de las columnas de salida de transformación Consulta de minería de datos no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Consulta de minería de datos](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md).  
  
##  <a name="derived-column-transformation-custom-properties"></a><a name="derived"></a> Propiedades personalizadas de la transformación Columna derivada  
 La transformación Columna derivada solo tiene las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada y de las columnas de salida de transformación Columna derivada. Cuando elige agregar la columna derivada como una columna nueva, estas propiedades personalizadas se aplican a la nueva columna de resultados; cuando decide reemplazar el contenido de una columna de entrada existente con los resultados derivados, estas propiedades personalizadas se aplican a la columna de entrada existente. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Expression|String|Expresión que representa la condición que la transformación División condicional evalúa. La propiedad **LineageID** de la columna representa las columnas.|  
|FriendlyExpression|String|Expresión que representa la condición que la transformación División condicional evalúa. Las columnas se representan mediante su nombre.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 La entrada y la salida de transformación Columna derivada no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
##  <a name="export-column-transformation-custom-properties"></a><a name="extract"></a> Propiedades personalizadas de la transformación Exportar columna  
 La transformación Exportar columna solo tiene las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Exportar columna. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|Valor que especifica si desea que la transformación anexe los datos a un archivo existente. El valor predeterminado de esta propiedad es **False**.|  
|ForceTruncate|Boolean|Valor que especifica si la transformación trunca un archivo existente antes de escribir los datos. El valor predeterminado de esta propiedad es **False**.|  
|FileDataColumnID|Entero|Valor que identifica la columna que contiene los datos que la transformación inserta en un archivo. En la Columna Extraer, esta propiedad tiene el valor **0**; en la columna Ruta de archivo, esta propiedad contiene el valor de **LineageID** de la columna Extraer.|  
|WriteBOM|Boolean|Valor que especifica si se escribe una marca de orden de bytes (BOM) en el archivo.|  
  
 La entrada, la salida y las columnas de salida de transformación Exportar columna no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Exportar columna](../../../integration-services/data-flow/transformations/export-column-transformation.md).  
  
##  <a name="import-column-transformation-custom-properties"></a><a name="insert"></a> Propiedades personalizadas de la transformación Importar columna  
 La transformación Importar columna solo tiene las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Importar columna. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|Valor que especifica si la transformación Importar columna espera una marca de orden de bytes (BOM). Solo se espera una marca BOM si los datos tienen el tipo de datos DT_NTEXT.|  
|FileDataColumnID|Entero|Valor que identifica la columna que contiene los datos que la transformación inserta en el flujo de datos. En la columna de datos que se van a insertar, esta propiedad tiene el valor 0; en la columna que contiene las rutas de acceso del archivo de origen, esta propiedad contiene el valor de **LineageID** de la columna de datos que se van a insertar.|  
  
 La entrada, la salida y las columnas de salida de transformación Importar columna no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Importar columna](../../../integration-services/data-flow/transformations/import-column-transformation.md).  
  
##  <a name="fuzzy-grouping-transformation-custom-properties"></a><a name="fgroup"></a> Propiedades personalizadas de la transformación Agrupación aproximada  
 La transformación Agrupación aproximada tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Agrupación aproximada. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Delimitadores|String|Los delimitadores de token que la transformación utiliza. Los delimitadores predeterminados incluyen los caracteres siguientes: espacio ( ), coma (,), punto (.), punto y coma (;), dos puntos (:), guión (-), comillas rectas dobles ("), comillas rectas sencillas ('), y comercial (&), barra diagonal (/), barra diagonal inversa (\\), arroba (@), signo de exclamación (!), signo de interrogación (?), paréntesis de apertura ((), paréntesis de cierre ()), menor que (\<), greater than (>), corchete de apertura ([), corchete de cierre (]), llave de apertura ({), llave de cierre (}), barra vertical (&#124;), signo de número (#), asterisco (*), símbolo de intercalación (^) y porcentaje (%).|  
|Exhaustive|Boolean|Valor que especifica si cada registro de entrada se compara con el resto. El valor de **True** está destinado sobre todo a fines de depuración. El valor predeterminado de esta propiedad es **False**.<br /><br /> Nota: Esta propiedad no está disponible en **Editor de transformación Agrupación aproximada**, pero se puede definir con el **Editor avanzado**.|  
|MaxMemoryUsage|Entero|Cantidad de memoria máxima que puede usar la transformación. El valor predeterminado de esta propiedad es **0**, que habilita el uso de la memoria dinámica.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.<br /><br /> Nota: Esta propiedad no está disponible en **Editor de transformación Agrupación aproximada**, pero se puede definir con el **Editor avanzado**.|  
|MinSimilarity|Double|Umbral de similitud que la transformación utiliza para identificar los duplicados, expresado como un valor entre 0 y 1.  El valor predeterminado de esta propiedad es 0.8.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Agrupación aproximada. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Integer (enumeración)|Valor que especifica si la transformación realiza una coincidencia aproximada o una coincidencia exacta. Los valores válidos son **Exacta** y **Aproximada**. El valor predeterminado de esta propiedad es **Aproximada**.|  
|FuzzyComparisonFlags|Integer (enumeración)|Valor que especifica cómo compara la transformación los datos de cadena de una columna. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|LeadingTrailingNumeralsSignificant|Integer (enumeración)|Valor que especifica la importancia de los numerales. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **NumeralsNotSpecial** (0): se usa si los números no son significativos.<br /><br /> **LeadingNumeralsSignificant** (1): se usa si los números iniciales son significativos.<br /><br /> **TrailingNumeralsSignificant** (2): se usa si los números finales son significativos.<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3): se usa si los números iniciales y finales son significativos.|  
|MinSimilarity|Double|Umbral de similitud que se usa para la combinación en la columna, especificado como un valor entre 0 y 1. Solo las filas mayores que el umbral se consideran coincidencias.|  
|ToBeCleaned|Boolean|Valor que especifica si la columna se utiliza para identificar los duplicados; es decir, si se trata de una columna en la que está agrupando. El valor predeterminado de esta propiedad es **False**.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Agrupación aproximada. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|ColumnType|Integer (enumeración)|Valor que identifica el tipo de columna de resultados. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Undefined** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonical**(6)|  
|InputID|Entero|**LineageID** de la columna de entrada correspondiente.|  
  
 La entrada y la salida de transformación Agrupación aproximada no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Agrupación aproximada](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
##  <a name="fuzzy-lookup-transformation-custom-properties"></a><a name="flookup"></a> Propiedades personalizadas de la transformación Búsqueda aproximada  
 La transformación Búsqueda aproximada tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Búsqueda aproximada. Todas las propiedades excepto **ReferenceMetadataXML** son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|Especifica si se debería crear una copia de la tabla de referencia para la construcción del índice de búsqueda aproximada y las búsquedas subsiguientes. El valor predeterminado de esta propiedad es **True**.|  
|Delimitadores|String|Delimitadores que la transformación utilizará para dividir en tokens los valores de las columnas. Los delimitadores predeterminados incluyen los caracteres siguientes: espacio ( ), coma (,), punto (.), punto y coma (;), dos puntos (:), guión (-), comillas rectas dobles ("), comillas rectas sencillas ('), y comercial (&), barra diagonal (/), barra diagonal inversa (\\), arroba (@), signo de exclamación (!), signo de interrogación (?), paréntesis de apertura ((), paréntesis de cierre ()), menor que (\<), greater than (>), corchete de apertura ([), corchete de cierre (]), llave de apertura ({), llave de cierre (}), barra vertical (&#124;). almohadilla (#), asterisco (*), símbolo de intercalación (^) y porcentaje (%).|  
|DropExistingMatchIndex|Boolean|Valor que especifica si el índice de coincidencia especificado en MatchIndexName se elimina cuando MatchIndexOptions no se establece en ReuseExistingIndex. El valor predeterminado de esta propiedad es **True**.|  
|Exhaustive|Boolean|Valor que especifica si cada registro de entrada se compara con el resto. El valor de **True** está destinado sobre todo a fines de depuración. El valor predeterminado de esta propiedad es **False**.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de transformación Búsqueda aproximada**, pero se puede definir con el **Editor avanzado**.|  
|MatchIndexName|String|Nombre del índice de coincidencia. El índice de coincidencia es la tabla en la que la transformación crea y guarda el índice que utiliza. Si se reutiliza el índice de coincidencia, MatchIndexName especifica el índice que se reutilizará. MatchIndexName debe ser un nombre de identificador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válido. Por ejemplo, si el nombre contiene espacios, debe escribirse entre corchetes.|  
|MatchIndexOptions|Integer (enumeración)|Valor que especifica cómo administra la transformación el índice de coincidencia. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Entero|Tamaño máximo permitido de la caché para la tabla de búsqueda. El valor predeterminado de esta propiedad es **0**, lo que significa que el tamaño de la memoria caché no tiene límite.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de transformación Búsqueda aproximada**, pero se puede definir con el **Editor avanzado**.|  
|MaxOutputMatchesPerInput|Entero|Número máximo de coincidencias que la transformación puede devolver para cada fila de entrada. El valor predeterminado de esta propiedad es **1**.<br /><br /> Nota: Los valores mayores que 100 solo se pueden especificar con el **Editor avanzado**.|  
|MinSimilarity|Entero|El umbral de similitud que la transformación usa en el nivel de componente, especificado como un valor entre 0 y 1. Solo las filas mayores que el umbral se consideran coincidencias.|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|Nombre de la tabla de búsqueda. El nombre debe ser un nombre de identificador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válido. Por ejemplo, si el nombre contiene espacios, debe escribirse entre corchetes.|  
|WarmCaches|Boolean|Cuando es true, la búsqueda carga parcialmente el índice y la tabla de referencia en la memoria antes de comenzar la ejecución. Esto puede mejorar el rendimiento.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Búsqueda aproximada. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Entero|Valor que especifica cómo compara la transformación los datos de cadena de una columna. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|FuzzyComparisonFlagsEx|Integer (enumeración)|Valor que especifica qué marcas de comparación extendida usa la transformación. Los valores pueden incluir **MapExpandLigatures, MapFoldCZone**, **MapFoldDigits**, **MapPrecomposed**y **NoMapping**. **NoMapping** no se puede usar con otras marcas.|  
|JoinToReferenceColumn|String|Valor que especifica el nombre de la columna en la tabla de referencia con la que se combina la columna.|  
|JoinType|Entero|Valor que especifica si la transformación realiza una coincidencia aproximada o exacta. El valor predeterminado de esta propiedad es **Aproximada**. El valor entero para el tipo de combinación exacta es **1** y para el tipo de combinación aproximado es **2**.|  
|MinSimilarity|Double|Umbral de similitud que la transformación usa en el nivel de columna, especificado como un valor entre 0 y 1. Solo las filas mayores que el umbral se consideran coincidencias.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Búsqueda aproximada. Todas las propiedades son de lectura y escritura.  
  
> [!NOTE]  
>  Para las columnas de salida que contienen los valores de paso a través de las columnas de entrada correspondientes, CopyFromReferenceColumn está vacío y SourceInputColumnLineageID contiene el valor de **LineageID** de la columna de entrada correspondiente. Para las columnas de salida que contienen los resultados de la búsqueda, CopyFromReferenceColumn contiene el nombre de la columna de búsqueda y SourceInputColumnLineageID está vacío.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ColumnType|Integer (enumeración)|Valor que identifica el tipo de columna de resultados para las columnas que la transformación agrega a la salida. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **Undefined** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confidence** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|String|Valor que especifica el nombre de la columna en la tabla de referencia que proporciona el valor en una columna de resultados.|  
|SourceInputColumnLineageId|Entero|Valor que identifica la columna de entrada que proporciona los valores de esta columna de resultados.|  
  
 La entrada y la salida de transformación Búsqueda aproximada no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Búsqueda aproximada](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
##  <a name="lookup-transformation-custom-properties"></a><a name="lookup"></a> Propiedades personalizadas de la transformación Búsqueda  
 La transformación Búsqueda tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Búsqueda. Todas las propiedades excepto **ReferenceMetadataXML** son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CacheType|Integer (enumeración)|Tipo de caché para la tabla de búsqueda. Los valores son **Full** (0), **Partial** (1) y **None** (2). El valor predeterminado de esta propiedad es **Full**.|  
|DefaultCodePage|Entero|Página de códigos predeterminada que se usa cuando no hay información disponible de la misma en el origen de datos.|  
|MaxMemoryUsage|Entero|Tamaño máximo permitido de la caché para la tabla de búsqueda. El valor predeterminado de esta propiedad es **25**, lo que significa que el tamaño de la memoria caché no tiene límite.|  
|MaxMemoryUsage64|Entero|Tamaño de caché máximo para la tabla de búsqueda en un equipo de 64 bits.|  
|NoMatchBehavior|Integer (enumeración)|Valor que especifica si las filas que no tienen entradas coincidentes del conjunto de datos de referencia se tratan como errores.<br /><br /> Cuando la propiedad se establece en **Tratar filas sin entradas coincidentes como errores** (0), las filas sin entradas coincidentes se tratan como errores. Puede especificar lo que debería pasar cuando se produce este tipo de error con la página **Salida de error** del cuadro de diálogo **Editor de transformación Búsqueda** . Para obtener más información, vea [Editor de transformación Búsqueda &#40;página Salida de error&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).<br /><br /> Cuando la propiedad está establecida en **Enviar las filas sin entradas coincidentes a la salida de entradas no coincidentes** (1), las filas no se tratan como errores.<br /><br /> El valor predeterminado es **Tratar filas sin entradas coincidentes como errores** (0).|  
|ParameterMap|String|Lista delimitada por puntos y comas de identificadores de linaje que se asignan a los parámetros que se usan en la instrucción **SqlCommand** .|  
|ReferenceMetadataXML|String|Metadatos para las columnas en la tabla de búsqueda que la transformación copia en su salida.|  
|SqlCommand|String|La instrucción SELECT que rellena la tabla de búsqueda.|  
|SqlCommandParam|String|La instrucción SQL parametrizada que rellena la tabla de búsqueda.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Búsqueda. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|Nombre de la columna en la tabla de referencia desde la que se copia una columna.|  
|JoinToReferenceColumns|String|El nombre de la columna de la tabla de referencia con la que una columna de origen se combina.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Búsqueda. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|Nombre de la columna en la tabla de referencia desde la que se copia una columna.|  
  
 La entrada y la salida de transformación Búsqueda no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
##  <a name="merge-join-transformation-custom-properties"></a><a name="mjoin"></a> Propiedades personalizadas de la Transformación Combinación de mezcla  
 La transformación Combinación de mezcla tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Combinación de mezcla.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|JoinType|Integer (enumeración)|Especifica si la combinación es una combinación interna (2), externa izquierda (1) o completa (0).|  
|MaxBuffersPerInput|Entero|Ya no tiene que configurar el valor de la propiedad **MaxBuffersPerInput** porque Microsoft ha realizado modificaciones que reducen el riesgo de que la transformación Combinación de mezcla utilice demasiada memoria. Este problema se producía a veces cuando varias entradas de la Combinación de mezcla generaban datos a velocidades desiguales.|  
|NumKeyColumns|Entero|Número de columnas que se utilizan en la combinación.|  
|TreatNullsAsEqual|Boolean|Valor que especifica si la transformación trata los valores nulos como valores iguales. El valor predeterminado de esta propiedad es **True**. Si el valor de la propiedad es **False**, la transformación trata los valores NULL como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Combinación de mezcla. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|InputColumnID|Entero|**LineageID** de la columna de entrada desde la que los datos se copian en esta columna de salida.|  
  
 La entrada, las columnas de entrada y la salida de transformación Combinación de mezcla no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Combinación de mezcla](../../../integration-services/data-flow/transformations/merge-join-transformation.md).  
  
##  <a name="ole-db-command-transformation-custom-properties"></a><a name="oledbcmd"></a> Propiedades personalizadas de la transformación Comando de OLE DB  
 La transformación Comando de OLE DB tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Comando de OLE DB.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|CommandTimeout|Entero|Número máximo de segundos que el comando SQL se puede ejecutar antes de superar el tiempo de espera. Si el valor es **0** , indica un tiempo infinito. El valor predeterminado de esta propiedad es **0**.|  
|DefaultCodePage|Entero|Página de códigos que se usa cuando no hay información disponible de la misma en el origen de datos.|  
|SqlCommand|String|La instrucción de Transact-SQL que la transformación ejecuta para cada fila en el flujo de datos.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas externas de la transformación Comando de OLE DB. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer (máscara de bits)|Conjunto de marcas que describen las características de los parámetros. Para obtener más información, vea DBPARAMFLAGSENUM en la documentación de OLE DB de MSDN Library.|  
  
 La entrada, las columnas de entrada, la salida y las columnas de salida de transformación Comando de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
##  <a name="percentage-sampling-transformation-custom-properties"></a><a name="percent"></a> Propiedades personalizadas de la transformación Muestreo de porcentaje  
 La transformación Muestreo de porcentaje tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Muestreo de porcentaje.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|SamplingSeed|Entero|Valor de inicialización que el generador de números aleatorios usa. El valor predeterminado de esta propiedad es **0**, lo que indica que la transformación usa un contador.|  
|SamplingValue|Entero|Tamaño del ejemplo como un porcentaje del origen.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las salidas de la transformación Muestreo de porcentaje. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Seleccionado|Boolean|Designa la salida a la que se dirigen las filas del muestreo. En la salida seleccionada, Selected se establece en **True**y, en la salida sin seleccionar, Selected se establece en **False**.|  
  
 La entrada, las columnas de entrada y las columnas de salida de transformación Muestreo de porcentaje no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Muestreo de porcentaje](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
##  <a name="pivot-transformation-custom-properties"></a><a name="pivot"></a> Propiedades personalizadas de la transformación Dinámica  
 En la tabla siguiente se describen las propiedades de componentes personalizadas de la transformación dinámica.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|Establezca esta opción en **True** para configurar la transformación dinámica con el fin de omitir las filas que contienen valores no reconocidos en la columna Clave dinámica y generar todos los valores de clave dinámica en un mensaje del registro, cuando se ejecuta el paquete.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Dinámica. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|PivotUsage|Integer (enumeración)|Valor que especifica el rol de una columna cuando se dinamiza el conjunto de datos.<br /><br /> **0**:<br />                      La columna no se dinamiza y los valores de la columna se pasan a la salida de transformación.<br /><br /> **1**:<br />                      La columna forma parte de la clave fija que identifica una o más filas como parte de un conjunto. Todas las filas de entrada con la misma clave fija se combinan en una sola fila de salida.<br /><br /> **2**:<br />                      La columna es una columna dinamizada. A partir de cada valor de columna se crea al menos una columna.<br /><br /> **3**:<br />                      Los valores de esta columna se colocan en columnas que se crean como resultado de la dinamización.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Dinámica. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|Uno de los valores posibles de la columna que se marca como la clave dinámica por el valor de su propiedad PivotUsage.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|SourceColumn|Entero|**LineageID** de una columna de entrada que contiene un valor dinamizado o -1. El valor -1 indica que la columna no se utiliza en una operación dinámica.|  
  
 Para obtener más información, vea [Transformación dinámica](../../../integration-services/data-flow/transformations/pivot-transformation.md).  
  
##  <a name="row-count-transformation-custom-properties"></a><a name="rowcount"></a> Propiedades personalizadas de la transformación Recuento de filas  
 La transformación Recuento de filas tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Recuento de filas. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|VariableName|String|Nombre de la variable que contiene el recuento de filas.|  
  
 La entrada, las columnas de entrada, la salida y las columnas de salida de transformación Recuento de filas no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md).  
  
##  <a name="row-sampling-transformation-custom-properties"></a><a name="rowsamp"></a> Propiedades personalizadas de la transformación Muestreo de fila  
 La transformación Muestreo de fila tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Muestreo de fila. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|SamplingSeed|Entero|Valor de inicialización que el generador de números aleatorios utiliza. El valor predeterminado de esta propiedad es **0**, lo que indica que la transformación usa un contador.|  
|SamplingValue|Entero|Recuento de filas del ejemplo.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las salidas de la transformación Muestreo de fila. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Seleccionado|Boolean|Designa la salida a la que se dirigen las filas del muestreo. En la salida seleccionada, Selected se establece en **True**y, en la salida sin seleccionar, Selected se establece en **False**.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Muestreo de fila. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Entero|Valor que especifica el valor de **LineageID** de la columna de entrada que es el origen de la columna de salida.|  
  
 La entrada y las columnas de entrada de la transformación Muestreo de fila no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
##  <a name="script-component-custom-properties"></a><a name="script"></a> Propiedades personalizadas del Componente de script  
 El componente de script tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos. Las mismas propiedades personalizadas están disponibles si el componente de script funciona como un origen, transformación o destino.  
  
 En la tabla siguiente se describen las propiedades personalizadas del componente de script. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Variables de solo lectura|String|Lista de variables separadas por comas disponible para el componente de script con acceso de solo lectura.|  
|Variables de lectura/escritura|String|Lista de variables separadas por comas disponible para el componente de script con acceso de lectura y escritura.|  
  
 La entrada, las columnas de entrada, la salida y las columnas de salida del componente de script no tienen ninguna propiedad personalizada, a menos que el desarrollador del script cree propiedades personalizadas para ellos.  
  
 Para más información, consulte [Script Component](../../../integration-services/data-flow/transformations/script-component.md).  
  
##  <a name="slowly-changing-dimension-transformation-custom-properties"></a><a name="scd"></a> Propiedades personalizadas de la transformación Dimensión de variación lenta  
 La transformación Dimensión de variación lenta tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Dimensión de variación lenta. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|Cláusula WHERE de la instrucción SELECT que selecciona la fila actual entre las filas con la misma clave empresarial.|  
|EnableInferredMember|Boolean|Valor que especifica si se detectan las actualizaciones de miembros deducidos. El valor predeterminado de esta propiedad es **True**.|  
|FailOnFixedAttributeChange|Boolean|Valor que especifica si se produce un error en la transformación cuando las columnas de fila con atributos fijos contienen cambios o también se produce un error en la búsqueda en la tabla de dimensiones. Si espera que las filas entrantes contengan registros nuevos, establezca este valor en **True** para hacer que la transformación continúe después de que se produzca el error en la búsqueda, porque la transformación usa el error para identificar los registros nuevos. El valor predeterminado de esta propiedad es **False**.|  
|FailOnLookupFailure|Boolean|Valor que especifica si se produce un error en la transformación cuando se produce un error en una búsqueda de un registro existente. El valor predeterminado de esta propiedad es **False**.|  
|IncomingRowChangeType|Entero|Valor que especifica si todas las filas entrantes son filas nuevas, o si la transformación debería detectar el tipo de cambio.|  
|InferredMemberIndicator|String|Nombre de columna del miembro deducido.|  
|SqlCommand|String|Instrucción SQL que se usa para crear un conjunto de filas de esquema.|  
|UpdateChangingAttributeHistory|Boolean|Valor que indica si las actualizaciones de atributos históricos se dirigen a la salida de transformación para cambiar las actualizaciones de atributos.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Dimensión de variación lenta. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ColumnType|Integer (enumeración)|Tipo de actualización de la columna. Los valores son: **Atributo variable** (2), **Atributo fijo** (4), **Atributo histórico** (3), **Clave** (1) y **Otro** (0).|  
  
 La entrada, las salidas y las columnas de resultados de la transformación Dimensión de variación lenta no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Dimensión de variación lenta](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
##  <a name="sort-transformation-custom-properties"></a><a name="sort"></a> Propiedades personalizadas de la transformación Ordenar  
 La transformación Ordenar tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Ordenar. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|Especifica si la transformación quita las filas duplicadas de la salida de transformación. El valor predeterminado de esta propiedad es **False**.|  
|MaximumThreads|Entero|Contiene el número máximo de subprocesos que la transformación puede utilizar para la ordenación. El valor **0** indica un número infinito de subprocesos. El valor predeterminado de esta propiedad es **0**.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Ordenación. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer (máscara de bits)|Valor que especifica cómo compara la transformación los datos de cadena de una columna. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|NewSortKeyPosition|Entero|Valor que especifica el criterio de ordenación de la columna. El valor 0 indica que los datos no están ordenados en esta columna.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Ordenar. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|SortColumnID|Entero|**LineageID** de una columna de ordenación.|  
  
 La entrada y la salida de transformación Ordenación no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md).  
  
##  <a name="term-extraction-transformation-custom-properties"></a><a name="textract"></a> Propiedades personalizadas de la transformación Extracción de términos  
 La transformación Extracción de términos tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Extracción de términos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Entero|Valor numérico que indica el número de veces que un término debe repetirse antes de extraerse. El valor predeterminado de esta propiedad es **2**.|  
|IsCaseSensitive|Boolean|Valor que especifica si se utiliza la distinción entre mayúsculas y minúsculas al extraer nombres y sintagmas nominales. El valor predeterminado de esta propiedad es **False**.|  
|MaxLengthOfTerm|Entero|Valor numérico que indica la longitud máxima de un término. Esta propiedad solo se aplica a las frases. El valor predeterminado de esta propiedad es **12**.|  
|NeedRefenceData|Boolean|Valor que especifica si la transformación utiliza una lista de condiciones de exclusión almacenada en una tabla de referencia. El valor predeterminado de esta propiedad es **False**.|  
|OutTermColumn|String|Nombre de la columna que contiene las condiciones de la exclusión.|  
|OutTermTable|String|Nombre de la tabla que contiene la columna con las condiciones de la exclusión.|  
|ScoreType|Entero|Valor que especifica el tipo de cuenta que asociar al término. Los valores válidos son 0, que indica la frecuencia, y 1, que indica una puntuación TFIDF. La puntuación TFIDF es el producto de la frecuencia del término y la frecuencia inversa del documento, tal y como se define a continuación: TFIDF de un término T = (frecuencia de T) \* log ((#filas en entrada)/(#filas con T)). El valor predeterminado de esta propiedad es **0**.|  
|WordOrPhrase|Entero|Valor que especifica el tipo de término. Los valores válidos son 0, que solamente indica palabras; 1, que solamente indica sintagmas nominales; y 2, que indica palabras y sintagmas nominales. El valor predeterminado de esta propiedad es **0**.|  
  
 La entrada, las columnas de entrada, la salida y las columnas de salida de transformación Extracción de términos no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Extracción de términos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
##  <a name="term-lookup-transformation-custom-properties"></a><a name="tlookup"></a> Propiedades personalizadas de la transformación Búsqueda de términos  
 La transformación Búsqueda de términos tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas de la transformación Búsqueda de términos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|Valor que especifica si una comparación con distinción entre mayúsculas y minúsculas se aplica a la coincidencia del texto de la columna de entrada y el término de búsqueda. El valor predeterminado de esta propiedad es **False**.|  
|RefTermColumn|String|Nombre de la columna que contiene los términos de la búsqueda.|  
|RefTermTable|String|Nombre de la tabla que contiene la columna con las condiciones de búsqueda.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Búsqueda de términos. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|InputColumnType|Entero|Valor que especifica el uso de la columna. Los valores válidos son 0 para una columna de paso a través, 1 para una columna de búsqueda y 2 para una columna que sea de paso a través y de búsqueda.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Búsqueda de términos. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Entero|**LineageID** de la columna de entrada correspondiente si **InputColumnType** de esa columna es 0 o 2.|  
  
 La entrada y la salida de transformación Búsqueda de términos no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
##  <a name="unpivot-transformation-custom-properties"></a><a name="unpivot"></a> Propiedades personalizadas de la transformación Anulación de dinamización  
 La transformación Anulación de dinamización tiene solo las propiedades comunes a todos los componentes de flujo de datos en el nivel de componente.  
  
> [!NOTE]  
>  Esta sección se basa en el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md) para ilustrar las opciones que se describen.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de entrada de la transformación Anulación de dinamización. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|DestinationColumn|Entero|**LineageID** de la columna de salida a la que asigna la columna de entrada. El valor -1 indica que la columna de entrada no está asignada a una columna de resultados.|  
|PivotKeyValue|String|Valor que se copia en una columna de salida de transformación.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.<br /><br /> En el escenario Anulación de dinamización que se describe en [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md), los valores de dinamización son los valores de texto Ham, Coke, Milk, Beer y Chips. Estos aparecerán como valores de texto en la nueva columna Product designada por la opción **Nombre de la columna del valor de clave dinámica** .|  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida de transformación Anulación de dinamización. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|Indica si los valores de la propiedad **PivotKeyValue** de las columnas de entrada se escriben en esta columna de salida.<br /><br /> En el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md), el nombre de la columna de valor dinámico es **Product** y designa la nueva columna **Product** en la que se anula la dinamización de las columnas Ham, Coke, Milk, Beer y Chips.|  
  
 La entrada y la salida de transformación Anulación de dinamización no tienen ninguna propiedad personalizada.  
  
 Para obtener más información, vea [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md).  
  
## <a name="see-also"></a>Consulte también  
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Propiedades comunes](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [Propiedades de la ruta de acceso](https://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [Propiedades de flujo de datos que se pueden establecer utilizando expresiones](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
