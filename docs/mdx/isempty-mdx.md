---
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dbed0eba3fec73d7134b1ce21275c28dbd387fcd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224961"
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)


  Informa de si la expresión evaluada es el valor de celda vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Value_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que normalmente devuelve las coordenadas de celda de un miembro o una tupla.  
  
## <a name="remarks"></a>Comentarios  
 El **IsEmpty** función devuelve **true** si la expresión evaluada es un valor de celda vacía. En caso contrario, esta función devuelve **false**.  
  
> [!NOTE]  
>  La propiedad predeterminada de un miembro es el valor del miembro.  
  
 El **IsEmpty** función es la única manera confiable de comprobar si una celda vacía porque el valor de celda vacía tiene un significado especial en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Si la evaluación de la expresión de valor devuelve un error, la función devolverá **false**. Una expresión de valor puede devolver un error, por ejemplo, si una referencia de propiedad hace referencia a una propiedad no válida o inexistente.  
  
 Para obtener más información acerca de las celdas vacías, consulte la documentación de OLE DB.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo devuelve TRUE si Internet Sales Amount para el miembro actual en la jerarquía Fiscal de la dimensión Date devuelve una celda vacía:  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con valores vacíos](../mdx/working-with-empty-values.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
