---
description: '- Afectar MDX'
title: '- Afectar (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8550e75d4f0807263678fc7badec8c8a0be52cfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483746"
---
# <a name="--negative-mdx"></a>- (Negativo) (MDX)


  Realiza una operación unaria que devuelve el valor negativo de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
- Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Numeric_Expression*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor negativo con el tipo de datos del parámetro especificado.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This member creates a negative version of the  
-- Reseller Freight Cost.  
WITH MEMBER   
   Measures.[Resell Cost as Negative]   
   AS -Measures.[Reseller Freight Cost]  
SELECT   
   [Date].[Calendar Month of Year].Children ON COLUMNS,  
   [Product].[Product Categories].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    {[Measures].[Resell Cost as Negative]}  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
