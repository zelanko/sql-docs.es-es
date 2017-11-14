---
title: Elemento Mode (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57c3450e8928b24dc03e2d5915983f39330d0b0c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mode-element-xmla"></a>Elemento Mode (XMLA)
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
 [Id. de elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)   
 [Elemento Object &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

