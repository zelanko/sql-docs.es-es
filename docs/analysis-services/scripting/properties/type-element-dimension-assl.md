---
title: Tipo de elemento (Dimension) (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3af3168c39f685702154bb7c76435bd1d241a642
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039369"
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
  
  
