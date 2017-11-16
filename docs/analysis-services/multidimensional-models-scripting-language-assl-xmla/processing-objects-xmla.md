---
title: Procesar objetos (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dfc2fafb76d19ea986b697ec065abec738f4c05
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="processing-objects-xmla"></a>Procesar objetos (XMLA)
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el procesamiento es el paso o serie de pasos que permiten convertir datos en información para análisis de negocios. El procesamiento varía en función del tipo de objeto, pero siempre forma parte de la conversión de datos en información.  
  
 Para procesar un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto, puede usar el [proceso](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comando. El **proceso** comando puede procesar los objetos siguientes en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia:  
  
-   Cubos  
  
-   Bases de datos  
  
-   Dimensions  
  
-   Grupos de medida  
  
-   Modelos de minería de datos  
  
-   Estructuras de minería de datos  
  
-   Particiones  
  
 Para controlar el procesamiento de objetos, el **proceso** comando tiene varias propiedades que se pueden establecer. El **proceso** comando tiene propiedades que controlan: se realizará la cantidad de procesamiento, se procesarán los objetos que, si desea utilizar los enlaces fuera de línea, cómo controlar errores y cómo administrar las tablas de reescritura.  
  
## <a name="specifying-processing-options"></a>Especificar opciones de procesamiento  
 El [tipo](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md) propiedad de la **proceso** comando Especifica la opción de procesamiento deben usar al procesar el objeto. Para más información sobre las opciones de procesamiento, vea [Opciones y valores de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 En la tabla siguiente se enumera las constantes para el **tipo** propiedad y los diversos objetos que se pueden procesar con cada una de ellas.  
  
|**Tipo** valor|Objetos aplicables|  
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
  
 Para obtener más información sobre el procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] los objetos, vea [procesar un modelo multidimensional &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Especificar los objetos que se van a procesar  
 El [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propiedad de la **proceso** comando contiene el identificador de objeto del objeto que se procesarán. Se puede especificar sólo un objeto en un **proceso** comando, pero el procesamiento de un objeto también se procesan los objetos secundarios. Por ejemplo, al procesar un grupo de medida de un cubo se procesan todas las particiones de dicho grupo de medida, mientras que al procesar una base de datos se procesan todos los objetos contenidos en ésta (incluidos los cubos, las dimensiones y las estructuras de minería de datos).  
  
 Si establece la **ProcessAffectedObjects** atributo de la **proceso** comando en true, cualquier relacionada también se procesa el objeto afectado por el procesamiento del objeto especificado. Por ejemplo, si una dimensión se actualiza de forma incremental mediante el uso de la *ProcessUpdate* procesamiento opción en el **proceso** de comandos, cualquier partición cuyas agregaciones se invaliden debido a los miembros que se va a Agregar o eliminar también procesa [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si **ProcessAffectedObjects** está establecido en true. En este caso, una sola **proceso** comando puede procesar varios objetos en una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia, pero [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina qué objetos además del objeto único especificado en el **proceso** También se debe procesar el comando.  
  
 Sin embargo, puede procesar varios objetos, como dimensiones, al mismo tiempo mediante el uso de varios **proceso** comandos dentro de un **lote** comando. Operaciones por lotes proporcionan un mayor nivel de control para procesamiento de serie o en paralelo de los objetos en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia que el uso de la **ProcessAffectedObjects** de atributo y permiten optimizar el enfoque del procesamiento de mayor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bases de datos. Para obtener más información acerca de cómo realizar operaciones por lotes, vea [realizar operaciones por lotes &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Especificar enlaces fuera de línea  
 Si el **proceso** comando no está incluido en un **lote** comando, también puede especificar enlaces fuera de línea en el [enlaces](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [delorigendedatos](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), y [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) propiedades de la **proceso** comando para los objetos que se va a procesar. Los enlaces fuera de línea son referencias a orígenes de datos, vistas del origen de datos y otros objetos en el que el enlace existe solamente durante la ejecución de la **proceso** comando y que invalidan los enlaces existentes asociados con la objetos que se procesan. Si no se especifican enlaces fuera de línea, se utilizan los enlaces actualmente asociados a los objetos que se van a procesar.  
  
 Los enlaces fuera de línea se utilizan en las circunstancias siguientes:  
  
-   Procesamiento incremental de una partición, donde debe especificarse una tabla de hechos alternativa o aplicarse un filtro a la tabla de hechos existente para asegurarse de que las filas no se cuentan dos veces.  
  
-   Utilizando una tarea de flujo de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para proporcionar datos al procesar una dimensión, el modelo de minería de datos o la partición.  
  
 Los enlaces fuera de línea se describen como parte de Analysis Services Scripting Language (ASSL). Para obtener más información sobre los enlaces fuera de línea en ASSL, vea [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Actualizar particiones de forma incremental  
 La actualización incremental de una partición ya procesada suele requerir un enlace fuera de línea, ya que el enlace especificado para la partición hace referencia a datos de la tabla de hechos ya agregados en la partición. Al actualizar incrementalmente una partición ya procesada mediante el uso de la **proceso** comando, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realiza las siguientes acciones:  
  
-   Crea una partición temporal con una estructura idéntica a la de la partición que se va a actualizar incrementalmente.  
  
-   Procesa la partición temporal, utilizando el enlace fuera de línea especificado en el **proceso** comando.  
  
-   Mezcla la partición temporal con la partición existente seleccionada.  
  
 Para obtener más información acerca de cómo combinar particiones con XML for Analysis (XMLA), consulte [mezclar particiones &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Controlar los errores de procesamiento  
 El [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) propiedad de la **proceso** comando le permite especificar cómo controlar los errores encontrados al procesar un objeto. Por ejemplo, durante el procesamiento de una dimensión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encuentra un valor duplicado en la columna de clave del atributo clave. Dado que las claves de atributo deben ser únicas, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta los registros duplicados. En función de la [KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md) propiedad de **ErrorConfiguration**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podría:  
  
-   Omitir el error y continuar el procesamiento de la dimensión.  
  
-   Devolver un mensaje que indique que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontró una clave duplicada y continuar el procesamiento.  
  
 Hay muchas condiciones similares para que **ErrorConfiguration** proporciona opciones durante una **proceso** comando.  
  
## <a name="managing-writeback-tables"></a>Administrar tablas de reescritura  
 Si el **proceso** comando encuentra una partición habilitada para escritura, o un cubo o grupo de medida para la partición que no se ha procesado ya están completamente, una tabla de reescritura no puede existir para esa partición. El [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md) propiedad de la **proceso** comando determina si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe crear una tabla de reescritura.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se procesa completamente la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>código  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se procesa de forma incremental el **Internet_Sales_2004** de partición en el **venta por Internet** grupo de medida de la **Adventure Works DW** cubo en el [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ejemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. El **proceso** comando es agregar agregaciones para el orden de fechas a más tardar el 31 de diciembre de 2006 a la partición mediante un enlace de consultas fuera de línea en el **enlaces** propiedad de la **proceso**  comandos para recuperar las filas de la tabla de hechos desde el que se va a generar las agregaciones para agregar a la partición.  
  
### <a name="code"></a>código  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
  

