---
title: Objeto de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Object Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: 99470537-2c4a-4072-9613-940c41c12487
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4fb7e25b9e813487b612bbd6269c2f080d85f5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178755"
---
# <a name="object-element-xmla"></a>Elemento Object (XMLA)
  Contiene una referencia de objeto usada por el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Alter> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <!-- One or more object identifiers, depending on the parent element -->  
   </Object>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|Antecesor o elemento primario: [Alter](../xml-elements-commands/create-element-xmla.md) &#124; 0-1: elemento opcional que puede aparecer solo una vez.<br /><br /> Antecesor o elemento primario: todos los demás &#124; 1-1: elemento necesario que se produce solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[ALTER](../xml-elements-commands/alter-element-xmla.md), [copia de seguridad](../xml-elements-commands/backup-element-xmla.md), [ClearCache](../xml-elements-commands/clearcache-element-xmla.md), [eliminar](../xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md), [bloqueo](../xml-elements-commands/lock-element-xmla.md), [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md), [proceso](../xml-elements-commands/process-element-xmla.md), [suscribirse](../xml-elements-commands/subscribe-element-xmla.md), [sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|Elementos requeridos de Analysis Services Scripting Language (ASSL). Se especifican haciendo una lista de los elementos Id. del objeto y de sus antecesores (excepto del objeto `Server`.) Por ejemplo, el elemento `Object` siguiente identifica una partición:<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>Comentarios  
 El orden en el que los identificadores aparecen no es importante.  
  
 Para `Alter` elementos, la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se usa como el objeto predeterminado si el `Object` no se especifica el elemento.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
