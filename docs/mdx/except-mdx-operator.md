---
title: '- (Excepto) (MDX) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '-'
dev_langs:
- kbMDX
helpviewer_keywords:
- Except operator [MDX]
- '- (except operator)'
ms.assetid: 8971a09d-b254-4c4c-a099-103664783589
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d06de38c64dda440d04d49c498653bcb52f8c6fa
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="except-mdx-operator"></a>Excepto operador (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 El **- (excepto)** operador es funcionalmente equivalente a la [excepto](../mdx/except-mdx-function.md) (función).  
  
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
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

