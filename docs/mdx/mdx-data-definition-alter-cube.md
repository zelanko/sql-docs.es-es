---
title: "ALTER CUBE (instrucción, MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- ALTER_CUBE
- ALTER CUBE
- ALTER
dev_langs:
- kbMDX
helpviewer_keywords:
- ALTER CUBE statement
- cubes [Analysis Services], modifying
- modifying cubes
ms.assetid: 2f0af61b-f509-4e1a-990f-20a215d22994
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e20832dac862a4a4973c4350c64efdd23a35b461
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---alter-cube"></a>Definición de datos MDX - ALTER CUBE
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera la estructura de un cubo especificado, que normalmente se usa para admitir la reescritura en la dimensión. Para obtener más información acerca del uso de reescritura en una aplicación, consulte esta entrada de blog: [compilar una aplicación de reescritura con Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977)  
  
 Tenga en cuenta que las reescrituras en dimensiones simultáneas pueden producir un interbloqueo, donde la primera reescritura no se puede confirmar debido al bloqueo compartido que mantiene la segunda reescritura. En esta situación no se genera ningún error, pero ninguna de las operaciones puede progresar. Al final, ambas operaciones agotan el tiempo de espera y se revierten los cambios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>Crear un miembro de dimensión  
 Se agrega una nueva fila a la tabla de dimensiones subyacente.  
  
### <a name="arguments"></a>Argumentos  
 *ParentName*  
 Expresión de cadena válida que proporciona el nombre del nivel primario del nuevo miembro de dimensión, a menos que el miembro de dimensión se cree en la raíz.  
  
 *Nombre de usuario registrado*  
 Expresión de cadena válida que proporciona un nombre de miembro.  
  
 *Key_Value*  
 Expresión escalar válida que define el valor de clave del nuevo miembro de dimensión.  
  
 *Property_name*  
 Identificador de expresión MDX válido que representa una propiedad de miembro.  
  
 *Property_Value*  
 Expresión MDX válida que define el valor de la propiedad de miembro calculado.  
  
## <a name="dropping-a-dimension-member"></a>Quitar un miembro de dimensión  
 Al quitar un miembro de dimensión de una dimensión habilitada para escritura se elimina dicho miembro y su fila correspondiente de la tabla de dimensiones subyacente.  
  
### <a name="arguments"></a>Argumentos  
 *Restricciones obligatorias Cube_Name*  
 Una expresión de cadena válida que proporciona un nombre de cubo.  
  
 *Member_Name*  
 Expresión de cadena válida que proporciona un nombre de miembro o una clave de miembro.  
  
### <a name="remarks"></a>Comentarios  
 Si no se utiliza la cláusula WITH DESCENDANTS, los elementos secundarios de un miembro quitado se convierten en elementos secundarios del elemento primario del miembro quitado. Si se utiliza la cláusula WITH DESCENDANTS, también se quitan todos los descendientes y sus filas de la tabla de dimensiones.  
  
> [!NOTE]  
>  Para obtener información acerca de cómo quitar miembros calculados, conjuntos con nombre, acciones y cálculos de celdas, vea [DROP MEMBER, instrucción &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-member.md), [Eliminar instrucción SET &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-set.md), [Eliminar acción instrucción &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-action.md), y [DROP CELL CALCULATION instrucción &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>Actualizar el miembro de dimensión predeterminado  
 Esta cláusula actualiza el miembro predeterminado de un cubo y se utiliza en el script de cálculo MDX para definir un miembro predeterminado. El miembro predeterminado puede especificarse para la dimensión de base de datos, una dimensión de cubo o para un inicio de sesión de usuario. Además, se puede cambiar el miembro predeterminado durante una sesión.  
  
### <a name="arguments"></a>Argumentos  
 *Dimension_Name*  
 Cadena válida que proporciona el nombre de una dimensión.  
  
 *MDX_Expression*  
 Expresión MDX válida que devuelve un miembro único.  
  
### <a name="remarks"></a>Comentarios  
 La expresión MDX especificada puede ser estática o dinámica.  
  
## <a name="moving-a-dimension-member"></a>Mover un miembro de dimensión  
 Una fila se modifica en la tabla de dimensiones subyacente.  
  
### <a name="arguments"></a>Argumentos  
 *ParentName*  
 Expresión de cadena válida que proporciona el nombre del nuevo elemento primario del miembro de dimensión que se está moviendo.  
  
 *Nombre de usuario registrado*  
 Expresión de cadena válida que proporciona un nombre de miembro.  
  
 Sin signo*entero*  
 Número válido que especifica el número de niveles que se omitirán.  
  
 Si se especifica la cláusula WITH DESCENDANTS, se mueve todo el árbol. Si no se especifica la cláusula WITH DESCENDANTS, los elementos secundarios de un elemento primario que se ha movido se convierten en los elementos secundarios del elemento primario del miembro que se ha movido. El efecto del movimiento es sencillamente actualizar los valores de la columna de clave primaria de la tabla de dimensiones subyacente.  
  
## <a name="updating-a-dimension-member"></a>Actualizar un miembro de dimensión  
 La cláusula UPDATE DIMENSION MEMBER permite modificar propiedades de un miembro, además de la fórmula de miembro personalizada asociada a un miembro.  
  
### <a name="arguments"></a>Argumentos  
 *Nombre de usuario registrado*  
 Expresión de cadena válida que proporciona un nombre de miembro.  
  
 *MDX_Expression*  
 Expresión MDX válida que devuelve un miembro único.  
  
 *Property_Value*  
 Expresión escalar MDX válida que define el valor de la propiedad de miembro calculado.  
  
## <a name="creating-a-cell-calculation"></a>Crear un cálculo de celda  
 Para obtener más información acerca de cómo crear un cálculo de celda mediante la instrucción ALTER CUBE, vea [DROP CELL CALCULATION instrucción &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

