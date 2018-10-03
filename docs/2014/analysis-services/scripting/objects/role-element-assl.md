---
title: Elemento role (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Role Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ROLE
helpviewer_keywords:
- Role element
ms.assetid: 56f52462-a7fd-4b51-a7fb-4311134439e9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 720eb01952d52e7c1b9a1ec73bae272694b1597a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084041"
---
# <a name="role-element-assl"></a>Elemento Role (ASSL)
  Contiene información sobre un rol de seguridad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Roles>  
      <Role>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreateTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Members>...</Members>  
      <Annotations>...</Annotations>  
   </Role>  
</Roles>  
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
|Elementos primarios|[Roles](../collections/roles-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descripción](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [miembros ](../collections/members-element-assl.md), [Nombre](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 La definición del rol incluye los usuarios que son miembros del rol.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de la base de datos &#40;ASSL&#41;](database-element-assl.md)   
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
