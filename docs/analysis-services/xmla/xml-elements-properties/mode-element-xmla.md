---
title: Elemento Mode (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Mode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Mode
- microsoft.xml.analysis.mode
- http://schemas.microsoft.com/analysisservices/2003/engine#Mode
helpviewer_keywords:
- Mode element
ms.assetid: 43a54181-6494-48c3-b14b-376d8939fa9f
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 656ea9623b7dea8296bc10221c916fe7afdd0568
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Identifica el modo que va a usar el elemento primario [bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) elemento para crear un bloqueo en un objeto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Lock>  
   ...  
   <Mode>...</Mode>  
   ...  
</Lock>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento primario **bloqueo** elemento utiliza el **modo** elemento para determinar el tipo de bloqueo que cree en un objeto. El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*CommitShared*|Se establece un bloqueo compartido en el objeto especificado. Se pueden crear otros bloqueos compartidos para el mismo objeto.<br /><br /> Un bloqueo compartido impide que las transacciones que contienen operaciones de escritura, como un [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método que ejecuta un [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, en un objeto especificado, confirmar hasta que se quite el bloqueo compartido. Un bloqueo compartido no evita que las transacciones que contienen operaciones de lectura, como un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) llamada al método o una **Execute** llamada al método que ejecuta un [instrucción](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando confirmar.|  
|*CommitExclusive*|Se establece un bloqueo exclusivo en el objeto especificado. No se puede crear otros bloqueos compartidos o exclusivos para el mismo objeto.<br /><br /> Un bloqueo exclusivo impide que se confirmen las transacciones que contienen operaciones de lectura o escritura en un objeto especificado hasta que se quite el bloqueo exclusivo.|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento Object &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
