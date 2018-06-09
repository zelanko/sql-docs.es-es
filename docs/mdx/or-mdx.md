---
title: O (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 668e8f1955290c31ee63ca5b81fc5e9c286d54c4
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742454"
---
# <a name="or-mdx"></a>OR (MDX)


  Realiza una disyunción lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parámetros  
 Expression1  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 Expression2  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **true** si uno o ambos argumentos se evalúan como **true**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Notas  
 El **o** operador trata a ambos argumentos como valores booleanos (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la disyunción lógica. La tabla siguiente se muestra cómo el **o** operador realiza la disyunción lógica.  
  
|*Expression1*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**False**|**true**|  
|**False**|**true**|**true**|  
|**False**|**False**|**False**|  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta contiene una medida calculada que devuelve la cadena "MARRIED OR MALE" si el miembro actual en la jerarquía Gender de la dimensión Customer es Male o el miembro actual de la jerarquía Marital Status de la dimensión Customer es Married; de lo contrario devuelve la cadena "UNMARRIEDA OR FEMALE".  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
