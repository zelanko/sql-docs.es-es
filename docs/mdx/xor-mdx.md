---
title: XOR (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb0a91faaec7e5c2b6a7b2289e65989ba19b33e3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581877"
---
# <a name="xor-mdx"></a>XOR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una exclusión lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 *Expression2*  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **true** si uno y solo un argumento se evalúa como **true**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Notas  
 El **XOR** operador trata a ambos operadores como valores booleanos (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la exclusión lógica. La tabla siguiente se muestra cómo el **XOR** operador realiza la exclusión lógica.  
  
|*Expression1*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**False**|  
|**true**|**False**|**true**|  
|**False**|**true**|**true**|  
|**False**|**False**|**False**|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
