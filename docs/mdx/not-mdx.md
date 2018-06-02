---
title: NO (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5020f461d2576bbac7d0292ca0bf75bd8033e173
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580507"
---
# <a name="not-mdx"></a>NOT (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una negación lógica de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **false** si el argumento se evalúa como **true**; en caso contrario, **true**.  
  
## <a name="remarks"></a>Notas  
 El **no** operador trata la expresión como un valor booleano (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la negación lógica. La tabla siguiente se muestra cómo el **no** operador realiza la negación lógica.  
  
|*Expression1*|Valor devuelto|  
|-------------------|------------------|  
|**true**|**False**|  
|**False**|**true**|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
