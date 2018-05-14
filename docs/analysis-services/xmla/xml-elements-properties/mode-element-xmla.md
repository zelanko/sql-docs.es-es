---
title: Elemento Mode (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 87ae7f667e4275c3c41253bc5374edc40bcc35a6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Identifica el modo que va a usar el elemento primario [bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) elemento para crear un bloqueo en un objeto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento primario **bloqueo** elemento utiliza el **modo** elemento para determinar el tipo de bloqueo que cree en un objeto. El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Se establece un bloqueo compartido en el objeto especificado. Se pueden crear otros bloqueos compartidos para el mismo objeto.<br /><br /> Un bloqueo compartido impide que las transacciones que contienen operaciones de escritura, como un [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método que ejecuta un [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, en un objeto especificado, confirmar hasta que se quite el bloqueo compartido. Un bloqueo compartido no evita que las transacciones que contienen operaciones de lectura, como un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) llamada al método o una **Execute** llamada al método que ejecuta un [instrucción](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando confirmar.|  
|*CommitExclusive*|Se establece un bloqueo exclusivo en el objeto especificado. No se puede crear otros bloqueos compartidos o exclusivos para el mismo objeto.<br /><br /> Un bloqueo exclusivo impide que se confirmen las transacciones que contienen operaciones de lectura o escritura en un objeto especificado hasta que se quite el bloqueo exclusivo.|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento Object & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
