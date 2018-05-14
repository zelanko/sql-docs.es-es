---
title: Elemento Subscribe (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 548336f5e891cc41c485bed4047c1223d0f9344c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="subscribe-element-xmla"></a>Elemento Subscribe (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Se suscribe a un seguimiento y devuelve un conjunto de filas que contiene los eventos de seguimiento desde una [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
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
|Elementos secundarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **suscribir** comando se suscribe a y secuencias de realizar la copia de un conjunto de filas de un seguimiento especificado en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si se especifica que no sea un seguimiento en el elemento **Object** , se produce un error.  
  
 Si el **objeto** elemento no se especifica, se define un seguimiento de sesión y se suscribe, en la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. El seguimiento de la sesión devuelve un conjunto fijo de eventos de seguimiento desde la sesión actual.  
  
 La secuencia de conjunto de filas devuelta por este comando se termina si la aplicación cliente cierra la conexión con el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, o si la sesión en la que el **suscribir** se ejecuta el comando finaliza.  
  
## <a name="see-also"></a>Vea también  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
