---
title: Elemento CollectionCaption (ASSL) | Documentos de Microsoft
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
ms.assetid: 33929373-11df-4f89-8d2e-d63923c44f53
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bba7c2ab2cffb2287b1eff84c5e9fc9f385119cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198533"
---
# <a name="collectioncaption-element-assl"></a>Elemento CollectionCaption (ASSL)
  Contiene el nombre plural del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndTranslation>  
   <CollectionCaption>...</CollectionCaption>  
</RelationshipEndTranslation>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndTranslation](../objects/translation-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que corresponde al elemento primario de `CollectionCaption` en el objeto de Analysis Management Objects (AMO) modelo es relationshipendtranslation.  
  
  