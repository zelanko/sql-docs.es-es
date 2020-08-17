---
description: + (Concatenación de cadenas) MDX
title: + (Concatenación de cadenas) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e92751cb709a93d3d5d8d05ac76361c22bee5fa7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386871"
---
# <a name="-string-concatenation-mdx"></a>+ (Concatenación de cadenas) (MDX)


  Realiza una operación de cadena que concatena dos o más cadenas de caracteres, tuplas o una combinación de cadenas y tuplas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *String_Expression*  
 Una expresión multidimensional (MDX) válida que devuelve un valor de cadena.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor con el tipo de datos del parámetro que tiene mayor precedencia.  
  
## <a name="remarks"></a>Observaciones  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si una expresión se evalúa como un valor NULL, el operador devuelve el resultado de la otra expresión.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
