---
title: Bloquear elemento (XMLA) | Documentos de Microsoft
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
apiname: Lock Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords: Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9d8ca1aec0fb36214dbceb92d3bcfafb6bf4a983
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="lock-element-xmla"></a>Elemento Lock (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Bloquea un objeto especificado en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
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
|Elementos secundarios|[Id. de](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md), [modo](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md), [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando **Lock** bloquea un objeto, para uso compartido o exclusivo, dentro del contexto de la transacción actualmente activa. Solo los administradores de bases de datos o de servidores pueden ejecutar explícitamente un comando **Lock** . Un bloqueo en un objeto impide que se confirmen las transacciones hasta que se quita el bloqueo. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite dos tipos de bloqueos, bloqueos compartidos y bloqueos exclusivos. Para obtener más información acerca de los tipos de bloqueo compatibles con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] solamente permite bloquear las bases de datos. El **objeto** elemento debe contener una referencia de objeto a una [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos. Si no se especifica el elemento **Object** o el elemento **Object** hace referencia a un objeto que no es una base de datos, se produce un error.  
  
 Otros comandos ejecutan implícitamente un **bloqueo** comando un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos. Cualquier operación que lee datos o metadatos de una base de datos, como cualquier método **Discover** o un método **Execute** que ejecuta un comando **Statement** , emite implícitamente un bloqueo compartido en la base de datos. Cualquier transacción que confirma los cambios de datos o metadatos en un objeto en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos, como un **Execute** método que se ejecuta un **Alter** comando, emite implícitamente un bloqueo exclusivo en el base de datos.  
  
 Todos los bloqueos se mantienen en el contexto de la transacción actual. Cuando la transacción actual se confirma o se revierte, se liberan automáticamente todos los bloqueos definidos dentro de la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Desbloquear elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
