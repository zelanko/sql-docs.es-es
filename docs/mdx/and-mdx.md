---
title: Y (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AND
dev_langs:
- kbMDX
helpviewer_keywords:
- AND, MDX
ms.assetid: 398fd483-d010-4524-b115-0becad66f25c
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 870aac2a9eb1c799cf6d83ddbe119d91c1f11f8e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="and-mdx"></a>AND (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una conjunción lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 *Expression2*  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve true si ambos parámetros se evalúan como **true**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Comentarios  
 El **AND** operador trata a ambas expresiones como valores booleanos (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la conjunción lógica. La tabla siguiente se muestra cómo el **AND** operador realiza la conjunción lógica.  
  
|*Expression1*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**False**|**False**|  
|**False**|**true**|**False**|  
|**False**|**False**|**False**|  
  
## <a name="example"></a>Ejemplo  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is between 20% and 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .3 AND   
      [Measures].[Gross Profit Margin] >= .2,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
