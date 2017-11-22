---
title: "Instrucción CREATE CELL CALCULATION (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CELL CALCULATION
- CREATE
- CALCULATION
- CELL
- CREATE_CELL_CALCULATION
- CREATE CELL
- CREATE CELL CALCULATION
dev_langs: kbMDX
helpviewer_keywords:
- calculations [Analysis Services], creating
- CREATE CELL CALCULATION statement
- cubes [Analysis Services], calculations
ms.assetid: 01ced1b3-ada1-4b55-b350-e4255c3cc679
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6ad2921ddea1c822c7b83ef38c43bbd771320e21
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-cell-calculation"></a>Definición de datos MDX - crear el cálculo de celda
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un cálculo que evalúa una expresión multidimensional (MDX) en un conjunto especificado de tuplas en un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Cadena válida que proporciona un nombre de cubo.  
  
 *Calculation_Name*  
 Cadena válida que proporciona un nombre de cálculo de celda.  
  
 *Set_Expression*  
 Expresión MDX válida que devuelve un conjunto.  
  
 *String*  
 Valor de cadena válido.  
  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
 *Filter*  
 Una expresión lógica de MDX válida.  
  
 *Integer*  
 Valor de entero válido.  
  
 *Calculation_Name*  
 Cadena válida que proporciona el nombre de una propiedad de cálculo de celda.  
  
 *Scalar_Expression*  
 Una expresión escalar de MDX válida.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el uso de celdas calculadas, la aplicación cliente puede especificar un valor de resumen para un conjunto concreto de celdas, en lugar de hacerlo para un conjunto completo de celdas en el caso de una fórmula de resumen personalizada o un miembro calculado. Por ejemplo, es posible especificar que cualquier celda del conjunto definida por `{[Canada],[Time].[2000]}` pueda contener un valor definido por una fórmula. El resto de celdas no contenidas en este conjunto se calculan normalmente.  
  
> [!NOTE]  
>  La forma de Backus-Naur (BNF) de `{*(<comment> | <whitespace> | <newline>)}` se analizará como `{*}` para la compatibilidad con versiones anteriores.  
  
## <a name="see-also"></a>Vea también  
 [Crear celdas calculadas de ámbito de sesión](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)   
 [Creación de cálculos de celdas del ámbito de consulta &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Generar cálculos de celdas en MDX &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)   
 [Mediante las propiedades de celda &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [FORMAT_STRING, contenido &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [FORE_COLOR y BACK_COLOR, contenido &#40; MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)   
 [Instrucciones de definición de datos MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
