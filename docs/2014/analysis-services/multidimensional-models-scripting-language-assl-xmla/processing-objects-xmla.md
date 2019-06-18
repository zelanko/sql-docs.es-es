---
title: Procesamiento de objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab38ea9b58e891d813a3ca73f43d20a364275da0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727601"
---
# <a name="processing-objects-xmla"></a>Procesar objetos (XMLA)
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], procesar es el paso o serie de pasos que permiten convertir datos en información para análisis de negocios. El procesamiento varía en función del tipo de objeto, pero siempre forma parte de la conversión de datos en información.  
  
 Para procesar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto, puede usar el [proceso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comando. El comando `Process` puede procesar los siguientes objetos en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   Cubos  
  
-   Bases de datos  
  
-   Dimensions  
  
-   Grupos de medida  
  
-   Modelos de minería de datos  
  
-   Estructuras de minería de datos  
  
-   Particiones  
  
 Para controlar el procesamiento de los objetos, pueden establecerse diversas propiedades del comando `Process`. El comando `Process` tiene propiedades para controlar: qué cantidad de procesamiento se va a realizar, qué objetos se van a procesar, si se van a utilizar o no enlaces fuera de línea, cómo controlar los errores y cómo administrar las tablas de reescritura.  
  
## <a name="specifying-processing-options"></a>Especificar opciones de procesamiento  
 El [tipo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) propiedad de la `Process` comando Especifica la opción de procesamiento deben usar al procesar el objeto. Para más información sobre las opciones de procesamiento, vea [Opciones y valores de procesamiento &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 En la tabla siguiente se enumeran las constantes para la propiedad `Type` y los diversos objetos que se pueden procesar con cada una de las constantes.  
  
|Valor `Type`|Objetos aplicables|  
|--------------------|------------------------|  
|*ProcessFull*|Cubo, base de datos, dimensión, grupo de medida, modelo de minería de datos, estructura de minería de datos, partición|  
|*ProcessAdd*|Dimensión, partición|  
|*ProcessUpdate*|Dimensión|  
|*ProcessIndexes*|Dimensión, cubo, grupo de medida, partición|  
|*ProcessData*|Dimensión, cubo, grupo de medida, partición|  
|*ProcessDefault*|Cubo, base de datos, dimensión, grupo de medida, modelo de minería de datos, estructura de minería de datos, partición|  
|*ProcessClear*|Cubo, base de datos, dimensión, grupo de medida, modelo de minería de datos, estructura de minería de datos, partición|  
|*ProcessStructure*|Cubo, estructura de minería de datos|  
|*ProcessClearStructureOnly*|Estructura de minería de datos|  
|*ProcessScriptCache*|Cube|  
  
 Para obtener más información sobre el procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos, vea [procesamiento del objeto de modelo Multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Especificar los objetos que se van a procesar  
 El [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propiedad de la `Process` comando contiene el identificador de objeto del objeto que se va a procesar. En un comando `Process` solamente puede especificarse un objeto, si bien al procesar un objeto también se procesan sus objetos secundarios. Por ejemplo, al procesar un grupo de medida de un cubo se procesan todas las particiones de dicho grupo de medida, mientras que al procesar una base de datos se procesan todos los objetos contenidos en ésta (incluidos los cubos, las dimensiones y las estructuras de minería de datos).  
  
 Si establece el atributo `ProcessAffectedObjects` del comando `Process` en true, también se procesa cualquier objeto relacionado afectado por el procesamiento del objeto especificado. Por ejemplo, si una dimensión se actualiza de forma incremental mediante el uso de la *ProcessUpdate* procesamiento opción en el `Process` de comandos, cualquier partición cuyas agregaciones se invaliden debido a los miembros que se agreguen o eliminen también es procesó [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si `ProcessAffectedObjects` está establecido en true. En este caso, un único comando `Process` puede procesar varios objetos de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], si bien [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina qué objetos deberán procesarse además del objeto único especificado en el comando `Process`.  
  
 No obstante, puede procesar diversos objetos (como dimensiones) al mismo tiempo si utiliza varios comandos `Process` dentro de un comando `Batch`. Las operaciones por lotes proporcionan un control más preciso para el procesamiento en serie o en paralelo de los objetos de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que el uso del atributo `ProcessAffectedObjects`; además, permiten optimizar el enfoque del procesamiento para bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de mayor tamaño. Para obtener más información acerca de cómo realizar operaciones por lotes, vea [realizar operaciones por lotes &#40;XMLA&#41;](performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Especificar enlaces fuera de línea  
 Si el `Process` comando no está incluido en un `Batch` comando, también puede especificar enlaces fuera de línea en el [enlaces](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla), [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla), y [DataSourceView ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) propiedades de la `Process` el comando para los objetos que se va a procesarse. Los enlaces fuera de línea son referencias a orígenes de datos, vistas del origen de datos y otros objetos en los que el enlace existe solamente durante la ejecución del comando `Process` y que invalidan cualquier enlace existente asociado a los objetos que se procesan. Si no se especifican enlaces fuera de línea, se utilizan los enlaces actualmente asociados a los objetos que se van a procesar.  
  
 Los enlaces fuera de línea se utilizan en las circunstancias siguientes:  
  
-   Procesamiento incremental de una partición, donde debe especificarse una tabla de hechos alternativa o aplicarse un filtro a la tabla de hechos existente para asegurarse de que las filas no se cuentan dos veces.  
  
-   Uso de una tarea de flujo de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para proporcionar datos al procesar una dimensión, el modelo de minería de datos o la partición.  
  
 Los enlaces fuera de línea se describen como parte de Analysis Services Scripting Language (ASSL). Para obtener más información sobre los enlaces fuera de línea en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Actualizar particiones de forma incremental  
 La actualización incremental de una partición ya procesada suele requerir un enlace fuera de línea, ya que el enlace especificado para la partición hace referencia a datos de la tabla de hechos ya agregados en la partición. Al actualizar incrementalmente una partición ya procesada mediante el comando `Process`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realiza las siguientes acciones:  
  
-   Crea una partición temporal con una estructura idéntica a la de la partición que se va a actualizar incrementalmente.  
  
-   Procesa la partición temporal, utilizando el enlace fuera de línea especificado en el comando `Process`.  
  
-   Mezcla la partición temporal con la partición existente seleccionada.  
  
 Para obtener más información acerca de cómo combinar particiones con XML for Analysis (XMLA), consulte [mezclar particiones &#40;XMLA&#41;](merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Controlar los errores de procesamiento  
 El [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) propiedad de la `Process` comando le permite especificar cómo controlar los errores detectados al procesar un objeto. Por ejemplo, durante el procesamiento de una dimensión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encuentra un valor duplicado en la columna de clave del atributo clave. Dado que las claves de atributo deben ser únicas, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta los registros duplicados. Según el [KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl) propiedad de `ErrorConfiguration`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podría:  
  
-   Omitir el error y continuar el procesamiento de la dimensión.  
  
-   Devolver un mensaje que indique que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontró una clave duplicada y continuar el procesamiento.  
  
 Hay muchas condiciones similares para las que `ErrorConfiguration` proporciona opciones durante la ejecución de un comando `Process`.  
  
## <a name="managing-writeback-tables"></a>Administrar tablas de reescritura  
 Si el comando `Process` encuentra una partición habilitada para escritura (o un cubo o grupo de medida para este tipo de partición) que aún no se haya procesado por completo, puede que aún no exista una tabla de reescritura para esa partición. El [WritebackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla) propiedad de la `Process` comando determina si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe crear una tabla de reescritura.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
 En el ejemplo siguiente se procesa completamente la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>Código  
  
```  
<Process xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Descripción  
 El ejemplo siguiente se procesa de forma incremental el **Internet_Sales_2004** de partición en la **Internet Sales** grupo de medida de la **Adventure Works DW** cubo en el [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ejemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. El `Process` comando es agregar agregaciones para el orden de fechas posterior al 31 de diciembre de 2006 a la partición mediante el uso de un enlace de consultas fuera de línea de la `Bindings` propiedad de la `Process` comando para recuperar las filas de tabla de hechos desde el que se va a generar agregaciones para agregar a la partición.  
  
### <a name="code"></a>Código  
  
```  
<Process ProcessAffectedObjects="true" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
