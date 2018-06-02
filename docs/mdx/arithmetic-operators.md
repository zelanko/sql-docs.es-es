---
title: Operadores aritméticos | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4bf4a182c73acb18d649de3888f735f8842964dc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576957"
---
# <a name="arithmetic-operators"></a>Operadores aritméticos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
