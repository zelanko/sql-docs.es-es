---
title: (Sintaxis de MDX) de palabras clave reservadas | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f50b0292b9139dcbb2b3a5652ad41136b31702a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149868"
---
# <a name="reserved-keywords-mdx-syntax"></a>Palabras clave reservadas (sintaxis de MDX)


  Analysis Services reserva ciertas palabras clave para su uso exclusivo. Para obtener una lista de palabras clave reservadas, consulte [palabras reservadas de MDX](../mdx/mdx-reserved-words.md).  
  
 Las palabras clave reservadas deben seguir las siguientes directrices:  
  
-   No se pueden incluir palabras clave reservadas en instrucciones de expresiones multidimensionales (MDX) en ninguna ubicación, excepto las definidas en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Ningún objeto de la base de datos debe recibir un nombre que coincida con una palabra clave reservada. Si existe dicho nombre, siempre se debe hacer referencia al objeto mediante identificadores delimitados. Aunque este método permite utilizar nombres de objeto como palabras reservadas, debe evitarse el uso de palabras clave para denominar objetos.  
  
-   Use una convención de nomenclatura que evite la utilización de palabras clave reservadas. Si el nombre de un objeto debe parecerse a una palabra clave reservada, se pueden quitar las consonantes o vocales.  
  
## <a name="see-also"></a>Vea también  
 [Los elementos de sintaxis MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
