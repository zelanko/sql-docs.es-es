---
title: Operadores (sintaxis de MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- precedence [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1ff5a529-88fd-4619-86e1-19fa214650d6
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fd52d724dc1b51943019339bacdc56ea334492cf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="operators-mdx-syntax"></a>Operadores (sintaxis de MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En las expresiones multidimensionales (MDX), los operadores permiten llevar a cabo las siguientes acciones:  
  
-   Cambiar datos, permanente o temporalmente.  
  
-   Buscar valores u objetos que cumplan una condición específica.  
  
-   Implementar una decisión entre columnas o expresiones.  
  
-   Probar determinadas condiciones antes de iniciar o confirmar una transacción, o antes de ejecutar determinadas instrucciones.  
  
 MDX es compatible con los operadores que se indican en la siguiente tabla:  
  
|Para realizar este tipo de operación|Utilice|  
|---------------------------------------|---------|  
|Asignar un valor a una variable o asociar una columna de un conjunto de resultados a un alias.|[Operadores de asignación](../mdx/assignment-operators.md)|  
|Sumar, restar, multiplicar, dividir.|[Operadores aritméticos](../mdx/arithmetic-operators.md)|  
|Probar si una condición es cierta, como AND, OR, NOT y XOR.|[Operadores bit a bit](../mdx/bitwise-operators.md)|  
|Comparar un valor con otro valor o una expresión.|[Operadores de comparación](../mdx/comparison-operators.md)|  
|Combinar de forma permanente o temporal dos cadenas en una.|[Operadores de concatenación](../mdx/concatenation-operators.md)|  
|Combinar temporal o permanentemente dos conjuntos de expresiones en un solo conjunto.|[Operadores de conjuntos](../mdx/set-operators.md)|  
|Realizar una operación en un operando.|[Operadores unarios](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  En las consultas, cualquier persona que pueda ver los datos del cubo que se usarán con algún tipo de operador puede realizar operaciones. Para cambiar los datos correctamente, son necesarios los permisos adecuados.  
  
 Cuando se utilizan varios operadores, el orden en que MDX los evalúa es importante. Del mismo modo, es posible que el usuario de los operadores tenga que convertir un tipo de datos en otro para poder evaluar los operadores.  
  
## <a name="evaluating-complex-expressions"></a>Evaluar expresiones complejas  
 Puede generar una expresión mediante el uso de operadores que combinen varias expresiones más pequeñas. En estas expresiones complejas, MDX evalúa los operadores en orden basado en la definición de la precedencia de operadores utilizados por [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. MDX ejecuta los operadores con mayor precedencia antes que los operadores con menor precedencia.  
  
### <a name="understanding-operator-precedence"></a>Descripción de la precedencia de los operadores  
 En la siguiente lista se muestra la precedencia de los operadores, de mayor a menor. Los operadores situados en la misma línea tienen el mismo nivel de precedencia y se evalúan de izquierda a derecha, salvo que el uso de un paréntesis obligue a hacerlo de otro modo:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   y  
  
-   XOR  
  
-   o  
  
 Para obtener más información acerca de los operadores en MDX, vea [referencia de operadores de MDX &#40; MDX &#41; ](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Determinar los resultados  
 Cuando se combinan expresiones simples para crear una más compleja, el tipo de datos del valor resultante viene determinado por la combinación de las reglas de los operadores con las reglas de precedencia para los tipos de datos.  
  
 Si el resultado es un carácter o un valor de Unicode, la intercalación del resultado viene determinada por la combinación de las reglas de los operadores con las reglas de precedencia de intercalación. Para obtener más información acerca de las intercalaciones, vea [idiomas e intercalaciones &#40; Analysis Services &#41; ](../analysis-services/languages-and-collations-analysis-services.md).  
  
 También hay reglas que determinan la precisión, escala y longitud del resultado basándose en la precisión, escala y longitud de las expresiones sencillas.  
  
## <a name="converting-data-types"></a>Convertir tipos de datos  
 MDX convierte implícitamente un objeto a un tipo distinto cuando el objeto se usa en una expresión que requiere un tipo diferente. En la siguiente tabla se definen las reglas de conversión de cada objeto.  
  
|Tipo original|Tipo necesario|Conversión|  
|-------------------|-----------------|----------------|  
|Nivel|Establecer|\<nivel > .members|  
|Jerarquía|Miembro|\<jerarquía > .defaultmember|  
|Miembro|Tuple|(\<Miembro >)|  
|Tuple|Miembro|\<tupla > .item(0)|  
|Tuple|Escalar|\<tupla > .value|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Elementos de sintaxis MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
