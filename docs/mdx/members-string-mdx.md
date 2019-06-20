---
title: Members (cadena) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 302445cadc829de35eca28db2888aaa01673ca75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048459"
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
  
## <a name="remarks"></a>Comentarios  
 El **Members (cadena)** función devuelve un único miembro cuyo nombre se especifica. Normalmente, se usa el **Members (cadena)** función con funciones externas, que proporciona a los **Members (cadena)** funcionar una cadena que identifica un miembro, y el **Members (cadena)**  función devuelve el valor de este miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el **Members (cadena)** función para convertir la cadena especificada en un miembro válido y, a continuación, devuelve la medida predeterminada para el miembro especificado en la cadena. La cadena se especifica entre comillas simples. La medida predeterminada es la medida Reseller Sales Amount.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
