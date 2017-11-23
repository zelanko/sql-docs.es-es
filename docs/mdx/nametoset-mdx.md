---
title: NameToSet (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: NAMETOSET
dev_langs: kbMDX
helpviewer_keywords: NameToSet function
ms.assetid: e02e17d5-4309-49cb-84c7-5b445ac2bd94
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 37fc3b63539cb621d6d7162ca53b6c01b0717254
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto que contiene el miembro especificado por una cadena con formato de Expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Expresión de cadena válida que representa el nombre de un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Si el nombre del miembro especificado no existe, el **NameToSet** función devuelve un conjunto que contiene ese miembro. En caso contrario, la función devuelve un conjunto vacío.  
  
> [!NOTE]  
>  El nombre del miembro especificado solamente debe ser un nombre de miembro; no puede ser una expresión de miembro. Para usar una expresión de miembro, vea [StrToSet &#40; MDX &#41; ](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor de medida predeterminado para el nombre de miembro especificado.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
