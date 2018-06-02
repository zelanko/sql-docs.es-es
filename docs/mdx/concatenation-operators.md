---
title: Operadores de concatenación | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a59ba79a2ba6cde723b79bb459734e7a8b5d752a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578437"
---
# <a name="concatenation-operators"></a>Operadores de concatenación
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
