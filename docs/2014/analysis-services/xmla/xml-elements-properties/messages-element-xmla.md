---
title: Mensajes de elemento (XMLA) | Microsoft Docs
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
- Messages Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Messages
- microsoft.xml.analysis.messages
- urn:schemas-microsoft-com:xml-analysis#Messages
helpviewer_keywords:
- Messages element
ms.assetid: 719d15ff-f18b-4c56-80ba-a9114c0b7d8a
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0fbaba30716831ef34a40dd94c6c9b2ab507641
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176782"
---
# <a name="messages-element-xmla"></a>Elemento Messages (XMLA)
  Contiene una colección de elementos [Message](message-element-xmla.md) devueltos de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] po una llamada al método [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Resultset>  
   <Messages>  
      <Message>  
   </Messages>  
</Resultset>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Conjunto de resultados](../xml-data-types/resultset-data-type-xmla.md)|  
|Elementos secundarios|[de mensaje](message-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento se utiliza en casos en los que una llamada al método `Discover` o un comando XMLA único dentro de una llamada al método `Execute` se completa correctamente, pero con errores o advertencias. En tales casos, un `Messages` elemento se agrega a la [raíz](root-element-xmla.md) elemento después de todos los demás elementos, que a su vez contiene uno o más `Message` elementos. Cada `Message` elemento representa un único mensaje, un error o una advertencia, devuelta por la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
