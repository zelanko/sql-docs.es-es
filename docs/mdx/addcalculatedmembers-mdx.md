---
title: AddCalculatedMembers (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18ccf4ad808c15945d82f1ca05616f0da878a7ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201617"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)


  Devuelve un conjunto generado al agregar miembros calculados a un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, MDX excluye los miembros calculados cuando resuelve funciones de conjunto. El **AddCalculatedMembers** función examina la expresión de conjunto especificada en *expresión_conjunto,* e incluye miembros calculados que están relacionados con los miembros incluidos dentro del ámbito de ese conjunto expresión.  
  
> [!NOTE]  
>  Esta función puede utilizarse solo con expresiones de conjunto de una dimensión.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de esta función.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 El ejemplo siguiente devuelve el `Measures.[Unit Price]` miembro, además de todos los miembros calculados en el **medidas** dimensión, desde el **Adventure Works** cubo.  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
