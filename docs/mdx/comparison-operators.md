---
title: Operadores de comparación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- comparison operators [MDX]
ms.assetid: 4a4bbc76-c6a2-4b19-ae75-6ac3ac14df01
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5a2ba472fe36b0b7a1415793c97f3b577adcb0e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="comparison-operators"></a>Operadores de comparación
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los operadores de comparación se pueden usar con los datos escalares. Por su parte, los operadores de comparación se pueden usar en cualquier expresión MDX.  
  
 Para comprobar una condición, también puede utilizar operadores de comparación en instrucciones MDX y funciones, como el código MDX [IIf](../mdx/iif-mdx.md) función. Sin embargo, si se utilizan operadores de comparación para comprobar una condición, asegúrese de que dispone de los permisos necesarios antes de intentar cambiar los datos basados en esa condición. Cualquiera que tenga acceso a los datos reales y pueda realizar consultas de ellos, puede utilizar los operadores de comparación en consultas adicionales. Sin embargo, el acceso no implica que esos usuarios tengan o deban tener los permisos necesarios para cambiar los datos. Además, para mantener la integridad de los datos, limite el número de personas que puedan realizar consultas de los datos y cambiarlos.  
  
 Los operadores de comparación dan se evalúan como un tipo de datos booleano y devuelven TRUE o FALSE según el resultado de la condición probada.  
  
 MDX es compatible con los operadores de comparación que se indican en la siguiente tabla.  
  
|Operador|Description|  
|--------------|-----------------|  
|[= (Igual a)](../mdx/equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si alguno de los argumentos, o ambos, se evalúan como un valor NULL, el operador devuelve un valor NULL, salvo si se efectúa la comparación `0=null`, en cuyo caso el valor booleano contiene TRUE.|  
|[<> (No es igual a)](../mdx/not-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo es distinto del derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[> (Mayor que)](../mdx/greater-than-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[>= (Mayor o igual a)](../mdx/greater-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor superior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[< (Menor que)](../mdx/less-than-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor inferior al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
|[<= (Menor o igual a)](../mdx/less-than-or-equal-to-mdx.md)|Para argumentos que no tengan un valor NULL, devuelve TRUE si el argumento izquierdo tiene un valor inferior o igual al derecho; de lo contrario, devuelve FALSE.<br /><br /> Si un argumento o ambos se evalúan como un valor NULL, el operador devuelve un valor NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
