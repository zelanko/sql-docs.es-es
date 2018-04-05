---
title: IsEmpty (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ISEMPTY
dev_langs:
- kbMDX
helpviewer_keywords:
- IsEmpty function
ms.assetid: b4a50996-61d1-4e23-8003-7d530195ea72
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 6f6d53545c505b32f9c9d045f07260cb23514641
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 El **IsEmpty** función es la única manera confiable de comprobar si una celda vacía porque el valor de celda vacía tiene un significado especial en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
