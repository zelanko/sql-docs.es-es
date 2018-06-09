---
title: '* (Multiplicar) (MDX) | Documentos de Microsoft'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f752aec0a2e1b49fbf1145129876d2f8c5901ed
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742274"
---
# <a name="-multiply-mdx"></a>* (Multiplicar) (MDX)


  Realiza una operación aritmética que multiplica dos números.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Numeric_expression*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor con el tipo de datos del parámetro que tiene mayor precedencia.  
  
## <a name="remarks"></a>Notas  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si una expresión se evalúa como un valor NULL, el operador devuelve un valor NULL.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
