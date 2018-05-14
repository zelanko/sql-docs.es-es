---
title: Elemento Cancel (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e8c4f015d5a606d67cb4c6b5f0519875db58b416
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="cancel-element-xmla"></a>Elemento Cancel (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
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
  
 Para recuperar información sobre las conexiones actuales y las sesiones para un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, el **Discover** el método puede ejecutarse para solicitar, respectivamente, los conjuntos de filas de esquema DISCOVER_CONNECTIONS y DISCOVER_SESSIONS. Los miembros de un rol que tienen permisos de administración para una base de datos determinada solo pueden devolver sesiones de una base de datos determinada especificando esa base de datos en la columna de restricción de SESSION_CURRENT_DATABASE para el conjunto de filas de esquema de DISCOVER_SESSIONS. Para obtener más información sobre la **Discover** método, consulte [método detectar &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
