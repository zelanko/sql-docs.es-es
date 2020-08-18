---
description: DataMember (MDX)
title: DataMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7291a8d2c57d4a996893146e8e855df234ed0139
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413141"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  Devuelve el miembro de datos generados por el sistema asociado a un miembro no hoja de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Esta función funciona en miembros no hoja de cualquier jerarquía y puede ser utilizada por el comando [Update Cube Statement (MDX)](../mdx/mdx-data-manipulation-update-cube.md) para reescribir los datos en un miembro no hoja directamente, en lugar de en los descendientes del miembro hoja.  
  
> [!NOTE]  
>  Devuelve el miembro especificado si es un miembro hoja o si el miembro no hoja no dispone de un miembro de datos asociado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la función **DataMember** en una medida calculada para mostrar la cuota de ventas de cada empleado individual:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Conceptos clave de MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
