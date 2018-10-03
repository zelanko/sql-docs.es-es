---
title: Elemento HideMemberIf (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- HideMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- HideMemberIf
helpviewer_keywords:
- HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae715268b4b62c88e8d4f660c7d8d1772ccae02c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109005"
---
# <a name="hidememberif-element-assl"></a>Elemento HideMemberIf (ASSL)
  Indica si un miembro en un nivel debe ocultarse de las aplicaciones cliente y cuándo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Nunca*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Level](../objects/level-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Nunca*|Los miembros nunca se ocultan.|  
|*OnlyChildWithNoName*|Se oculta un miembro cuando es el único elemento secundario de un elemento primario y su nombre está vacío.|  
|*OnlyChildWithParentName*|Un miembro está oculto cuando es el único elemento secundario de su elemento primario y su nombre es idéntico al de su primario.|  
|*NoName*|Un miembro está oculto cuando su nombre está vacío.|  
|*ParentName*|Un miembro está oculto cuando su nombre es idéntico al de su primario.|  
  
## <a name="remarks"></a>Comentarios  
 La enumeración que corresponde a los valores permitidos para `HideMemberIf` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.HideIfValue>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
