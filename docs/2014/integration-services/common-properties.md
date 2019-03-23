---
title: Propiedades comunes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- external metadata column properties [Integration Services]
- output properties [Integration Services]
- data types [Integration Services], properties
- input properties [Integration Services]
- component properties [Integration Services]
ms.assetid: 51973502-5cc6-4125-9fce-e60fa1b7b796
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ab92e158fe5da6312959cc0797ff48e1c44e0080
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378883"
---
# <a name="common-properties"></a>Propiedades comunes
  Los objetos de flujo de datos en el modelo de objetos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tienen propiedades comunes y propiedades personalizadas en el nivel del componente, de las entradas y salidas, y de las columnas de entrada y de salida. Muchas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
 En este tema se enumeran y describen las propiedades comunes de los objetos de flujo de datos.  
  
-   [Components](#components)  
  
-   [Entradas](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [Salidas](#outputs)  
  
-   [Columnas de salida](#outputcolumns)  
  
 Para obtener información acerca de propiedades cliente, vea los siguientes temas  
  
-   [Propiedades personalizadas de ADO NET](data-flow/ado-net-custom-properties.md)  
  
-   [Propiedades personalizadas de la tarea Control CDC](control-flow/cdc-control-task-custom-properties.md)  
  
-   [Propiedades personalizadas del origen de CDC](data-flow/cdc-source-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos](data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino DataReader](data-flow/datareader-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de procesamiento de dimensiones](data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Propiedades personalizadas de Excel](data-flow/excel-custom-properties.md)  
  
-   [Propiedades personalizadas de archivo plano](data-flow/flat-file-custom-properties.md)  
  
-   [Propiedades personalizadas de los destinos de ODBC](data-flow/odbc-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del origen ODBC](data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)Propiedades personalizadas de OLE DB  
  
-   [Propiedades personalizadas del destino de procesamiento de particiones](data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Propiedades personalizadas de archivo sin formato](data-flow/raw-file-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de conjunto de registros](data-flow/recordset-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de SQL Server Compact Edition](data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de SQL Server](data-flow/sql-server-destination-custom-properties.md)  
  
-   [Propiedades personalizadas de transformación](data-flow/transformations/transformation-custom-properties.md)  
  
-   [Propiedades personalizadas del origen XML](data-flow/xml-source-custom-properties.md)  
  
##  <a name="components"></a> Propiedades de componente  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 La tabla siguiente describe las propiedades de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|CLSID del componente.|  
|ContactInfo|String|Información de contacto para el programador de un componente.|  
|Descripción|String|Descripción del componente de flujo de datos. El valor predeterminado de esta propiedad es el nombre del componente de flujo de datos.|  
|Id.|Integer|Valor que identifica de forma única esta instancia del componente.|  
|IdentificationString|String|Identifica el componente.|  
|IsDefaultLocale|Boolean|Indica si el componente utiliza la configuración regional de la tarea Flujo de Datos a la que pertenece.|  
|LocaleID|Integer|Configuración regional que el componente de flujo de datos utiliza cuando el paquete se ejecuta. Todas las configuraciones regionales de Windows están disponibles para su uso en componentes de flujo de datos.|  
|Nombre|String|Nombre del componente de flujo de datos.|  
|PipelineVersion|Integer|La versión de la tarea de flujo de datos para la que se ha diseñado la ejecución de un componente.|  
|UsesDispositions|Boolean|Indica si un componente tiene una salida de error.|  
|ValidateExternalMetadata|Boolean|Indica si se validan los metadatos de columnas externas. El valor predeterminado de esta propiedad es `True`.|  
|Versión|Integer|Versión de un componente.|  
  
##  <a name="inputs"></a> Propiedades de entrada  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , las transformaciones y los destinos tienen entradas. Una entrada de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 La tabla siguiente describe las propiedades de las entradas de componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Descripción|String|Descripción de la entrada.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
|HasSideEffects|Boolean|Indica si un componente puede quitarse del plan de ejecución del flujo de datos cuando no está asociado a un componente de nivel inferior y cuando `RunInOptimizedMode` es `true`.|  
|Id.|Integer|Valor que identifica la entrada de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la entrada.|  
|IsSorted|Boolean|Indica si los datos de la entrada están ordenados.|  
|Nombre|String|Nombre de la entrada.|  
|SourceLocale|Integer|El Id. de configuración regional (LCID) de los datos de entrada.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. . Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
  
 Los destinos y algunas transformaciones no admiten la salida de errores y, además, las propiedades ErrorRowDisposition y TruncationRowDisposition de estos componentes son de solo lectura.  
  
###  <a name="inputcolumns"></a> Propiedades de columna de entrada  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , una entrada contiene una colección de columnas de entrada. Una columna de entrada de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de entrada de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Conjunto de marcas que especifican la comparación de columnas cuyo tipo de datos es carácter. Para más información, consulte [Comparing String Data](data-flow/comparing-string-data.md).|  
|Descripción|String|Describe la columna de entrada.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|El Id. de la columna de metadatos externa asignado a una columna de entrada.|  
|Id.|Integer|Valor que identifica la columna de entrada de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna de entrada.|  
|LineageID|Integer|El Id. de columna para la columna de nivel superior.|  
|Nombre|String|Nombre de la columna de entrada.|  
|SortKeyPosition|Integer|Valor que indica si una columna está ordenada, su criterio de ordenación y la secuencia en la que se ordenan varias columnas. El valor **0** indica que la columna no está ordenada.  Para obtener más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
|UpstreamComponentName|String|Nombre del componente de nivel superior.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Valor que determina la forma en que el componente utiliza una columna de entrada.|  
  
 Las columnas de entrada también tienen las propiedades de tipo de datos descritas en "Propiedades del tipo de datos”.  
  
##  <a name="outputs"></a> Propiedades de salida  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , las transformaciones y los orígenes tienen salidas. Una salida de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 La tabla siguiente describe las propiedades de las salidas de componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|Valor que determina si el motor de flujo de datos elimina la salida cuando ésta se separa de una ruta.|  
|Descripción|String|Describe la salida.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
|ExclusionGroup|Integer|Valor que identifica un grupo de salidas mutuamente excluyentes.|  
|HasSideEffects|Boolean|Valor que indica si un componente puede quitarse del plan de ejecución del flujo de datos cuando no está adjunto con un componente de nivel superior y cuando `RunInOptimizedMode` es `true`.|  
|Id.|Integer|Valor que identifica la salida de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la salida.|  
|IsErrorOut|Boolean|Indica si la salida es una salida de errores.|  
|IsSorted|Boolean|Indica si la salida está ordenada. El valor predeterminado es `False`.<br /><br /> **\*\* Importante \* \***  estableciendo el valor de la `IsSorted` propiedad `True` no se ordenan los datos. Esta propiedad únicamente proporciona una sugerencia a los componentes de nivel inferior acerca de que los datos se han ordenado previamente. Para obtener más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Nombre|String|Nombre de la salida.|  
|SynchronousInputID|Integer|El Id. de una entrada que es sincrónica con la salida.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son `Fail component`, `Ignore failure` y `Redirect row`.|  
  
###  <a name="outputcolumns"></a> Propiedades de columna de salida  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , una salida contiene una colección de columnas de resultados. Una columna de resultados de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de resultados de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Conjunto de marcas que especifican la comparación de columnas cuyo tipo de datos es carácter. Para más información, consulte [Comparing String Data](data-flow/comparing-string-data.md).|  
|Descripción|String|Describe la columna de resultados.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son `Fail component`, `Ignore failure` y `Redirect row`. El valor predeterminado es `Fail component`.|  
|ExternalMetadataColumnID|Integer|El Id. de la columna de metadatos externa asignado a una columna de entrada.|  
|Id.|Integer|Valor que identifica la columna de resultados de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna de resultados.|  
|LineageID|Integer|El Id. de columna para la columna de resultados. Los componentes de nivel inferior hacen referencia a la columna utilizando este valor.|  
|Nombre|String|Nombre de la columna de resultados.|  
|SortKeyPosition|Integer|Valor que indica si una columna está ordenada, su criterio de ordenación y la secuencia en la que se ordenan varias columnas. El valor **0** indica que la columna no está ordenada. Para más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Un valor que contiene las marcas especiales de la columna de resultados.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son `Fail component`, `Ignore failure` y `Redirect row`. El valor predeterminado es `Fail component`.|  
  
 Las columnas de resultados también incluyen un conjunto de propiedades de tipo de datos.  
  
## <a name="external-metadata-column-properties"></a>Propiedades de columna de metadatos externos  
 En el modelo de objetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , las entradas y salidas pueden contener una colección de columnas de metadatos externos. Una columna de metadatos externos de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de metadatos externos de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Descripción|String|Describe la columna externa.|  
|Id.|Integer|Valor que identifica la columna de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna.|  
|Nombre|String|Nombre de la columna de externa.|  
  
 Las columnas de metadatos externos también incluyen un conjunto de propiedades de tipo de datos.  
  
## <a name="data-type-properties"></a>Propiedades del tipo de datos  
 Las columnas de resultados y de metadatos externos incluyen un conjunto de propiedades de tipo de datos. Dependiendo del tipo de datos de la columna, las propiedades pueden ser de lectura y escritura o de solo lectura.  
  
 La tabla siguiente describe las propiedades del tipo de datos de las columnas de resultados y de metadatos externos.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Especifica la página de códigos para cadenas en un formato que no es Unicode.|  
|DataType|Integer (enumeración)|Tipo de datos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de la columna. Para obtener más información, vea [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|Longitud|Integer|Longitud de una columna en caracteres.|  
|Precisión|Integer|Precisión de una columna numérica.|  
|Escala|Integer|Escala de una columna numérica.|  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](data-flow/data-flow.md)   
 [Propiedades personalizadas de transformación](data-flow/transformations/transformation-custom-properties.md)   
 [Propiedades de la ruta de acceso](../../2014/integration-services/path-properties.md)   
 [Propiedades de flujo de datos que se pueden establecer utilizando expresiones](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
