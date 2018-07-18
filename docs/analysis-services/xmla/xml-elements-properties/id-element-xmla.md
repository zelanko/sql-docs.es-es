---
title: Elemento ID (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18c0a9e1db03ef30b54b788d16223e70bc9e9059
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38037033"
---
# <a name="id-element-xmla"></a>Elemento ID (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Identifica un bloqueo en el que se va a ejecutar el elemento primario [bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) o [Unlock](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Lock> <!-- or Unlock>  
   ...  
   <ID>...</ID>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **ID** elemento contiene un identificador único global (GUID) utilizado para identificar un bloqueo.  
  
## <a name="see-also"></a>Vea también
 [Elemento de objeto &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Elemento Mode &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
