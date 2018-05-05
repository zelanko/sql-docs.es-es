---
title: Union (MDX) | Documentos de Microsoft
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
dev_langs:
- kbMDX
helpviewer_keywords:
- functions [MDX], Union
ms.assetid: cc083455-8b3b-46af-bb55-1e238376f162
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 03daa8edf505d816435a3e10a71f687895574823
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Comentarios  
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
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
