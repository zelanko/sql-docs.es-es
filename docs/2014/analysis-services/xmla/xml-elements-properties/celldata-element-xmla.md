---
title: Elemento CellData (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellData
- http://schemas.microsoft.com/analysisservices/2003/engine#CellData
- urn:schemas-microsoft-com:xml-analysis#CellData
- microsoft.xml.analysis.celldata
helpviewer_keywords:
- CellData element
ms.assetid: 0ebfb5e1-a674-4b9b-bd8c-c529da105f61
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ca9810ece8670c2072674b16e58d996973913a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079875"
---
# <a name="celldata-element-xmla"></a>Elemento CellData (XMLA)
  Contiene una colección de los elementos Cell que representan los datos de celda contenidos por un elemento [root](root-element-xmla.md) que utiliza el tipo de datos [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) .  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Raíz](root-element-xmla.md)|  
|Elementos secundarios|[celda](cell-element-mddataset-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 En el elemento raíz primario, el elemento `Axes` va seguido del elemento `CellData`, una colección de elementos `Cell` que contienen los valores de propiedad para cada celda devuelta en un conjunto de datos multidimensional.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
