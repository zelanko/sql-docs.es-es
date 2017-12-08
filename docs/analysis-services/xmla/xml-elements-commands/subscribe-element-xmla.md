---
title: Elemento Subscribe (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
apiname: Subscribe Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords: Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 324239ae113bc5f1323de718462a904b15fabc11
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="subscribe-element-xmla"></a>Elemento Subscribe (XMLA)
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
|Elementos secundarios|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **suscribir** comando se suscribe a y secuencias de realizar la copia de un conjunto de filas de un seguimiento especificado en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si se especifica que no sea un seguimiento en el elemento **Object** , se produce un error.  
  
 Si el **objeto** elemento no se especifica, se define un seguimiento de sesión y se suscribe, en la [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. El seguimiento de la sesión devuelve un conjunto fijo de eventos de seguimiento desde la sesión actual.  
  
 La secuencia de conjunto de filas devuelta por este comando se termina si la aplicación cliente cierra la conexión con el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, o si la sesión en la que el **suscribir** se ejecuta el comando finaliza.  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
