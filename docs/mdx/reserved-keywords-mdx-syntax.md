---
title: (Sintaxis de MDX) de palabras clave reservadas | Documentos de Microsoft
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
- reserved words [MDX]
- Multidimensional Expressions [Analysis Services], reserved words
- MDX [Analysis Services], reserved words
ms.assetid: 0baab5fb-bd04-4ab3-b99a-9f91f3470fbb
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 986213edcc0e95c593e4bd9954b36cfbefca8be3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="reserved-keywords-mdx-syntax"></a>Palabras clave reservadas (sintaxis de MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] reserva ciertas palabras clave para su uso exclusivo. Para obtener una lista de palabras clave reservadas, consulte [palabras reservadas de MDX](../mdx/mdx-reserved-words.md).  
  
 Las palabras clave reservadas deben seguir las siguientes directrices:  
  
-   No se pueden incluir palabras clave reservadas en instrucciones de expresiones multidimensionales (MDX) en ninguna ubicación, excepto las definidas en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Ningún objeto de la base de datos debe recibir un nombre que coincida con una palabra clave reservada. Si existe dicho nombre, siempre se debe hacer referencia al objeto mediante identificadores delimitados. Aunque este método permite utilizar nombres de objeto como palabras reservadas, debe evitarse el uso de palabras clave para denominar objetos.  
  
-   Use una convención de nomenclatura que evite la utilización de palabras clave reservadas. Si el nombre de un objeto debe parecerse a una palabra clave reservada, se pueden quitar las consonantes o vocales.  
  
## <a name="see-also"></a>Vea también  
 [Elementos de sintaxis MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
