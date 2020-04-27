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
ms.openlocfilehash: 8b31b884e0f86bf2aebe4859cd1c7a441669e813
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905990"
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
  
## <a name="remarks"></a>Observaciones  
 La función **IsEmpty** devuelve **true** si la expresión evaluada es un valor de celda vacía. De lo contrario, esta función devuelve **false**.  
  
> [!NOTE]  
>  La propiedad predeterminada de un miembro es el valor del miembro.  
  
 La función **IsEmpty** es la única manera de probar de forma confiable una celda vacía porque el valor de la celda vacía tiene un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]significado especial en.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con valores vacíos](../mdx/working-with-empty-values.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
