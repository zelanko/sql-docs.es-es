---
title: Operadores de concatenación | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8eacfc08fdeb0f92874758d0f95e5cde3e6b295a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739404"
---
# <a name="concatenation-operators"></a>Operadores de concatenación


  El operador de concatenación es el signo más (+). Puede combinar, o concatenar, dos o más cadenas de caracteres en una única cadena. También puede concatenar cadenas binarias.  
  
 El siguiente código es un ejemplo de un operador de concatenación que combina el nombre del producto con el nombre único del producto:  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>Consideraciones de idioma  
 Cuando las cadenas que se utilizan en la concatenación tienen la misma intercalación, la cadena resultante tiene la misma intercalación que las entradas. Cuando las cadenas usadas en una concatenación tienen distintas intercalaciones, las reglas de prioridad de intercalación determinan la intercalación de la cadena concatenada resultante. Para más información, vea [Idiomas e intercalaciones &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
