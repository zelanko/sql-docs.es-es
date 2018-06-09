---
title: Los elementos secundarios (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d61eb168b01e9b6d48c4c003ba28d0f977026906
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740104"
---
# <a name="children-mdx"></a>Children (MDX)


  Devuelve el conjunto de elementos secundarios de un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **elementos secundarios** función devuelve un conjunto ordenado de forma natural que contiene los elementos secundarios de un miembro especificado. Si el miembro especificado no tiene elementos secundarios, esta función devuelve un conjunto vacío.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve los elementos secundarios del miembro United States de la jerarquía Geography de la dimensión Geography.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve todos los miembros de la **medidas** dimensión en el eje de columna, esto incluye todos los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` atributo la jerarquía del eje de fila de la **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Versión|Historial|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Contenido modificado:**<br /> : Actualiza la sintaxis y los argumentos para mejorar la claridad.<br /><br /> : Agregado ejemplos actualizados.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
