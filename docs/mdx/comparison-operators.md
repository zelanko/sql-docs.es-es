---
title: Operadores de comparación | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001514"
---
# <a name="comparison-operators"></a>Operadores de comparación


  Los operadores de comparación se pueden usar con los datos escalares. Por su parte, los operadores de comparación se pueden usar en cualquier expresión MDX.  
  
 Para comprobar una condición, también puede usar operadores de comparación en instrucciones y funciones MDX, como la función [IIf](../mdx/iif-mdx.md) de MDX. Sin embargo, si se utilizan operadores de comparación para comprobar una condición, asegúrese de que dispone de los permisos necesarios antes de intentar cambiar los datos basados en esa condición. Cualquiera que tenga acceso a los datos reales y pueda realizar consultas de ellos, puede utilizar los operadores de comparación en consultas adicionales. Sin embargo, el acceso no implica que esos usuarios tengan o deban tener los permisos necesarios para cambiar los datos. Además, para mantener la integridad de los datos, limite el número de personas que puedan realizar consultas de los datos y cambiarlos.  
  
 Los operadores de comparación dan se evalúan como un tipo de datos booleano y devuelven TRUE o FALSE según el resultado de la condición probada.  
  
 MDX es compatible con los operadores de comparación que se indican en la siguiente tabla.  
  
|Operator|Descripción|  
|--------------|-----------------|  
|[= (Igual a)](../mdx/equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si alguno de los argumentos, o ambos, se evalúan como un valor NULL, el operador devuelve un valor NULL, salvo si se efectúa la comparación `0=null`, en cuyo caso el valor booleano contiene TRUE.|  
|[<>  (no es igual a)](../mdx/not-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es distinto del derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[> (mayor que)](../mdx/greater-than-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[>= (mayor o igual que)](../mdx/greater-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[< (menor que)](../mdx/less-than-mdx.md)|Para los argumentos que no son NULL, devuelve TRUE si el argumento izquierdo tiene un valor que es menor que el argumento derecho. en caso contrario, FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[<= (menor o igual que)](../mdx/less-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor inferior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
