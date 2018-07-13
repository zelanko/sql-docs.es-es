---
title: Elemento AllMemberTranslations (ASSL) | Microsoft Docs
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
- AllMemberTranslations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberTranslations
helpviewer_keywords:
- AllMemberTranslations element
ms.assetid: 982ee2bf-c88d-4da5-a679-7a6b08a48a0d
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 977168f25f81c1755b6c25e442bae4b7e6e3bfa7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171546"
---
# <a name="allmembertranslations-element-assl"></a>Elemento AllMemberTranslations (ASSL)
  Contiene la colección de [traducción](../objects/translation-element-assl.md) elementos para el título del miembro All de un [jerarquía](../objects/hierarchy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Hierarchy>  
   ...  
   <AllMemberTranslations>  
      <AllMemberTranslation xsi:type="Translation">...  
            </AllMemberTranslation>  
   </AllMemberTranslations>  
      ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno (colección)|  
|Valor predeterminado|Ninguno (colección)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Hierarchy](../objects/hierarchy-element-assl.md)|  
|Elementos secundarios|[AllMemberTranslation](../objects/allmembertranslation-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente al elemento primario de `AllMemberTranslations` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Hierarchy>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Translation &#40;ASSL&#41;](../objects/translation-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
