---
title: Dimensión de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63b9043b3ba88200a060a8b333ff53cf95340df3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578347"
---
# <a name="dimension-element-xmla"></a>Elemento Dimension (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Identifica la dimensión de cubo representada por el elemento primario [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Object>  
   ...  
   <Dimension>...</Dimension>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **dimensión** elemento es un identificador de objeto que contiene el nombre de la dimensión de cubo representada por la **objeto** elemento.  
  
## <a name="see-also"></a>Vea también
 [Elemento de la base de datos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)   
 [Elemento Dimension (XMLA)](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
