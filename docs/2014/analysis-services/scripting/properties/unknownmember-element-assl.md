---
title: Elemento UnknownMember (ASSL) | Microsoft Docs
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
- UnknownMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fdfbaa296a7c83c96a7a41d759d582833d2ed8e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151176"
---
# <a name="unknownmember-element-assl"></a>Elemento UnknownMember (ASSL)
  Indica si el miembro desconocido está visible.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Ninguno*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Dimension](../objects/dimension-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Visible*|El miembro desconocido existe y se muestra.|  
|*Oculto*|El miembro desconocido existe pero no se muestra.|  
|*Ninguno*|El miembro desconocido no se usa.|  
  
 La enumeración que corresponde a los valores permitidos para `UnknownMember` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento UnknownMemberName &#40;ASSL&#41;](name-element-assl.md)   
 [Elemento UnknownMemberTranslation &#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
