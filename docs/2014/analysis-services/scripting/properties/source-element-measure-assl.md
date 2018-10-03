---
title: (Medida) (ASSL) del elemento de origen | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element (Measure)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 933851f354f14e325608c954ce77ba5f3d034a10
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117331"
---
# <a name="source-element-measure-assl"></a>Elemento Source (Measure) (ASSL)
  Contiene los detalles de la fuente que contiene el valor de la [medida](../objects/measure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Measure>  
      ...  
   <Source xsi:type="DataItem">...</Source>  
      ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Medida](../objects/measure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El `Source` de la `DataItem`, que actúa como el `Source` de la `Measure`, a su vez puede ser de tipo [RowBinding](../data-type/binding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [MeasureBinding ](../data-type/measurebinding-data-type-assl.md), o [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md).  
  
 Para obtener más información sobre la `DataItem` tipo, incluida una tabla de objetos ASSL y propiedades de la `DataItem` , vea [tipo de datos DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 El elemento correspondiente al elemento primario de `Source` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
