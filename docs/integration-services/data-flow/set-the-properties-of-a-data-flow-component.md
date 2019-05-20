---
title: Establecer las propiedades de un componente de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e2dcaff5b7b8ad834eb12277c587b222b8f782d4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726380"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Establecer las propiedades de un componente de flujo de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para establecer las propiedades de los componentes de flujo de datos, que incluyen orígenes, destinos y transformaciones, utilice una de las características siguientes:  
  
-   Los editores de componentes que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona. Estos editores incluyen solo las propiedades personalizadas de cada componente de flujo de datos.  
  
-   La ventana **Propiedades** enumera las propiedades personalizadas de nivel de componente de cada elemento, al igual que las propiedades que son comunes a todos los elementos de flujo de datos.  
  
-   El cuadro de diálogo **Editor avanzado** proporciona acceso a las propiedades personalizadas de cada componente. El cuadro de diálogo **Editor avanzado** también permite acceder a las propiedades comunes de todos los componentes de flujo de datos (propiedades de entradas, salidas, salidas de error, columnas y columnas externas).  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>Establecer las propiedades de un componente de flujo de datos con un editor de componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el flujo de datos con el componente cuyas propiedades quiere ver y modificar.  
  
4.  Haga doble clic en el componente de flujo de datos.  
  
5.  En el editor de componentes, vea o modifique los valores de las propiedades y luego cierre el editor.  
  
6.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>Establecer las propiedades de un componente de flujo de datos en la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el componente cuyas propiedades quiere ver y modificar.  
  
4.  Haga clic con el botón derecho en el componente de flujo de datos y luego haga clic en **Propiedades**.  
  
5.  Vea o modifique los valores de la propiedad y luego cierre la ventana **Propiedades** .  
  
    > [!NOTE]  
    >  Muchas propiedades son de solo lectura y no pueden modificarse.  
  
6.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>Establecer las propiedades de un componente de flujo de datos con el Editor avanzado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el componente que quiere ver o modificar.  
  
4.  En el diseñador de flujos de datos, haga clic con el botón derecho en el componente de flujo de datos y luego haga clic en **Mostrar editor avanzado**.  
  
    > [!NOTE]  
    >  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los componentes de flujo de datos que admiten varias entradas no pueden usar el **Editor avanzado**.  
  
