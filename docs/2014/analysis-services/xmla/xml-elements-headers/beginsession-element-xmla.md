---
title: Elemento BeginSession (XMLA) | Microsoft Docs
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
- BeginSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf272ae8221b66f7ac8390fab900d22d6b8aaf87
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285831"
---
# <a name="beginsession-element-xmla"></a>Elemento BeginSession (XMLA)
  Utiliza un encabezado SOAP en un mensaje de solicitud SOAP para iniciar una nueva sesión en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
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
|Elementos primarios|None|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento de encabezado `BeginSession` forma parte de una solicitud SOAP enviada a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e inicia explícitamente una nueva sesión en la instancia. El encabezado SOAP devuelto por la respuesta SOAP contiene un [sesión](session-element-xmla.md) elemento que identifica la sesión nuevo. Este nuevo identificador de sesión se puede almacenar y enviar en solicitudes SOAP posteriores utilizando el elemento de encabezado `Session`.  
  
 Si no se envía el elemento de encabezado `BeginSession`, no se inicia explícitamente una sesión. Si no se inicia una sesión explícitamente, no se pueden administrar transacciones en esa sesión. En otras palabras, no se puede usar el siguiente código XML para los comandos de Analysis (XMLA): [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md), y [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md). Todos los métodos XMLA y comandos ejecutados en una sesión iniciada implícitamente se consideran transacciones atómicas.  
  
## <a name="see-also"></a>Vea también  
 [Elemento EndSession &#40;XMLA&#41;](endsession-element-xmla.md)   
 [Elemento de la sesión &#40;XMLA&#41;](session-element-xmla.md)   
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
