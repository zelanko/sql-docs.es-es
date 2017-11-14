---
title: Elemento CellData (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CellData Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CellData
- http://schemas.microsoft.com/analysisservices/2003/engine#CellData
- urn:schemas-microsoft-com:xml-analysis#CellData
- microsoft.xml.analysis.celldata
helpviewer_keywords:
- CellData element
ms.assetid: 0ebfb5e1-a674-4b9b-bd8c-c529da105f61
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a515382d8fc43e29e5f79e19887868a286aee415
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="celldata-element-xmla"></a>Elemento CellData (XMLA)
  Contiene una colección de los elementos Cell que representan los datos de celda contenidos por un elemento [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) que utiliza el tipo de datos [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <CellData>  
      <Cell>...</Cell>  
   </CellData>  
</root>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Elementos secundarios|[Celda](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 En el elemento raíz primario, el elemento **Axes** va seguido del elemento **CellData** , una colección de elementos **Cell** que contienen los valores de propiedad para cada celda devuelta en un conjunto de datos multidimensional.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

