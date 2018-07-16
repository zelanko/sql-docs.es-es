---
title: Elemento Mode (XMLA) | Microsoft Docs
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
- Mode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c90d67995e6775c035265db57c2b55380ad0fe76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267651"
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
  Identifica el modo que va a usar el elemento primario [bloqueo](../xml-elements-commands/lock-element-xmla.md) elemento cuando se crea un bloqueo en un objeto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bloqueo](../xml-elements-commands/lock-element-xmla.md), [desbloquear](../xml-elements-commands/unlock-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento primario `Lock` usa el elemento `Mode` para determinar el tipo de bloqueo que ha de crear para un objeto. El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*CommitShared*|Se establece un bloqueo compartido en el objeto especificado. Se pueden crear otros bloqueos compartidos para el mismo objeto.<br /><br /> Un bloqueo compartido impide que las transacciones que contienen operaciones de escritura, como un [Execute](../xml-elements-methods-execute.md) llamada al método ejecuta un [Alter](../xml-elements-commands/alter-element-xmla.md) comando en un objeto especificado, confirmar hasta que se quite el bloqueo compartido. Un bloqueo compartido no evita que las transacciones que contienen operaciones de lectura, como un [Discover](../xml-elements-methods-discover.md) llamada al método o una `Execute` llamada al método ejecuta un [instrucción](../xml-elements-commands/statement-element-xmla.md) comando confirmen.|  
|*Commitexclusive para*|Se establece un bloqueo exclusivo en el objeto especificado. No se puede crear otros bloqueos compartidos o exclusivos para el mismo objeto.<br /><br /> Un bloqueo exclusivo impide que se confirmen las transacciones que contienen operaciones de lectura o escritura en un objeto especificado hasta que se quite el bloqueo exclusivo.|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento de objeto &#40;XMLA&#41;](object-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
