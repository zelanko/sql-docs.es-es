---
title: Ascendants (MDX) | Documentos de Microsoft
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
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a290643abeb55db3a2c7091976731af9dbb200ff
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **antecesores** función devuelve todos los antecesores de un miembro desde el propio miembro hasta la parte superior de la jerarquía del miembro; más específicamente, realiza un recorrido transversal posterior a la de la jerarquía para el miembro especificado y, a continuación, devuelve todos los miembros antecesores relacionados con el miembro, incluido él mismo, en un conjunto. Se trata de diferencia el [antecesor](../mdx/ancestor-mdx.md) función, que devuelve un miembro antecesor específico, o antecesor, en un nivel específico.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el número de pedidos de distribuidores el `[Sales Territory].[Northwest]` miembro y todos los antecesores de ese miembro de la **Adventure Works** cubo. El **antecesores** función crea el conjunto que incluye el `[Sales Territory].[Northwest]` miembro y sus antecesores para el eje de filas.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

