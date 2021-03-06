---
description: NameToSet (MDX)
title: NameToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd1de5e8c126d9457fda2c7c9545dedea26fd1f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483758"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  Devuelve un conjunto que contiene el miembro especificado por una cadena con formato de expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Expresión de cadena válida que representa el nombre de un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Si el nombre del miembro especificado existe, la función **NameToSet** devuelve un conjunto que contiene ese miembro. En caso contrario, la función devuelve un conjunto vacío.  
  
> [!NOTE]  
>  El nombre del miembro especificado solamente debe ser un nombre de miembro; no puede ser una expresión de miembro. Para usar una expresión de miembro, consulte [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor de medida predeterminado para el nombre de miembro especificado.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
