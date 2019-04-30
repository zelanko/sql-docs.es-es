---
title: Operadores unarios | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6704d9a2fad8b1b19d7757c0e6de40bfccdcc1f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287801"
---
# <a name="unary-operators"></a>Operadores unarios


  En las expresiones multidimensionales (MDX), los operadores unarios realizan una operación en un solo operando, como devolver el valor positivo o negativo de una expresión numérica.  
  
 MDX es compatible con los operadores unarios que se indican en la siguiente tabla.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[- (Negativo)](../mdx/negative-mdx.md)|Devuelve el valor negativo de una expresión numérica.|  
|[+ (Positivo)](../mdx/positive-mdx.md)|Devuelve el valor positivo de una expresión numérica.|  
  
 En el siguiente ejemplo se ilustra el uso de un operador unario para devolver el valor negativo de una medida:  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Además, MDX utiliza operadores unarios especiales para determinar la operación de agregación realizada por el [RollupChildren](../mdx/rollupchildren-mdx.md) función. Para obtener más información sobre estos operadores unarios especiales, consulte [agregar una agregación personalizada a una dimensión](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40;sintaxis de MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
