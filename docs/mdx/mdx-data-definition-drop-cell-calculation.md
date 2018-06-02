---
title: Instrucción DROP CELL CALCULATION (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac37584d12f2efa68084ada626ba57ab9fb28155
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579317"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Definición de datos MDX - DROP CELL CALCULATION
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quita el cálculo de celda especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Expresión de cadena válida que proporciona el nombre de una expresión de cubo.  
  
 *CellCalc_Name*  
 Expresión de cadena válida que proporciona el nombre del cálculo de celda que se va a quitar.  
  
## <a name="see-also"></a>Vea también  
 [Instrucción CREATE CELL CALCULATION &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
