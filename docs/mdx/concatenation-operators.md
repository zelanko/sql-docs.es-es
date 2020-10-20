---
description: Operadores de concatenación
title: Operadores de concatenación | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b53f5d79124a86e8748a473af5b371152932514e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192560"
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
 Cuando las cadenas que se utilizan en la concatenación tienen la misma intercalación, la cadena resultante tiene la misma intercalación que las entradas. Cuando las cadenas usadas en una concatenación tienen distintas intercalaciones, las reglas de prioridad de intercalación determinan la intercalación de la cadena concatenada resultante. Para más información, vea [Idiomas e intercalaciones &#40;Analysis Services&#41;](/analysis-services/languages-and-collations-analysis-services).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
