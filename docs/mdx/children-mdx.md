---
title: Children (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03c96a1c90f7ca0a18bd49c371a2ec90582b38f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208782"
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
  
## <a name="remarks"></a>Comentarios  
 El **hijos** función devuelve un conjunto ordenado de forma natural que contiene los elementos secundarios de un miembro especificado. Si el miembro especificado no tiene elementos secundarios, esta función devuelve un conjunto vacío.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve los elementos secundarios del miembro United States de la jerarquía Geography de la dimensión Geography.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve todos los miembros de la **medidas** dimensión en el eje de columna, esto incluye todos los miembros calculados y el conjunto de todos los elementos secundarios de la `[Product].[Model Name]` jerarquía del eje de fila del atributo desde el **Adventure Works** cubo.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Versión|Historial|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Contenido modificado:**<br /> -Actualizar la sintaxis y los argumentos para mejorar la claridad.<br /><br /> -Se ha agregado ejemplos actualizados.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
