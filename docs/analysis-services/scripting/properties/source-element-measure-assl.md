---
title: Origen de elemento (Measure) (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Source Element (Measure)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 9bae7ba4-3065-4623-b3e0-d54cebea7503
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 14911562374b97fbc41ded8cb8932f80ce08adcc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="source-element-measure-assl"></a>Elemento Source (Measure) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene los detalles de la fuente que contiene el valor de la [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **origen** de la **DataItem**, que actúa como el **origen** de la **medida**, a su vez puede ser de tipo [RowBinding ](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), o [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md).  
  
 Para obtener información adicional acerca de la **DataItem** tipo, incluida una tabla de objetos ASSL y las propiedades de la **DataItem** los tipos, vea [tipo de datos DataItem &#40;ASSL&#41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 El elemento correspondiente al elemento primario de **origen** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
