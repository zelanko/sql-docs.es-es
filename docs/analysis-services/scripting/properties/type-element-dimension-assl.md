---
title: Tipo de elemento (Dimension) (ASSL) | Documentos de Microsoft
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
- Type Element (Dimension)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 075ebc645c67f496d7e6946035371244dd229c88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="type-element-dimension-assl"></a>Elemento Type (Dimension) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Proporciona información acerca del contenido de la dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Regular*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Algunos valores para **Type**, por ejemplo *Accounts*, determinan el comportamiento concreto.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|La dimensión es una dimensión normal.|  
|*Time*|La dimensión es una dimensión de tiempo.<br /><br /> Nota: Este valor indica que la dimensión admite la funcionalidad específica de las dimensiones de tiempo.|  
|*Geografía*|La dimensión contiene atributos geográficos.|  
|*Organización*|La dimensión contiene atributos de organización.|  
|*Lista de materiales*|La dimensión contiene atributos de lista de materiales.|  
|*Cuentas*|La dimensión contiene los atributos relacionados con cuentas.<br /><br /> Nota: Este valor indica que la dimensión admite la funcionalidad específica de las dimensiones de cuenta.|  
|*Clientes*|La dimensión contiene los atributos relacionados con clientes.|  
|*Productos*|La dimensión contiene los atributos relacionados con productos.|  
|*Escenario*|La dimensión contiene los atributos relacionados con escenarios.|  
|*Cuantitativo*|La dimensión contiene los atributos cuantitativos.|  
|*Utilidad*|La dimensión contiene los atributos de utilidad.|  
|*Moneda*|La dimensión contiene los atributos de moneda.|  
|*Tasas*|La dimensión contiene los atributos de tasa de cambio.|  
|*Canal*|La dimensión contiene los atributos de canal.|  
|*Promoción*|La dimensión contiene los atributos relacionados con la promoción.|  
  
 La enumeración que corresponde a los valores permitidos para **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionType>.  
  
 El elemento que corresponde al elemento primario de **tipo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Dimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
