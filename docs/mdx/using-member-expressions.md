---
title: Uso de expresiones de miembro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41ff63d47a62b9b83fb583c55ff2405638de22cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097111"
---
# <a name="using-member-expressions"></a>Usar expresiones de miembro


  Una expresión de miembro contiene un identificador de miembro, una función de miembro o una expresión que puede convertirse en un miembro.  
  
 Los identificadores de miembro pueden presentarse en muchos formatos diferentes. El formato más simple de un identificador de miembro consiste en el nombre del miembro. Por ejemplo:  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 Sin embargo, si hay varios miembros con el mismo nombre en diferentes jerarquías, no hay ningún método para determinar qué miembro devolverá la consulta. Por ejemplo, la consulta siguiente solicita los datos de un miembro con el nombre [CY 2004]. La consulta se ejecuta correctamente, pero hay por lo menos seis miembros con ese nombre en el cubo Adventure Works:  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 Por consiguiente, el formato más confiable de identificador de miembro es el nombre único del miembro, que garantiza la identificación de un miembro específico de un cubo. Analysis Services pueden generar nombres únicos de varias maneras, pero un nombre único siempre se compone de al menos dos identificadores: el nombre de la dimensión y el nombre del miembro o la clave del miembro. Un nombre único tiene el siguiente formato:  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 A continuación se muestran algunos ejemplos de nombres únicos de miembro del cubo Adventure Works:  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 Existen muchas funciones MDX que devuelven miembros. Para obtener una lista completa, consulte [referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  Para obtener más información acerca de los nombres de miembro y las claves de miembro, vea [trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>Vea también  
 [Las expresiones &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
