---
title: Mezclar particiones (XMLA) | Documentos de Microsoft
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 90d92549184a5dc3a93123a86870d3905f38791a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="merging-partitions-xmla"></a>Mezclar particiones (XMLA)
  Si las particiones tienen el mismo diseño de agregaciones y la estructura, puede combinar la partición mediante la [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) comando de XML for Analysis (XMLA). Combinar particiones es una acción importante que se debe realizar cuando se administran particiones, sobre todo aquellas particiones que contienen datos históricos con particiones por fecha.  
  
 Por ejemplo, un cubo financiero puede usar dos particiones:  
  
-   Una partición representa los datos financieros del año en curso, usando la configuración de almacenamiento de OLAP relacional (ROLAP) en tiempo real para el rendimiento.  
  
-   Otra partición contiene los datos financieros de años anteriores, usando la configuración de almacenamiento de OLAP multidimensional (MOLAP) para el almacenamiento.  
  
 Ambas particiones usan valores de almacenamiento diferentes, pero utilizan el mismo diseño de agregaciones. En lugar de procesar el cubo a través de años de datos históricos al final del año, puede utilizar el **MergePartitions** comando para mezclar la partición para el año actual con la partición de años anteriores. Con ello se conservan los datos de agregación sin tener que realizar un proceso completo del cubo que puede requerir mucho tiempo.  
  
## <a name="specifying-partitions-to-merge"></a>Especificar particiones para combinar  
 Cuando el **MergePartitions** comando se ejecuta, los datos de agregación almacenados en las particiones de origen especificadas en el [origen](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) propiedad se agrega a la partición de destino especificada en el [destino ](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md) propiedad.  
  
> [!NOTE]  
>  El **origen** propiedad puede contener más de una referencia de objeto de partición. Sin embargo, el **destino** propiedad no se puede.  
  
 Que se combinarán correctamente, las particiones especificadas tanto en el **origen** y **destino** debe estar incluido en el mismo grupo de medida y usar el mismo diseño de agregaciones. De lo contrario, se produce un error.  
  
 Las particiones especificadas en el **origen** se eliminan después de la **MergePartitions** comando se ha completado correctamente.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se combina todas las particiones en el **Customer Counts** grupo de medida de la **Adventure Works** de cubo en el **Adventure Works DW** ejemplo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la base de datos la **Customers_2004** partición.  
  
### <a name="code"></a>código  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>Vea también  
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
