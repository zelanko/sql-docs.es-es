---
title: Tipo de elemento (Dimension) (ASSL) | Microsoft Docs
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
- Type Element (Dimension)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6afa3b273200630a4d36e0c4df679c58efb6bd5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283951"
---
# <a name="type-element-dimension-assl"></a>Elemento Type (Dimension) (ASSL)
  Proporciona información acerca del contenido de la dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Regular*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimension](../objects/dimension-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Algunos valores para `Type`, por ejemplo *cuentas*, determinan el comportamiento concreto.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Regular*|La dimensión es una dimensión normal.|  
|*Time*|La dimensión es una dimensión de tiempo. **Nota:** este valor indica que la dimensión admite la funcionalidad específica de las dimensiones de tiempo.|  
|*Geography*|La dimensión contiene atributos geográficos.|  
|*Organización*|La dimensión contiene atributos de organización.|  
|*BillOfMaterials*|La dimensión contiene atributos de lista de materiales.|  
|*Cuentas*|La dimensión contiene los atributos relacionados con cuentas. **Nota:** este valor indica que la dimensión admite la funcionalidad específica de las dimensiones de cuenta.|  
|*Clientes*|La dimensión contiene los atributos relacionados con clientes.|  
|*Productos*|La dimensión contiene los atributos relacionados con productos.|  
|*Escenario*|La dimensión contiene los atributos relacionados con escenarios.|  
|*Cuantitativa*|La dimensión contiene los atributos cuantitativos.|  
|*Utilidad*|La dimensión contiene los atributos de utilidad.|  
|*Moneda*|La dimensión contiene los atributos de moneda.|  
|*Tarifas*|La dimensión contiene los atributos de tasa de cambio.|  
|*Canal*|La dimensión contiene los atributos de canal.|  
|*Promoción*|La dimensión contiene los atributos relacionados con la promoción.|  
  
 La enumeración que corresponde a los valores permitidos para `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionType>.  
  
 El elemento que se corresponde con el elemento primario de `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
