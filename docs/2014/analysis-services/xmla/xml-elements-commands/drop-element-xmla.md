---
title: Elemento DROP (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Drop Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Drop
- microsoft.xml.analysis.drop
- http://schemas.microsoft.com/analysisservices/2003/engine#Drop
helpviewer_keywords:
- Drop element
ms.assetid: a5d21db3-743a-4958-b16d-b6816a5ee787
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b723e6ae10ae045ce43c7138ce481ffdab3955bd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194945"
---
# <a name="drop-element-xmla"></a>Elemento Drop (XMLA)
  Elimina miembros de atributo de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Drop>  
      <Object>...</Object>  
      <DeleteWithDescendants>...</DeleteWithDescendants>  
      <Where>...</Where>  
   </Drop>  
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
|Elementos secundarios|[DeleteWithDescendants](../xml-elements-properties/deletewithdescendants-element-xmla.md), [objeto](../xml-elements-properties/object-element-dimension-xmla.md), [donde](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando `Drop` elimina los miembros de atributo de una dimensión habilitada para escritura.  
  
 Para obtener más información acerca de cómo eliminar los miembros, vea [Insertar, actualizar y quitar miembros &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento &#40;XMLA&#41;](insert-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](update-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
