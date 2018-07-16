---
title: Elemento (XMLA) del mensaje | Microsoft Docs
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
- Message Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords:
- Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fbeb2085c41e239e764621a89f34b4f17661584
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241275"
---
# <a name="message-element-xmla"></a>Elemento Message (XMLA)
  Contiene un mensaje devuelto de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] po una llamada al método [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Messages>  
   ...  
   <Message>  
      <Error>...</Error>  
      <!-- or -->  
      <Warning>...</Warning>  
   </Message>  
   ...  
</Messages>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Mensajes](messages-element-xmla.md)|  
|Elementos secundarios|[Error](error-element-xmla.md), [Warning](warning-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento se utiliza en casos en los que una llamada al método `Discover` o un comando XMLA único dentro de una llamada al método `Execute` se completa correctamente, pero con errores o advertencias. En tales casos se agrega un elemento `Messages` al elemento root después de todos los otros elementos, que a su vez contiene uno o más elementos `Message`. Cada `Message` elemento representa un único mensaje, un error o una advertencia, devuelta por la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
