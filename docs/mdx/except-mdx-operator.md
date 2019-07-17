---
title: '- (Excepto) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139081"
---
# <a name="except-mdx-operator"></a>Salvo el operador (MDX)


  Realiza una operación de conjunto que devuelve la diferencia entre dos conjuntos y quita los miembros duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="return-value"></a>Valor devuelto  
 Un conjunto que contiene miembros que no comparten ambos parámetros especificados.  
  
## <a name="remarks"></a>Comentarios  
 El **- (excepto)** operador es funcionalmente equivalente a la [excepto](../mdx/except-mdx-function.md) función.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador:  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
