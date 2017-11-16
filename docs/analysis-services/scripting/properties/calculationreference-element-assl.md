---
title: Elemento CalculationReference (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CalculationReference Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CalculationReference
helpviewer_keywords:
- CalculationReference element
ms.assetid: 4dd18b1f-55c3-4673-afbe-736d1bce8331
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18df3c7f00efc4173b5651c2f2fb7528419278c3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="calculationreference-element-assl"></a>Elemento CalculationReference (ASSL)
  Contiene el nombre del conjunto con nombre o de celda calculada al que hace referencia el [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty>  
   ...  
   <CalculationReference>...</CalculationReference>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si el valor de la **CalculationReference** no coincide con el nombre de un objeto con nombre se establece o se calcula una definición, de celda la **CalculationReference** se omite.  
  
 El elemento que corresponde al elemento primario de **CalculationReference** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Calculationproperties, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

