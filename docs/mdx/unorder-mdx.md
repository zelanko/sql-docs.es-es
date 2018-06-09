---
title: Unorder, (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b5e360c8f15eafba2b4565ca41a557c9e1ceda9
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743454"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  Quita cualquier orden impuesto sobre un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Notas  
 El **Unorder** función quita cualquier ordenación impuesta en las tuplas contenidas en el conjunto por cualquier otra función o instrucción, como la [orden](../mdx/order-mdx.md) función. El orden de las tuplas en el conjunto devuelto por la **Unorder** función es indeterminada.  
  
 El **Unorder** función se utiliza como una sugerencia para optimizar la consulta para el procesamiento del conjunto. Si el orden de las tuplas de un conjunto no es relevante para una consulta o cálculo, usando la **Unorder** función puede proporcionar una mejora del rendimiento en casos como este. Por ejemplo, el [NonEmpty (MDX)](../mdx/nonempty-mdx.md) función puede funcionar mejor cuando el conjunto especificado a esta función está ordenado que si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tiene que conservar el orden, aunque con [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], el procesador de consultas intenta realizar esta función automáticamente para muchas funciones, como **suma** y **agregado**. La ventaja de rendimiento de usar **Unorder** es probable que sea notable en conjuntos muy grandes que consta de millones de tuplas.  
  
## <a name="example"></a>Ejemplo  
 El siguiente pseudocódigo muestra la sintaxis de esta función.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
