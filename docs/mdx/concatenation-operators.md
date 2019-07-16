---
title: Operadores de concatenación | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 235320a65bf04e8b0ce1d7c23da588a4d541a0b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915861"
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
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis de MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
