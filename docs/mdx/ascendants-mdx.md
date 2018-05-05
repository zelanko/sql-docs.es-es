---
title: Ascendants (MDX) | Documentos de Microsoft
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
ms.openlocfilehash: df35665a82149bd133e4116d97cb739d70865ac7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
