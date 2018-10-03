---
title: Elemento Session (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Session Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2f18754a2ef7d44a2a85bb9da78378bc631ecd0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080395"
---
# <a name="session-element-xmla"></a>Elemento Session (XMLA)
  Utiliza el encabezado SOAP en un mensaje de solicitud SOAP para identificar una sesión explícita existente en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
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
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|SessionId|Atributo `String` requerido que identifica la sesión que se va a utilizar. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] utiliza un identificador único global (GUID) para identificar una sesión.|  
  
## <a name="remarks"></a>Comentarios  
 El elemento de encabezado `Session` identifica una sesión existente explícitamente iniciada en la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El elemento `Session` forma parte del encabezado SOAP en los siguientes tipos de mensajes:  
  
-   Una respuesta SOAP que contiene un [BeginSession](session-element-xmla.md) elemento de encabezado SOAP.  
  
-   Una solicitud SOAP para identificar la sesión en el que se va a ejecutar el [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) método.  
  
 Un identificador de sesión no garantiza que una sesión continúe siendo válida. La sesión especificada en el elemento `Session` puede expirar. Por ejemplo, una sesión puede expirar si supera el tiempo de espera o se interrumpe la conexión asociada a la sesión. Si la sesión expira o deja de ser válida, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] finaliza la sesión y revierte cualquier transacción que esté en curso en ese momento. Cualquier mensaje SOAP enviado con un identificador de sesión que ya no sea válido emitirá un error SOAP que indica que la sesión especificada no se puede encontrar.  
  
 Si un elemento `Session` no se envía como parte de una solicitud SOAP, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] iniciará implícitamente una sesión mientras que dure la llamada a los métodos `Discover` o `Execute` y, a continuación, finalizará dicha sesión una vez completada la llamada al método.  
  
## <a name="see-also"></a>Vea también  
 [Elemento EndSession &#40;XMLA&#41;](endsession-element-xmla.md)   
 [Administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Encabezados &#40;XMLA&#41;](xml-elements-headers.md)  
  
  
