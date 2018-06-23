---
title: Origen de elemento (Measure) (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed41316f62469268d86a89d0c0a5e59f07c8f726
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107496"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Elemento de datos](../data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Medida](../objects/measure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `Source` de la `DataItem`, que actúa como el `Source` de la `Measure`, a su vez puede ser de tipo [RowBinding](../data-type/binding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [MeasureBinding ](../data-type/measurebinding-data-type-assl.md), o [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md).  
  
 Para obtener información adicional acerca de la `DataItem` tipo, incluida una tabla de objetos ASSL y las propiedades de la `DataItem` los tipos, vea [tipo de datos DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 El elemento correspondiente al elemento primario de `Source` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  