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
manager: kfile
ms.openlocfilehash: ae175665c2a62caa2d3b7b845c68fefebcfd4c32
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "49071667"
---
# <a name="comparison-operators"></a>Operadores de comparación


  Los operadores de comparación se pueden usar con los datos escalares. Por su parte, los operadores de comparación se pueden usar en cualquier expresión MDX.  
  
 Para comprobar una condición, también puede usar los operadores de comparación en instrucciones MDX y funciones, como el MDX [IIf](../mdx/iif-mdx.md) función. Sin embargo, si se utilizan operadores de comparación para comprobar una condición, asegúrese de que dispone de los permisos necesarios antes de intentar cambiar los datos basados en esa condición. Cualquiera que tenga acceso a los datos reales y pueda realizar consultas de ellos, puede utilizar los operadores de comparación en consultas adicionales. Sin embargo, el acceso no implica que esos usuarios tengan o deban tener los permisos necesarios para cambiar los datos. Además, para mantener la integridad de los datos, limite el número de personas que puedan realizar consultas de los datos y cambiarlos.  
  
 Los operadores de comparación dan se evalúan como un tipo de datos booleano y devuelven TRUE o FALSE según el resultado de la condición probada.  
  
 MDX es compatible con los operadores de comparación que se indican en la siguiente tabla.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[= (Igual a)](../mdx/equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si alguno de los argumentos, o ambos, se evalúan como un valor NULL, el operador devuelve un valor NULL, salvo si se efectúa la comparación `0=null`, en cuyo caso el valor booleano contiene TRUE.|  
|[<> (No es igual a)](../mdx/not-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es distinto del derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[> (Mayor que)](../mdx/greater-than-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[>= (Mayor o igual a)](../mdx/greater-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[< (Menor que)](../mdx/less-than-mdx.md)|Para argumentos distintos de null, devuelve TRUE si el argumento izquierdo tiene un valor que es menor que el argumento derecho; en caso contrario, FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[<= (Menor o igual a)](../mdx/less-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor inferior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis de MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
