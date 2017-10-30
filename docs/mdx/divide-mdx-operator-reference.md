---
title: "(División) (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /
dev_langs:
- kbMDX
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 42b7d3ea-234d-41b3-a849-f457be6d7972
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c980a9505ab69cd521edf5e72d3cd99028b4070b
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="divide---mdx-operator-reference"></a>División - referencia de operadores MDX
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una operación aritmética que divide un número por otro número.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Dividendo*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 *Divisor*  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor con el tipo de datos del parámetro que tiene mayor precedencia.  
  
## <a name="remarks"></a>Comentarios  
 El valor real devuelto por la **/ (dividir)** operador representa el cociente de la primera expresión, dividida por la segunda expresión.  
  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si *Divisor* se evalúa como un valor null, el operador genera un error. Si ambos *Divisor* y *dividendo* evaluar en un valor null, el operador devuelve un valor null.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This query returns the freight cost per user,  
-- for products, averaged by month.   
With Member [Measures].[Freight Per Customer] as  
    [Measures].[Internet Freight Cost]  
    /   
    [Measures].[Customer Count]  
  
SELECT   
    [Ship Date].[Calendar].[Calendar Year] Members ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
 Al dividir un valor distinto de cero o no NULL entre cero o NULL, devolverá el valor Infinity, que se muestra en los resultados de la consulta como el valor "1.#INF". En la mayoría de los casos, debe comprobar la división entre cero para evitar esta situación. En el siguiente ejemplo se muestra lo siguiente:  
  
 `//Returns 1.#INF when Internet Sales Amount is zero or null`  
  
 `Member [Measures].[Reseller to Internet Ratio] AS`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `//Traps the division by zero scenario and returns null instead of 1.#INF`  
  
 `Member [Measures].[Reseller to Internet Ratio With Error Handling] AS`  
  
 `IIF([Measures].[Internet Sales Amount]=0, NULL,`  
  
 `[Measures].[Reseller Sales Amount]`  
  
 `/`  
  
 `[Measures].[Internet Sales Amount])`  
  
 `SELECT`  
  
 `{[Measures].[Reseller to Internet Ratio],[Measures].[Reseller to Internet Ratio With Error Handling]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
## <a name="see-also"></a>Vea también  
 [IIf &#40; MDX &#41;](../mdx/iif-mdx.md)   
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

