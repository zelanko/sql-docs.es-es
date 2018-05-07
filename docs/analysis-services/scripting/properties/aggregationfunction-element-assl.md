---
title: Elemento AggregationFunction (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AggregationFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c7c9aedc12abbeb5ab805e0d85cfe1421857749b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationfunction-element-assl"></a>Elemento AggregationFunction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la función de agregación que se usará para el tipo de cuenta.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Sum*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cuenta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Value|Description|  
|-----------|-----------------|  
|*Sum*|La medida se agrega utilizando la función **Sum** .|  
|*Count*|La medida se agrega utilizando la función **Count** .|  
|*Min*|La medida se agrega utilizando la función **Min** .|  
|*Max*|La medida se agrega utilizando la función **Max** .|  
|*DistinctCount*|La medida se agrega utilizando la función **DistinctCount** .|  
|*Ninguno*|No se agrega la medida.|  
|*AverageOfChildren*|La medida se agrega devolviendo la media de sus elementos secundarios.|  
|*FirstChild*|Se agrega la medida devolviendo su primer miembro secundario.|  
|*LastChild*|Se agrega la medida devolviendo su último miembro secundario.|  
|*FirstNonEmpty*|Se agrega la medida devolviendo su primer miembro no vacío.|  
|*LastNonEmpty*|Se agrega la medida devolviendo su último miembro no vacío.|  
  
 La enumeración que corresponde a los valores permitidos para **AggregationFunction** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Vea también  
 [Cuentas de elemento &#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
