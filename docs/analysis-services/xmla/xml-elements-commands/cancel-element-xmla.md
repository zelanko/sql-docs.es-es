---
title: Elemento Cancel (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- Cancel Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c50ff4e923e046a157c06ccb139e1b8645d1e9aa
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="cancel-element-xmla"></a>Elemento Cancel (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Cancela un comando que se está ejecutando un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[CancelAssociated](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md), [ConnectionID](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md), [SessionID](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md), [SPID](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando **Cancel** cancela los comandos que actualmente están en ejecución en el contexto de una sesión. Si la aplicación cliente no ha solicitado una sesión, no se puede cancelar un comando.  
  
 Si el comando **Cancel** se ejecuta durante la ejecución de un comando **Batch** , se cancela el comando **Batch** completo. Si el comando **Batch** es transaccional, todos los comandos contenidos por el comando **Batch** se revierten. Si el comando **Batch** no es transaccional, solo se revierten los comandos contenidos por el comando **Batch** que se estaban ejecutando en el momento en que se ejecutó el comando **Cancel** . Los comandos de un comando **Batch** no transaccional que ya se ha ejecutado no se revertirán.  
  
 Normalmente, el comando **Cancel** se utiliza para cancelar comandos que se están ejecutando actualmente en la sesión activa. En ese caso, no se debe especificar ninguno de los elementos secundarios del comando **Cancel** . Los administradores también pueden utilizar el comando **Cancel** para cancelar comandos que se ejecutan en conexiones o sesiones que no sean la sesión activa actualmente. Los miembros de un rol que tiene permisos de administración de una base de datos determinada pueden cancelar comandos de conexiones y sesiones aplicables a esa base de datos, mientras que los administradores del servidor pueden cancelar comandos de conexiones y sesiones de una instancia de los Analysis Service determinada.  
  
 Para recuperar información sobre las conexiones actuales y las sesiones para un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, el **Discover** el método puede ejecutarse para solicitar, respectivamente, los conjuntos de filas de esquema DISCOVER_CONNECTIONS y DISCOVER_SESSIONS. Los miembros de un rol que tienen permisos de administración para una base de datos determinada solo pueden devolver sesiones de una base de datos determinada especificando esa base de datos en la columna de restricción de SESSION_CURRENT_DATABASE para el conjunto de filas de esquema de DISCOVER_SESSIONS. Para obtener más información sobre la **Discover** método, consulte [método detectar &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-methods-discover.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
