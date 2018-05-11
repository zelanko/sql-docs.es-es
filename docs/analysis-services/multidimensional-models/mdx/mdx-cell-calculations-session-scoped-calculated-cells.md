---
title: Crear ámbito de sesión celdas calculadas | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1681e8843686f0f5e2e4abf474a401733ce4396
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>Cálculos de celdas MDX - celdas calculadas de ámbito de sesión
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Para crear celdas calculadas disponibles para todas las consultas realizadas en la misma sesión, se pueden utilizar las instrucciones [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) o [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) . Ambas devuelven el mismo resultado.  
  
## <a name="create-cell-calculation-syntax"></a>Sintaxis de CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
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
>  Esta sintaxis ya no se utiliza. En su lugar debería utilizar asignaciones MDX. Para más información sobre asignaciones, vea [Script MDX básico &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
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
  
|Categoría|Description|  
|--------------|-----------------|  
|Conjunto vacío|Una expresión de conjunto MDX que se resuelve en un conjunto vacío. En este caso, el ámbito de la celda calculada es todo el cubo.|  
|Conjunto de un solo miembro|Una expresión de conjunto MDX que se resuelve en un solo miembro.|  
|Conjunto de miembros de nivel|Una expresión de conjunto MDX que se resuelve en miembros de un solo nivel. Un ejemplo de esto es la función MDX *Level_Expression*.**Members** . Para incluir miembros calculados, use la función MDX *Level_Expression*.**AllMembers**.<br /><br /> Para más información, vea [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Conjunto de descendientes|Una expresión de conjunto MDX que se resuelve en los descendientes de un miembro determinado. Un ejemplo de esto es la función MDX **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Para más información, vea [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
## <a name="see-also"></a>Vea también  
 [Generar cálculos de celdas en MDX & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
