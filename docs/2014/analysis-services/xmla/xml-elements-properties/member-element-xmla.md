---
title: Elemento Member (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Member
- microsoft.xml.analysis.member
- http://schemas.microsoft.com/analysisservices/2003/engine#Member
helpviewer_keywords:
- Member element
ms.assetid: 5cc33a1f-192e-4821-a4ef-9a5f2bb7a9f0
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f612e2cff38d71a956a9f273feba54cb8a867ffd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109014"
---
# <a name="member-element-xmla"></a>Elemento Member (XMLA)
  Representa un único miembro de un elemento primario [Members](members-element-xmla.md) o [Tuple](tuple-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Members](members-element-xmla.md), [Tuple](tuple-element-xmla.md)|  
|Elementos secundarios|[Caption](caption-element-xmla.md), [DisplayInfo](displayinfo-element-xmla.md), [LName](name-element-xmla.md), [LNum](lnum-element-xmla.md), [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|Hierarchy|Atributo `String` necesario (solo para elementos primarios `Tuple`). El nombre de la jerarquía a la que pertenece el miembro representado por el elemento `Member`.|  
  
## <a name="remarks"></a>Notas  
 El elemento `Member` contiene la información necesaria para identificar y mostrar un miembro dentro de una jerarquía determinada. La jerarquía de los elementos primarios `Members` ya está especificada por el atributo `Hierarchy` del elemento primario. La jerarquía de los elementos primarios `Tuple` se especifica en el atributo `Hierarchy` del elemento `Member`.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  