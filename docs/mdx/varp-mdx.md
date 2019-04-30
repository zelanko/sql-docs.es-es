---
title: VarP (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc1e6276de9a03af9800b9e242d54130c4241732
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251482"
---
# <a name="varp-mdx"></a>VarP (MDX)


  Devuelve la varianza de población de una expresión numérica evaluada sobre un conjunto mediante la fórmula de población sesgada (al dividir por *n*-1).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
VarP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 El **VarP** función devuelve la varianza sesgada de una expresión numérica especificada, evaluada sobre un conjunto especificado.  
  
 El **VarP** función usa la población sesgada fórmulas, mientras el [Var](../mdx/var-mdx.md) función utiliza la fórmula de población no sesgada.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
