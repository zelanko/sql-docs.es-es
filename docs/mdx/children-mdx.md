---
title: Elementos secundarios (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0af4d7b97777002dc5683c075f82531ccc8df86e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016797"
---
# <a name="children-mdx"></a>Children (MDX)


  Devuelve el conjunto de elementos secundarios de un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **Children** devuelve un conjunto ordenado de forma natural que contiene los elementos secundarios de un miembro especificado. Si el miembro especificado no tiene elementos secundarios, esta función devuelve un conjunto vacío.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve los elementos secundarios del miembro Estados Unidos de la jerarquía Geography de la dimensión Geography.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se devuelven todos los miembros de la dimensión **Measures** en el eje de columna, lo que incluye todos los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` jerarquía de atributo en el eje de filas del cubo **Adventure Works** .  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Release|Historial|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Contenido modificado:**<br /> -Sintaxis y argumentos actualizados para mejorar la claridad.<br /><br /> -Se han agregado ejemplos actualizados.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