5.  En el cuadro de diálogo **Editor avanzado** , realice cualquiera de los pasos siguientes:  
  
    -   Para ver y especificar la conexión que el componente utiliza, haga clic en la pestaña **Administradores de conexiones** .  
  
        > [!NOTE]  
        >  La pestaña **Administradores de conexiones** está disponible solamente para los componentes de flujo de datos que usan administradores de conexiones para conectarse a orígenes de datos como archivos y bases de datos  
  
    -   Para ver y modificar propiedades de nivel de componente, haga clic en la pestaña **Propiedades de componente** .  
  
    -   Para ver y modificar asignaciones entre columnas externas y la salida disponible, haga clic en la pestaña **Asignaciones de columnas** .  
  
        > [!NOTE]  
        >  La pestaña **Asignaciones de columnas** solo está disponible al ver o editar orígenes o destinos.  
  
    -   Para ver una lista de las columnas de entrada disponibles y para actualizar los nombres de las columnas de salida, haga clic en la pestaña **Columnas de entrada** .  
  
        > [!NOTE]  
        >  La pestaña Columnas de entrada está disponible solamente cuando se trabaja con transformaciones o destinos. Para más información, consulte [Integration Services Transformations](../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
    -   Para ver y modificar las propiedades de las entradas, salidas y salidas de errores, y las propiedades de las columnas que contienen, haga clic en la pestaña **Propiedades de entrada y salida** .  
  
        > [!NOTE]  
        >  Los orígenes no tienen entradas. Los destinos no tienen salidas, excepto una salida de errores opcional.  
  
6.  Vea o modifique los valores de propiedades.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  

## <a name="common-properties-of-data-flow-components"></a>Propiedades comunes de los componentes de flujo de datos
Los objetos de flujo de datos en el modelo de objetos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tienen propiedades comunes y propiedades personalizadas en el nivel del componente, de las entradas y salidas, y de las columnas de entrada y de salida. Muchas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
 En este tema se enumeran y describen las propiedades comunes de los objetos de flujo de datos.  
  
-   [Components](#components)  
  
-   [Entradas](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [Salidas](#outputs)  
  
-   [Columnas de salida](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 La tabla siguiente describe las propiedades de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
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
|ValidateExternalMetadata|Boolean|Indica si se validan los metadatos de columnas externas. El valor predeterminado de esta propiedad es **True**.|  
|Versión|Integer|Versión de un componente.|  
  
###  <a name="inputs"></a> Propiedades de entradas  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , las transformaciones y los destinos tienen entradas. Una entrada de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 La tabla siguiente describe las propiedades de las entradas de componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Descripción|String|Descripción de la entrada.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
|HasSideEffects|Boolean|Indica si un componente se puede quitar del plan de ejecución del flujo de datos cuando no está adjunto a un componente de nivel inferior y cuando **RunInOptimizedMode** es **true**.|  
|Id.|Integer|Valor que identifica la entrada de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la entrada.|  
|IsSorted|Boolean|Indica si los datos de la entrada están ordenados.|  
|Nombre|String|Nombre de la entrada.|  
|SourceLocale|Integer|El Id. de configuración regional (LCID) de los datos de entrada.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. . Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
  
 Los destinos y algunas transformaciones no admiten la salida de errores y, además, las propiedades ErrorRowDisposition y TruncationRowDisposition de estos componentes son de solo lectura.  
  
###  <a name="inputcolumns"></a> Propiedades de las columnas de entrada  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , una entrada contiene una colección de columnas de entrada. Una columna de entrada de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de entrada de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Conjunto de marcas que especifican la comparación de columnas cuyo tipo de datos es carácter. Para más información, consulte [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descripción|String|Describe la columna de entrada.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|El Id. de la columna de metadatos externa asignado a una columna de entrada.|  
|Id.|Integer|Valor que identifica la columna de entrada de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna de entrada.|  
|LineageID|Integer|El Id. de columna para la columna de nivel superior.|  
|LineageIdentificationString|String|La cadena de identificación que incluye el nombre de la columna de nivel superior.|  
|Nombre|String|Nombre de la columna de entrada.|  
|SortKeyPosition|Integer|Valor que indica si una columna está ordenada, su criterio de ordenación y la secuencia en la que se ordenan varias columnas. El valor **0** indica que la columna no está ordenada.  Para obtener más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
|UpstreamComponentName|String|Nombre del componente de nivel superior.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Valor que determina la forma en que el componente utiliza una columna de entrada.|  
  
 Las columnas de entrada también tienen las propiedades de tipo de datos descritas en "Propiedades del tipo de datos”.  
  
###  <a name="outputs"></a> Propiedades de salidas  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , las transformaciones y los orígenes tienen salidas. Una salida de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 La tabla siguiente describe las propiedades de las salidas de componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|Valor que determina si el motor de flujo de datos elimina la salida cuando ésta se separa de una ruta.|  
|Descripción|String|Describe la salida.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
|ExclusionGroup|Integer|Valor que identifica un grupo de salidas mutuamente excluyentes.|  
|HasSideEffects|Boolean|Valor que indica si un componente puede quitarse del plan de ejecución del flujo de datos cuando no está adjunto con un componente de nivel superior y cuando **RunInOptimizedMode** es **true**.|  
|Id.|Integer|Valor que identifica la salida de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la salida.|  
|IsErrorOut|Boolean|Indica si la salida es una salida de errores.|  
|IsSorted|Boolean|Indica si la salida está ordenada. El valor predeterminado es **False**.<br /><br /> **\*\* Importante \*\*** Aunque se establezca el valor de la propiedad **IsSorted** en **True**, los datos no se ordenan. Esta propiedad únicamente proporciona una sugerencia a los componentes de nivel inferior acerca de que los datos se han ordenado previamente. Para obtener más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Nombre|String|Nombre de la salida.|  
|SynchronousInputID|Integer|El Id. de una entrada que es sincrónica con la salida.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son **Fail component**, **Ignore failure**y **Redirect row**.|  
  
###  <a name="outputcolumns"></a> Propiedades de las columnas de salida  
 En el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , una salida contiene una colección de columnas de resultados. Una columna de resultados de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de resultados de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Conjunto de marcas que especifican la comparación de columnas cuyo tipo de datos es carácter. Para más información, consulte [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descripción|String|Describe la columna de resultados.|  
|ErrorOrTruncationOperation|String|Cadena opcional que especifica los tipos de errores o truncamientos que pueden producirse al procesar una fila.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica el control de errores. Los valores son **Fail component**, **Ignore failure**y **Redirect row**. El valor predeterminado es **Error de componente**.|  
|ExternalMetadataColumnID|Integer|El Id. de la columna de metadatos externa asignado a una columna de entrada.|  
|Id.|Integer|Valor que identifica la columna de resultados de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna de resultados.|  
|LineageID|Integer|El Id. de columna para la columna de resultados. Los componentes de nivel inferior hacen referencia a la columna utilizando este valor.|  
|LineageIdentificationString|String|La cadena de identificación que incluye el nombre de la columna.|  
|Nombre|String|Nombre de la columna de resultados.|  
|SortKeyPosition|Integer|Valor que indica si una columna está ordenada, su criterio de ordenación y la secuencia en la que se ordenan varias columnas. El valor **0** indica que la columna no está ordenada. Para más información, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Un valor que contiene las marcas especiales de la columna de resultados.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina la forma en que el componente administra los truncamientos producidos al procesar las filas. Los valores son **Fail component**, **Ignore failure**y **Redirect row**. El valor predeterminado es **Error de componente**.|  
  
 Las columnas de resultados también incluyen un conjunto de propiedades de tipo de datos.  
  
### <a name="external-metadata-column-properties"></a>Propiedades de las columnas de metadatos externos  
 En el modelo de objetos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , las entradas y salidas pueden contener una colección de columnas de metadatos externos. Una columna de metadatos externos de un componente en el flujo de datos implementa la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 La tabla siguiente describe las propiedades de las columnas de metadatos externos de los componentes en un flujo de datos. Algunas propiedades tienen valores de solo lectura que son asignados en tiempo de ejecución por el motor de flujo de datos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|Descripción|String|Describe la columna externa.|  
|Id.|Integer|Valor que identifica la columna de forma inequívoca.|  
|IdentificationString|String|Cadena que identifica la columna.|  
|Nombre|String|Nombre de la columna de externa.|  
  
 Las columnas de metadatos externos también incluyen un conjunto de propiedades de tipo de datos.  
  
### <a name="data-type-properties"></a>Propiedades de tipos de datos  
 Las columnas de resultados y de metadatos externos incluyen un conjunto de propiedades de tipo de datos. Dependiendo del tipo de datos de la columna, las propiedades pueden ser de lectura y escritura o de solo lectura.  
  
 La tabla siguiente describe las propiedades del tipo de datos de las columnas de resultados y de metadatos externos.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Especifica la página de códigos para cadenas en un formato que no es Unicode.|  
|DataType|Integer (enumeración)|Tipo de datos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de la columna. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|Longitud|Integer|Longitud de una columna en caracteres.|  
|Precisión|Integer|Precisión de una columna numérica.|  
|Escala|Integer|Escala de una columna numérica.|  

## <a name="custom-properties-of-data-flow-components"></a>Propiedades personalizadas de los componentes de flujo de datos
Para obtener información acerca de propiedades personalizadas, vea los siguientes temas.  
  
-   [Propiedades personalizadas de ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [Propiedades personalizadas de la tarea Control CDC](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [Propiedades personalizadas del origen de CDC](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de procesamiento de dimensiones](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Propiedades personalizadas de Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [Propiedades personalizadas de archivo plano](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [Propiedades personalizadas de los destinos de ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del origen ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)Propiedades personalizadas de OLE DB  
  
-   [Propiedades personalizadas del destino de procesamiento de particiones](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Propiedades personalizadas de archivo sin formato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de conjunto de registros](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Propiedades personalizadas del destino de SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [Propiedades personalizadas de transformación](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [Propiedades personalizadas del origen XML](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>Utilizar una expresión en un componente de flujo de datos
Este procedimiento describe cómo agregar una expresión a la transformación División condicional o a la transformación Columna derivada. La transformación División condicional utiliza expresiones para definir las condiciones que dirigen las filas de datos a una salida de transformación y la transformación Columna derivada utiliza expresiones para definir los valores asignados a las columnas.  
  
 Para implementar una expresión en una transformación, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen. 
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** y, a continuación, en la tarea Flujo de datos que contiene el flujo de datos en el que desea implementar la expresión.  
  
4.  Haga clic en la pestaña **Flujo de datos** y arrastre una transformación División condicional o Columna derivada del **Cuadro de herramientas** a la superficie de diseño.  
  
5.  Arrastre el conector verde desde el origen o desde una transformación a la transformación División condicional o Columna derivada.  
  
6.  Haga doble clic en la transformación para abrir el cuadro de diálogo correspondiente.  
  
7.  En el panel de la izquierda, expanda **Variables** para ver las variables del sistema y las definidas por el usuario, y expanda **Columnas** para ver las columnas de entrada de la transformación.  
  
8.  En el panel de la derecha, expanda **Funciones matemáticas**, **Funciones de cadena**, **Funciones de fecha y hora**, **Funciones NULL**, **Conversiones de tipo**y **Operadores** para tener acceso a las funciones, las conversiones y los operadores que proporciona la gramática de expresiones.  
  
9. Dependiendo de la transformación, siga uno de estos procedimientos para crear una expresión:  
  
    -   En el cuadro de diálogo **Editor de transformación División condicional** , arrastre las variables, columnas, funciones, operadores y conversiones a la columna **Condición** . O bien, puede escribir una expresión directamente en la columna **Condición** .  
  
    -   En el cuadro de diálogo **Editor de transformación Columna derivada** , arrastre las variables, columnas, funciones, operadores y conversiones a la columna **Expresión** . O bien, puede escribir una expresión directamente en la columna **Expresión** .  
  
        > [!NOTE]  
        >  Al quitar el foco de la columna **Condición** o **Expresión** , el texto de la expresión podría resaltarse para indicar que la sintaxis de la expresión es incorrecta.  
  
10. Haga clic en **Aceptar** para salir del cuadro de diálogo.  
  
    > [!NOTE]  
    >  Si la expresión no es válida, aparece una alerta que describe los errores de sintaxis de la expresión.  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>Propiedades del flujo de datos que se pueden establecer con una expresión
Los valores de ciertas propiedades de objetos de flujo de datos se pueden especificar utilizando expresiones de propiedades disponibles en el contenedor de tareas Flujo de Datos.  
  
 Para obtener información sobre el uso de expresiones de propiedades, vea [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Puede utilizar las expresiones de propiedades para personalizar las configuraciones de cada instancia implementada de un paquete. También puede usar expresiones de propiedades para especificar restricciones en tiempo de ejecución para un paquete mediante la opción **/set** con la utilidad de símbolo del sistema **dtexec** . Por ejemplo, puede restringir el **MaximumThreads** utilizado por la transformación Ordenación o bien el **MaxMemoryUsage** de las transformaciones Fuzzy Grouping y Fuzzy Lookup. Si no presentan restricciones, estas transformaciones pueden almacenar en memoria caché grandes cantidades de datos en memoria.  
  
 Para especificar una expresión de propiedades para una de las propiedades de los objetos de flujo de datos mencionados en este tema, muestre la ventana **Propiedades** para la tarea Flujo de Datos seleccionando la tarea Flujo de Datos en la superficie **Flujo de control** del diseñador o seleccionando la pestaña **Flujo de datos** del diseñador sin seleccionar ningún componente o ruta de acceso individual. Seleccione la propiedad **Expresiones** y haga clic en los puntos suspensivos (…) para mostrar el cuadro de diálogo **Editor de expresiones de propiedad** . Despliegue la lista **Propiedad** para seleccionar una propiedad y, después, escriba una expresión en el cuadro de texto **Expresión** o haga clic en los puntos suspensivos (…) para mostrar el cuadro de diálogo **Generador de expresiones** .  
  
 La lista **Propiedad** muestra las propiedades disponibles solo para aquellos objetos de flujo de datos que ya haya colocado en la superficie **Flujo de datos** del diseñador. Por consiguiente, no puede utilizar la lista **Propiedad** para ver todas las posibles propiedades de los objetos de flujo de datos que admiten expresiones de propiedades. Por ejemplo, si ha colocado un origen ADO NET en la superficie del diseñador, la lista **Propiedad** contiene una entrada para la propiedad **[ADO NET Source].[SqlCommand]** . La lista también muestra muchas propiedades de la propia tarea Flujo de Datos.  
 
 Los valores de las propiedades de la siguiente lista se pueden especificar mediante expresiones de propiedades.  
  
### <a name="data-flow-sources"></a>Orígenes de flujos de datos  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|Origen ADO NET|Propiedad TableOrViewName<br /><br /> Propiedad SQLCommand|  
|Origen XML|Propiedad XMLData<br /><br /> Propiedad XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Transformaciones de flujos de datos  
 Para obtener más información acerca de estas propiedades personalizadas, vea [Transformation Custom Properties](../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|División condicional, transformación|Propiedad FriendlyExpression|  
|Transformación Columna derivada|Propiedad FriendlyExpression|  
|Agrupación aproximada, transformación|Propiedad MaxMemoryUsage|  
|Búsqueda aproximada, transformación|Propiedad MaxMemoryUsage|  
|Transformación de búsqueda|Propiedad SQLCommand<br /><br /> Propiedad SqlCommandParam|  
|transformación Comando de OLE DB|Propiedad SQLCommand|  
|Muestreo de porcentaje, transformación|Propiedad SamplingValue|  
|Dinámica, transformación|Propiedad PivotKeyValue|  
|Muestreo de fila, transformación|Propiedad SamplingValue|  
|Ordenar, transformación|Propiedad MaximumThreads|  
|Anulación de dinamización, transformación|Propiedad PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinos de flujos de datos  
  
|Objeto Flujo de datos|Propiedad|  
|----------------------|--------------|  
|Destino ADO NET|Propiedad TableOrViewName<br /><br /> Propiedad BatchSize<br /><br /> Propiedad CommandTimeOut|  
|Destino de archivo plano|Propiedad Header|  
|Destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact|Propiedad TableName|  
|Destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Propiedad BulkInsertTableName<br /><br /> Propiedad BulkInsertFirstRow<br /><br /> Propiedad BulkInsertLastRow<br /><br /> Propiedad BulkInsertOrder<br /><br /> Propiedad Tiempo de espera|  

