---
description: Operadores unarios
title: Operadores unarios | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32f5084190642bd4237d225404c92f0c4754da7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466477"
---
# <a name="unary-operators"></a>Operadores unarios


  En las expresiones multidimensionales (MDX), los operadores unarios realizan una operación en un solo operando, como devolver el valor positivo o negativo de una expresión numérica.  
  
 MDX es compatible con los operadores unarios que se indican en la siguiente tabla.  
  
|Operator|Descripción|  
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
  
 Además, MDX utiliza operadores unarios especiales para determinar la operación de agregación realizada por la función [RollupChildren](../mdx/rollupchildren-mdx.md) . Para obtener más información sobre estos operadores unarios especiales, vea [Agregar una agregación personalizada a una dimensión](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension).  
  
## <a name="see-also"></a>Consulte también  
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
