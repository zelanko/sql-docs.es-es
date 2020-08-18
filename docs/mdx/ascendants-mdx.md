---
description: Ascendants (MDX)
title: Antecesores (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb485e2785facba4a47647f8a51548e0140b3efb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491471"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **antecesoras** devuelve todos los antecesores de un miembro del miembro en sí hasta la parte superior de la jerarquía del miembro; más concretamente, realiza un recorrido de postorden de la jerarquía para el miembro especificado y, a continuación, devuelve todos los miembros antecesores relacionados con el miembro, incluido él mismo, en un conjunto. Esto contrasta con la función [ancestor](../mdx/ancestor-mdx.md) , que devuelve un miembro antecesor específico, o antecesor, en un nivel específico.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el recuento de pedidos de distribuidor para el `[Sales Territory].[Northwest]` miembro y todos los antecesores de ese miembro del cubo **Adventure Works** . La función **antecesoras** crea el conjunto que incluye el `[Sales Territory].[Northwest]` miembro y sus antecesores para el eje Rows.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
