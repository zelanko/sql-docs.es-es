---
title: Union (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7712e1f925aa514ec059a88d46db05d337f0c140
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582237"
---
# <a name="union--mdx"></a>Union (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un conjunto generado por la unión de dos conjuntos que, opcionalmente, conserva miembros duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión de conjunto 1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Expresión de conjunto 2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Notas  
 Esta función devuelve la unión de dos o más conjuntos especificados *.* Con la sintaxis estándar y con la sintaxis alternativa 1, los duplicados se eliminan de forma predeterminada. Con la sintaxis estándar, con el **todos los** marca mantiene los duplicados en el conjunto combinado. Se eliminan los duplicados de la cola del conjunto. Con la sintaxis alternativa 2, siempre se conservan los duplicados.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran el comportamiento de la **unión** funcionar con cada sintaxis.  
  
### <a name="standard-syntax-duplicates-eliminated"></a>Sintaxis estándar, eliminación de duplicados  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>Sintaxis estándar, conservación de duplicados  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>Sintaxis alternativa 1, eliminación de duplicados  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>Sintaxis alternativa 2, conservación de duplicados  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [+ &#40;Unión&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
