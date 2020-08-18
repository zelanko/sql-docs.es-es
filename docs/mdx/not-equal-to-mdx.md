---
description: '&lt;&gt; (No es igual a) MDX'
title: '&lt;&gt; (No es igual a) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8c2651c7d542ac0a8707c20e8b32f4ba33ac7b54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471797"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (No es igual a) MDX


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
  
-   **true** si ambos parámetros son no NULL y el primer parámetro no es igual que el segundo parámetro.  
  
-   es **false** si ambos parámetros son no NULL y el primer parámetro es igual que el segundo parámetro.  
  
-   valor NULL si uno de los parámetros (o ambos) se evalúa en un valor NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
