---
title: Elemento Members (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c6d3eb270566bc387b2e9ce8ff48aec3c6531b6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032246"
---
# <a name="members-element-assl"></a>Elemento Members (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la colección de elementos [Member](../../../analysis-services/scripting/objects/member-element-assl.md) asociada al elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Group> <!-- or Role --<  
   ...  
   <Members>  
      <Member>...</Member>  
   </Members>  
   ...  
</Group>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Group](../../../analysis-services/scripting/objects/group-element-assl.md), [Role](../../../analysis-services/scripting/objects/role-element-assl.md)|  
|Elementos secundarios|[Miembro](../../../analysis-services/scripting/objects/member-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos que corresponden a los elementos primarios de **miembros** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Group> y <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
