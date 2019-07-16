---
title: '&lt;&gt; (No es igual a) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088317"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (No es igual a) (MDX)


  Realiza una operación de comparación que determina si el valor de una expresión multidimensional (MDX) no es igual al valor de otra expresión MDX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano basado en las condiciones siguientes:  
  
-   **True** si ambos parámetros son no null y el primer parámetro no es igual que el segundo parámetro.  
  
-   **false** si ambos parámetros son no null y el primer parámetro es igual que el segundo parámetro.  
  
-   valor NULL si uno de los parámetros (o ambos) se evalúa en un valor NULL.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
