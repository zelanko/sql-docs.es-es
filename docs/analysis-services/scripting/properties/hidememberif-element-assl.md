---
title: Elemento HideMemberIf (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0e01cbbf403636bf42a806ba516f9947eaab20e4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="hidememberif-element-assl"></a>Elemento HideMemberIf (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Elemento primario|[Nivel](../../../analysis-services/scripting/objects/level-element-assl.md)|  
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
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
