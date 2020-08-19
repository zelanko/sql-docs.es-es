---
description: Members (String) (MDX)
title: Members (cadena) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 95e90f488f4b9182fc237045b570bc9da02f47e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483828"
---
# <a name="members-string-mdx"></a>Members (String) (MDX)


  Devuelve un miembro especificado por una expresión de cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Expresión de cadena válida que especifica un nombre de miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **Members (String)** devuelve un único miembro cuyo nombre se especifica. Normalmente, se usa la función **Members (String)** con funciones externas, lo que proporciona a la función **Members (String)** una cadena que identifica un miembro, y la función **Members (String)** devuelve el valor de este miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la función **Members (String)** para convertir la cadena especificada en un miembro válido y, a continuación, se devuelve la medida predeterminada para el miembro especificado en la cadena. La cadena se especifica entre comillas simples. La medida predeterminada es la medida Reseller Sales Amount.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
