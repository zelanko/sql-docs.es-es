---
title: "Operadores de concatenación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- concatenation operators [MDX]
ms.assetid: 9e4c181a-b71e-41ec-98a1-ec8b5b5103b1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ae299577ece2c712504631fb85eeac4499c4d4c7
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="concatenation-operators"></a>Operadores de concatenación
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40; La sintaxis de MDX &#41;](../mdx/operators-mdx-syntax.md)  
  
  

