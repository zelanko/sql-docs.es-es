---
title: Los elementos secundarios (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CHILDREN
dev_langs: kbMDX
helpviewer_keywords: Children function
ms.assetid: ce2c3069-914c-44a3-8a4c-5cbd4fb71e4c
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8a818777528583214a948a5fefd7d9c78896fc79
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="children-mdx"></a>Children (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el conjunto de elementos secundarios de un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
