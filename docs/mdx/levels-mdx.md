---
description: Levels (MDX)
title: Niveles (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f3b0a7eaea166fdefbfd947faf95b58f74bdb8be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429877"
---
# <a name="levels-mdx"></a>Levels (MDX)


  Devuelve el nivel cuya posición en una dimensión o jerarquía se especifica mediante una expresión numérica, o cuyo nombre se especifica mediante una expresión de cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Level_Number*  
 Expresión numérica válida que especifica un número de nivel.  
  
 *Level_Name*  
 Expresión de cadena válida que especifica un nombre de nivel.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un número de nivel, la función **Levels** devuelve el nivel asociado a la posición basada en cero especificada.  
  
 Si se especifica un nombre de nivel, la función **Levels** devuelve el nivel especificado.  
  
> [!NOTE]  
>  Utilice la sintaxis de expresión de cadena para funciones definidas por el usuario.  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se ilustra cada una de las sintaxis de las funciones de **niveles** .  
  
### <a name="numeric"></a>Numérica  
 El ejemplo siguiente devuelve el nivel Country:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 El ejemplo siguiente devuelve el nivel Country:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
