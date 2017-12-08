---
title: Elemento HideMemberIf (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: HideMemberIf Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HideMemberIf
helpviewer_keywords: HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eefed5009773186d939401a508785abe4f956125
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nunca*|Los miembros nunca se ocultan.|  
|*OnlyChildWithNoName*|Se oculta un miembro cuando es el único elemento secundario de un elemento primario y su nombre está vacío.|  
|*OnlyChildWithParentName*|Un miembro está oculto cuando es el único elemento secundario de su elemento primario y su nombre es idéntico al de su primario.|  
|*NoName*|Un miembro está oculto cuando su nombre está vacío.|  
|*ParentName*|Un miembro está oculto cuando su nombre es idéntico al de su primario.|  
  
## <a name="remarks"></a>Comentarios  
 La enumeración que corresponde a los valores permitidos para **HideMemberIf** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.HideIfValue>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
