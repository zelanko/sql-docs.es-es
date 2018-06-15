---
title: Elemento AggregateFunction (ASSL) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f0b499b81d8c29c51cc086127bad8749ee089120
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036646"
---
# <a name="aggregatefunction-element-assl"></a>Elemento AggregateFunction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define el tipo de función de agregado usada por un [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Measure>  
   ...  
   <AggregateFunction>...</AggregateFunction>  
   ...  
</Measure>  
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
|Elementos primarios|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sum*|La medida se agrega utilizando la función **Sum** .|  
|*Count*|La medida se agrega utilizando la función **Count** .|  
|*Min*|La medida se agrega utilizando la función **Min** .|  
|*Max*|La medida se agrega utilizando la función **Max** .|  
|*DistinctCount*|La medida se agrega utilizando la función **DistinctCount** .|  
|*Ninguno*|No se agrega la medida.|  
|*ByAccount*|La cuenta agrega la medida.|  
|*AverageOfChildren*|La medida se agrega devolviendo la media de sus elementos secundarios.|  
|*FirstChild*|Se agrega la medida devolviendo su primer miembro secundario.|  
|*LastChild*|Se agrega la medida devolviendo su último miembro secundario.|  
|*FirstNonEmpty*|Se agrega la medida devolviendo su primer miembro no vacío.|  
|*LastNonEmpty*|Se agrega la medida devolviendo su último miembro no vacío.|  
  
 La enumeración que corresponde a los valores permitidos para **AggregateFunction** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
