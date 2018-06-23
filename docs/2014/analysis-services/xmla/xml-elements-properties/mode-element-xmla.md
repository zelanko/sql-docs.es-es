---
title: Elemento Mode (XMLA) | Documentos de Microsoft
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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5634e273e1708f9de213436e20008cc6874f50a7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204682"
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
  Identifica el modo que va a usar el elemento primario [bloqueo](../xml-elements-commands/lock-element-xmla.md) elemento para crear un bloqueo en un objeto especificado.  
  
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
|*CommitShared*|Se establece un bloqueo compartido en el objeto especificado. Se pueden crear otros bloqueos compartidos para el mismo objeto.<br /><br /> Un bloqueo compartido impide que las transacciones que contienen operaciones de escritura, como un [Execute](../xml-elements-methods-execute.md) llamada al método que ejecuta un [Alter](../xml-elements-commands/alter-element-xmla.md) comando, en un objeto especificado, confirmar hasta que se quite el bloqueo compartido. Un bloqueo compartido no evita que las transacciones que contienen operaciones de lectura, como un [Discover](../xml-elements-methods-discover.md) llamada al método o una `Execute` llamada al método que ejecuta un [instrucción](../xml-elements-commands/statement-element-xmla.md) comando confirmen.|  
|*CommitExclusive*|Se establece un bloqueo exclusivo en el objeto especificado. No se puede crear otros bloqueos compartidos o exclusivos para el mismo objeto.<br /><br /> Un bloqueo exclusivo impide que se confirmen las transacciones que contienen operaciones de lectura o escritura en un objeto especificado hasta que se quite el bloqueo exclusivo.|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento de objeto &#40;XMLA&#41;](object-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  