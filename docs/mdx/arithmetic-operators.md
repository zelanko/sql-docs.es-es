---
title: Operadores aritméticos | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c422df08152eaf9266a6ca3408bfce12e023c2a3
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739464"
---
# <a name="arithmetic-operators"></a>Operadores aritméticos


  Puede utilizar operadores aritméticos en expresiones multidimensionales (DMX) para realizar cálculos aritméticos, incluida la suma, la resta, la multiplicación y la división.  
  
 MDX es compatible con los operadores aritméticos que se indican en la siguiente tabla.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[+ (Sumar)](../mdx/add-mdx.md)|Suma dos números.|  
|[/ (Dividir)](../mdx/divide-mdx-operator-reference.md)|Divide un número entre otro.|  
|[* (Multiplicar)](../mdx/multiply-mdx.md)|Multiplica dos números.|  
|[- (Restar)](../mdx/subtract-mdx.md)|Resta dos números.|  
|^ (Elevar a una potencia)|Eleva un número a otro.|  
  
> [!NOTE]  
>  MDX no incluye una función para obtener la raíz cuadrada de un número. Para obtener la raíz cuadrada de un número, elévelo a la potencia 0,5 utilizando el operador ^.  
  
## <a name="order-of-precedence"></a>Orden de precedencia  
 Las siguientes reglas determinan el orden de precedencia para operadores aritméticos en una expresión MDX:  
  
-   Cuando hay más de un operador aritmético en una expresión, MDX realiza primero las multiplicaciones y divisiones y, después, las restas y las sumas.  
  
-   Si todos los operadores aritméticos de una expresión tienen la misma precedencia, el orden de ejecución es de izquierda a derecha.  
  
-   Las expresiones entre paréntesis tienen precedencia sobre el resto de las operaciones.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
