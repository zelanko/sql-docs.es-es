---
title: Elemento aliases (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Aliases Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aliases
helpviewer_keywords:
- Aliases element
ms.assetid: 9de9e683-d30d-4d61-b32d-c5a946825742
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 677434b5ea6383e5905a703225edb5e56e3fb4e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267691"
---
# <a name="aliases-element-assl"></a>Elemento Aliases (ASSL)
  Contiene la colección de [Alias](../properties/alias-element-assl.md) elementos asociados con un [cuenta](../objects/account-element-assl.md) elemento  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Account>  
      ...  
   <Aliases>  
      <Alias>...</Alias>  
      </Aliases>  
      ...  
</Account>  
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
|Elementos primarios|[Cuenta](../objects/account-element-assl.md)|  
|Elementos secundarios|[Alias](../properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente al elemento primario de `Aliases` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Vea también  
 [Cuentas de elemento &#40;ASSL&#41;](accounts-element-assl.md)   
 [Elemento de la base de datos &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
