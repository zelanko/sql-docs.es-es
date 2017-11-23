---
title: Convenciones de sintaxis MDX (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], syntax
- MDX [Analysis Services], syntax
ms.assetid: 50a6e723-91c4-407b-a0d5-87d0d4e4e0f6
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1ea6c7ecf3ecebf9fcb29e11ef89e554b2a343f0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-syntax-conventions-mdx"></a>Convenciones de sintaxis de MDX (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Los diagramas de sintaxis de las Expresiones multidimensionales (MDX) del tema Lenguaje MDX utilizan estas convenciones.  
  
|Convención|Uso|  
|----------------|-----------|  
|*cursiva*|Indica argumentos proporcionados por el usuario de la sintaxis de MDX.|  
|&#124; (barra vertical)|Separa los elementos de sintaxis con corchetes o llaves. Solo se puede seleccionar uno de los elementos.|  
|`[ ]` (corchetes)|Indica los elementos de sintaxis opcionales. No escriba los corchetes.|  
|[,] ...n|Indica que el elemento anterior se puede repetir muchas veces. En algunos casos, los elementos se separan mediante comas.|  
|\<etiqueta >:: =|Indica el nombre de un bloque de sintaxis. Esta convención se utiliza para agrupar y asignar etiquetas a porciones de sintaxis largas o una unidad de sintaxis que se puede utilizar en más de un lugar dentro de una instrucción. Cada ubicación en la que se puede utilizar el bloque de sintaxis se indica con la etiqueta incluida entre corchetes angulares: \<etiqueta >.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  

