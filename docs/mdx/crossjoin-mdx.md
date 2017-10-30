---
title: Crossjoin (MDX) | Documentos de Microsoft
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
- CROSSJOIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Crossjoin function
ms.assetid: 503b8376-d244-4855-8f44-a749764162e4
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f40d75ab7552728f578da2c90020a087348f6414
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el producto cruzado de uno o más conjuntos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **Crossjoin** función devuelve el producto cruzado de dos o más conjuntos especificados. El orden de las tuplas en el conjunto resultante depende del orden de los conjuntos que deben unirse y del orden de sus miembros. Por ejemplo, cuando el primer conjunto consta de {x1, x2,..., x*n*}, y el segundo conjunto consta de {y1, y2,..., y*n*}, el producto cruzado de estos conjuntos es:  
  
 {(x1, y1), (x1, y2),...,(x1, y*n*), (x2, y1), (x2, y2),...,  
  
 (x2, y*n*),..., (x*n*, y1), (x*n*, y2),..., (xn, y*n*)}  
  
> [!IMPORTANT]  
>  Si los conjuntos de la combinación cruzada están compuestos por tuplas de diferentes jerarquías de atributo de la misma dimensión, esta función solo devolverá aquellas tuplas que realmente existen. Para obtener más información, vea [conceptos clave de MDX &#40; Analysis Services &#41; ](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra ejemplos simples del uso de la función Crossjoin en los ejes de columnas y filas de una consulta:  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 En el ejemplo siguiente se muestra el filtrado automático que tiene lugar cuando las distintas jerarquías de una misma dimensión están unidas de forma cruzada:  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 Los tres ejemplos siguientes devuelven los mismos resultados (cifra de ventas por Internet por estado para los estados de Estados Unidos). Los dos primeros utilizan las dos sintaxis de combinación cruzada y el tercero muestra el uso de la cláusula WHERE para devolver la misma información.  
  
### <a name="example-1"></a>Ejemplo 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>Ejemplo 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>Ejemplo 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

