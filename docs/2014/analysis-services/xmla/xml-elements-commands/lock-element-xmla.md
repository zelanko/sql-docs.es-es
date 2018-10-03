---
title: Bloquear elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Lock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5d603c2708cb42b666d3cc0c9acc5ea208f0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079525"
---
# <a name="lock-element-xmla"></a>Elemento Lock (XMLA)
  Bloquea un objeto especificado en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Id. de](../xml-elements-properties/id-element-xmla.md), [modo](../xml-elements-properties/mode-element-xmla.md), [objeto](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando `Lock` bloquea un objeto, para uso compartido o exclusivo, dentro del contexto de la transacción actualmente activa. Solo los administradores de bases de datos o de servidores pueden ejecutar explícitamente un comando `Lock`. Un bloqueo en un objeto impide que se confirmen las transacciones hasta que se quita el bloqueo. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite dos tipos de bloqueos, bloqueos compartidos y bloqueos exclusivos. Para obtener más información acerca de los tipos de bloqueo admitidos por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40;XMLA&#41;](../xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] solamente permite bloquear las bases de datos. El elemento `Object` debe contener una referencia de objeto a una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Si no se especifica el elemento `Object` o el elemento `Object` hace referencia a un objeto que no es una base de datos, se produce un error.  
  
 Otros comandos ejecutan implícitamente un comando `Lock` en una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Cualquier operación que lee datos o metadatos de una base de datos, como cualquier método `Discover` o un método `Execute` que ejecuta un comando `Statement`, emite implícitamente un bloqueo compartido en la base de datos. Cualquier transacción que confirma los cambios de los datos o metadatos en un objeto de una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], como un método `Execute` que ejecuta un comando `Alter`, emite implícitamente un bloqueo exclusivo en la base de datos.  
  
 Todos los bloqueos se mantienen en el contexto de la transacción actual. Cuando la transacción actual se confirma o se revierte, se liberan automáticamente todos los bloqueos definidos dentro de la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Unlock &#40;XMLA&#41;](lock-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
