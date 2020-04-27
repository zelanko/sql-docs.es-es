---
title: Crear celdas calculadas de ámbito de sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4388ef278c0762184859162dc55f656aae1c9a15
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074426"
---
# <a name="creating-session-scoped-calculated-cells"></a>Crear celdas calculadas de ámbito de sesión
    
> [!IMPORTANT]  
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Para crear celdas calculadas disponibles para todas las consultas realizadas en la misma sesión, se pueden utilizar las instrucciones [CREATE CELL CALCULATION](/sql/mdx/mdx-data-definition-create-cell-calculation) o [ALTER CUBE](/sql/mdx/mdx-data-definition-alter-cube) . Ambas devuelven el mismo resultado.  
  
## <a name="create-cell-calculation-syntax"></a>Sintaxis de CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Utilice la siguiente sintaxis si desea definir una celda calculada de ámbito de sesión mediante la instrucción CREATE CELL CALCULATION:  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>Sintaxis de ALTER CUBE  
  
> [!IMPORTANT]  
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Utilice la siguiente sintaxis si desea definir una celda calculada de ámbito de sesión mediante la instrucción ALTER CUBE:  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 El valor `String_Expression` contiene una lista de expresiones de conjunto MDX ortogonales de una sola dimensión, cada una de las cuales debe resolverse en alguna de las siguientes categorías de conjuntos que se indican en la siguiente tabla.  
  
|Category|Descripción|  
|--------------|-----------------|  
|Conjunto vacío|Una expresión de conjunto MDX que se resuelve en un conjunto vacío. En este caso, el ámbito de la celda calculada es todo el cubo.|  
|Conjunto de un solo miembro|Una expresión de conjunto MDX que se resuelve en un solo miembro.|  
|Conjunto de miembros de nivel|Una expresión de conjunto MDX que se resuelve en miembros de un solo nivel. Un ejemplo de esto es el *Level_Expression*.`Members` Función MDX. Para incluir miembros calculados, use el *Level_Expression*.`AllMembers` Función MDX.<br /><br /> Para más información, vea [AllMembers &#40;MDX&#41;](/sql/mdx/allmembers-mdx).|  
|Conjunto de descendientes|Una expresión de conjunto MDX que se resuelve en los descendientes de un miembro determinado. Un ejemplo de esto es la `Descendants`función MDX (*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Para más información, vea [Descendants &#40;MDX&#41;](/sql/mdx/descendants-mdx).|  
  
## <a name="see-also"></a>Consulte también  
 [Generar cálculos de celdas en MDX &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
