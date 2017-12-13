---
title: Elemento (XMLA) del mensaje | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Message Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.message
- http://schemas.microsoft.com/analysisservices/2003/engine#Message
- urn:schemas-microsoft-com:xml-analysis#Message
helpviewer_keywords: Message element
ms.assetid: 028911e2-9779-43b1-824d-6d7fb2295885
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1370ae3b3f37e28d212a37219a0ad50be0da740f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="message-element-xmla"></a>Elemento Message (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene un mensaje devuelto de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] por una [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Mensajes](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|Elementos secundarios|[Error](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md), [Warning](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento se utiliza en casos en los que una llamada al método **Discover** o un comando XMLA único dentro de una llamada al método **Execute** se completa correctamente, pero con errores o advertencias. En tales casos se agrega un elemento **Messages** al elemento root después de todos los otros elementos, que a su vez contiene uno o más elementos **Message** . Cada elemento **Message** representa un mensaje único, un error o una advertencia, devuelta por la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
