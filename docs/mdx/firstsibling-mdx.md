---
title: FirstSibling (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FIRSTSIBLING
dev_langs:
- kbMDX
helpviewer_keywords:
- FirstSibling function
ms.assetid: ed2fbd36-6665-4445-a894-cbeca29584ab
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0f3394960d9056dce0139daeeef736428d406705
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el primer elemento secundario del elemento primario de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
### <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve el primer miembro del mismo nivel que el año fiscal 2003 de la jerarquía Fiscal, que es el año fiscal 2002.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
