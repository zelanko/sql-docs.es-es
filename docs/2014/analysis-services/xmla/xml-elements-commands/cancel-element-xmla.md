---
title: Elemento Cancel (XMLA) | Documentos de Microsoft
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
- Cancel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cd0fdd50a1dcddb51d167ab76cd5408b631bb3ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199451"
---
# <a name="cancel-element-xmla"></a>Elemento Cancel (XMLA)
  Cancela un comando que se está ejecutando un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
</Command>  
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
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[CancelAssociated](../xml-elements-properties/cancelassociated-element-xmla.md), [ConnectionID](../xml-elements-properties/id-element-xmla.md), [SessionID](../xml-elements-properties/sessionid-element-xmla.md), [SPID](../xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El comando `Cancel` cancela los comandos que actualmente están en ejecución en el contexto de una sesión. Si la aplicación cliente no ha solicitado una sesión, no se puede cancelar un comando.  
  
 Si el comando `Cancel` se ejecuta durante la ejecución de un comando `Batch`, se cancela el comando `Batch` completo. Si el comando `Batch` es transaccional, todos los comandos contenidos por el comando `Batch` se revierten. Si el comando `Batch` no es transaccional, solo se revierten los comandos contenidos por el comando `Batch` que se estaban ejecutando en el momento en que se ejecutó el comando `Cancel`. Los comandos de un comando `Batch` no transaccional que ya se ha ejecutado no se revertirán.  
  
 Normalmente, el comando `Cancel` se utiliza para cancelar comandos que se están ejecutando actualmente en la sesión activa. En ese caso, no se debe especificar ninguno de los elementos secundarios del comando `Cancel`. Los administradores también pueden utilizar el comando `Cancel` para cancelar comandos que se ejecutan en conexiones o sesiones que no sean la sesión activa actualmente. Los miembros de un rol que tiene permisos de administración de una base de datos determinada pueden cancelar comandos de conexiones y sesiones aplicables a esa base de datos, mientras que los administradores del servidor pueden cancelar comandos de conexiones y sesiones de una instancia de los Analysis Service determinada.  
  
 Para recuperar información sobre las conexiones y sesiones actuales de una instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], se puede ejecutar el método `Discover` para solicitar conjuntos de filas de esquema DISCOVER_CONNECTIONS y DISCOVER_SESSIONS, respectivamente. Los miembros de un rol que tienen permisos de administración para una base de datos determinada solo pueden devolver sesiones de una base de datos determinada especificando esa base de datos en la columna de restricción de SESSION_CURRENT_DATABASE para el conjunto de filas de esquema de DISCOVER_SESSIONS. Para obtener más información sobre la `Discover` método, consulte [método detectar &#40;XMLA&#41;](../xml-elements-methods-discover.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote &#40;XMLA&#41;](batch-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  