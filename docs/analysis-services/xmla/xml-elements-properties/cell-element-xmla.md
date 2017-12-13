---
title: Celda elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cell Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords: Cell element
ms.assetid: 88daba54-89e9-423f-8d12-8de80cf52d6b
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 22331e6f94fdfcbfbac9a480831dd40e6ff89868
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="cell-element-xmla"></a>Elemento Cell (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene información sobre una celda que se va a actualizar una [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<UpdateCells>  
   ...  
   <Cell CellOrdinal="Long">  
      <Value>...</Value>  
   </Cell>  
   ...  
</UpdateCells>  
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
|Elementos primarios|[UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Elementos secundarios|[Valor](../../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|CellOrdinal|Atributo **Long** requerido. Contiene la posición ordinal basada en cero de la celda que se va a actualizar.|  
  
## <a name="remarks"></a>Comentarios  
 Para más información sobre la actualización de celdas, vea [Actualizar celdas &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
