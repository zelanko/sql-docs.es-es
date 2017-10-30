---
title: Lag (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eedeae82c5b7566f0c59a6876fc6743c61794de0
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="lag-mdx"></a>Lag (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el miembro que se encuentra un número especificado de posiciones por delante de un miembro especificado en el nivel del miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Índice*  
 Expresión numérica válida que especifica el número de posiciones que se van a retrasar.  
  
## <a name="remarks"></a>Comentarios  
 Las posiciones de los miembros en un nivel se determinan por el orden natural de la jerarquía de atributo. La numeración de las posiciones tiene como base cero.  
  
 Si el retraso especificado es cero, el **Lag** función devuelve el propio miembro especificado.  
  
 Si el retraso especificado es negativo, el **Lag** función devuelve un miembro subsiguiente.  
  
 `Lag(1)`es equivalente a la [PrevMember](../mdx/prevmember-mdx.md) función. `Lag(-1)`es equivalente a la [NextMember](../mdx/nextmember-mdx.md) función.  
  
 El **Lag** función es similar a la [provocar](../mdx/lead-mdx.md) funcione, salvo que la **provocar** función busca en la dirección opuesta a la **Lag** función. Es decir, `Lag(n)` es equivalente a `Lead(-n)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor para diciembre de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor para marzo de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

