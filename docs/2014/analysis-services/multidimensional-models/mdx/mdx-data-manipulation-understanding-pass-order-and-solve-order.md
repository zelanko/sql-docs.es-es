---
title: Descripción, orden de paso y orden (MDX) de resolución | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d8d1797bc1ffdf937e37fb1ffae075691a892ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083015"
---
# <a name="understanding-pass-order-and-solve-order-mdx"></a>Descripción de orden de paso y orden de resolución (MDX)
  Cuando un cubo se calcula como el resultado de un script de MDX, puede atravesar varias fases de computación según el uso de varias características relativas al cálculo. Cada una de estas fases se denomina paso de cálculo.  
  
 Se puede hacer referencia a un paso de cálculo con una posición ordinal, llamada número de paso de cálculo. El recuento de los pasos de cálculo necesarios para calcular por completo todas las celdas de un cubo se denomina profundidad de paso de cálculo del cubo.  
  
 Los datos de la tabla de hechos y reescritura solo afectan al paso 0. Los scripts rellenan los datos después del paso 0; cada instrucción de asignación y cálculo de un script crea un nuevo paso. Fuera del script MDX, las referencias al paso absoluto 0 hacen referencia al último paso creado por el script del cubo.  
  
 Los miembros calculados se crean en todos los pasos, pero la expresión se aplica al paso actual. Los pasos anteriores contienen la medida calculada, pero con un valor NULL.  
  
## <a name="solve-order"></a>Orden de resolución  
 El orden de resolución determina la prioridad de cálculo en el caso de expresiones enfrentadas. En un solo paso, el orden de resolución determina dos cosas:  
  
-   El orden en el que [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] evalúa dimensiones, miembros, miembros calculados, resúmenes personalizados y celdas calculadas.  
  
-   El orden en el que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calcula miembros personalizados, miembros calculados, resúmenes personalizados y celdas calculadas.  
  
 Tendrá prioridad el miembro con el orden de resolución superior.  
  
> [!NOTE]  
>  La excepción a esta prioridad es la función Agregado. Los miembros calculados con la función Agregado tienen un orden de resolución inferior al de las medidas calculadas coincidentes.  
  
## <a name="solve-order-values-and-precedence"></a>Valores y prioridad de orden de resolución  
 Los valores de orden de resolución varían de -8181 a 65535. En este intervalo, algunos valores de orden de resolución corresponden a tipos específicos de cálculos, como se muestra en la siguiente tabla.  
  
|Cálculo|Orden de resolución|  
|-----------------|-----------------|  
|Fórmulas de miembro personalizado|-5119|  
|Operadores unarios|-5119|  
|Cálculo de totales visuales|-4096|  
|Resto de cálculos (si no se especifica lo contrario)|0|  
  
 Se recomienda utilizar enteros positivos para establecer valores de orden de resolución. Si asigna valores posteriores a los valores de orden de resolución mostrados en la tabla anterior, el paso de cálculo puede resultar imprevisible. Por ejemplo, el cálculo de un miembro calculado recibe un valor de orden de resolución que es menor que el valor de la fórmula de resumen personalizado predeterminado de -5119. Dicho valor de orden de resolución bajo produce los miembros calculados que se van a calcular antes de las fórmulas de resumen personalizadas y puede generar resultados incorrectos.  
  
### <a name="creating-and-changing-solve-order"></a>Crear y cambiar el orden de resolución  
 En el Diseñador de cubos, en el panel **Cálculos**, puede cambiar el orden de resolución de miembros calculados y celdas calculadas si cambia el orden de los cálculos.  
  
 En MDX, puede utilizar la palabra clave `SOLVE_ORDER` para crear o cambiar miembros calculados y celdas calculadas.  
  
## <a name="solve-order-examples"></a>Ejemplos de orden de resolución  
 Para ilustrar las posibles complejidades del orden de resolución, la siguiente serie de consultas MDX comienza con dos consultas que no presentan individualmente problemas de orden de resolución. Estas dos consultas se combinan en una consulta que requiere un orden de resolución.  
  
> [!NOTE]  
>  Puede ejecutar estas consultas MDX con la base de datos multidimensional de ejemplo de Adventure Works. Puede descargar el ejemplo de [modelos multidimensionales AdventureWorks SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) del sitio de codeplex.  
  
### <a name="query-1differences-in-income-and-expenses"></a>Consulta 1—Diferencias de Income y Expenses  
 En la primera consulta MDX, calcule la diferencia de ventas y costos de cada año creando una consulta MDX simple similar al siguiente ejemplo:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 En esta consulta, solo existe un miembro calculado: `Year Difference`. Dado que solo existe un miembro calculado, el orden de resolución no supone un problema mientras el cubo no utilice miembros calculados.  
  
 Esta consulta MDX ofrece un conjunto de resultados similar a la siguiente tabla.  
  
||Internet Sales Amount|Costo total del producto por Internet|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**Year Difference**|($20,160.56)|$2,878.06|  
  
### <a name="query-2percentage-of-income-after-expenses"></a>Consulta 2: porcentaje de ingresos después de gastos  
 En la segunda consulta, calcule el porcentaje de ingresos después de gastos para cada año con la siguiente consulta MDX:  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 En esta consulta MDX, al igual que en la anterior, solo existe un miembro calculado, `Profit Margin`, por lo que no se producen complicaciones por el orden de resolución.  
  
 Esta consulta MDX ofrece un conjunto de resultados similar a la siguiente tabla.  
  
||Internet Sales Amount|Costo total del producto por Internet|Margen de beneficio|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60 %|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45 %|  
  
 La diferencia de los conjuntos de resultados entre la primera y la segunda consulta radica en la distinta colocación del miembro calculado. En la primera consulta, el miembro calculado se encuentra en el eje ROWS, mientras que en la segunda consulta se encuentra en el eje COLUMNS. Esta distinta colocación adquiere importancia en la siguiente consulta, en la que se combinan dos miembros calculados en una única consulta MDX.  
  
### <a name="query-3combined-year-difference-and-net-income-calculations"></a>Consulta 3—Cálculos combinados de Year Difference y Net Income  
 En esta consulta final que combina los dos ejemplos previos en una sola consulta MDX, el orden de resolución es importante debido a los cálculos de ambas columnas y filas. Para asegurarse de que los cálculos se realizan en la secuencia correcta, defina la secuencia en que los cálculos se realizan con el `SOLVE_ORDER` palabra clave.  
  
 La palabra clave `SOLVE_ORDER` especifica el orden de resolución de los miembros calculados en una consulta MDX o en un comando `CREATE MEMBER`. Los valores enteros usados con el `SOLVE_ORDER` palabra clave son relativos, no necesitan empieza en cero y tienen que ser consecutivos. El valor ordena a MDX calcular un miembro según los valores resultantes del cálculo de miembros con un valor superior. Si se define un miembro calculado sin la `SOLVE_ORDER` palabra clave, el valor predeterminado es cero.  
  
 Por ejemplo, si combina los cálculos utilizados en las dos primeras consultas de ejemplo, la intersección de los dos miembros calculados, `Year Difference` y `Profit Margin`, se produce en una única celda en el conjunto de datos de resultados del ejemplo de consulta MDX. La única manera de determinar cómo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] evaluará esta celda es mediante el orden de resolución. Las fórmulas utilizadas para crear esta celda ofrecerán resultados diferentes según del orden de resolución de los dos miembros calculados.  
  
 En primer lugar, intente combinar los cálculos utilizados en las dos primeras consultas en la siguiente consulta MDX:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 En este ejemplo combinado de consulta MDX, `Profit Margin` posee el orden de resolución superior, por lo que tendrá prioridad si interactúan las dos expresiones. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] evalúa dicha celda mediante la fórmula `Profit Margin` . Los resultados de este cálculo anidado pueden verse en la siguiente tabla.  
  
||Internet Sales Amount|Costo total del producto por Internet|Margen de beneficio|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60 %|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45 %|  
|**Year Difference**|($20,160.56)|$2,878.06|114.28 %|  
  
 El resultado de la celda compartida se basa en la fórmula para `Profit Margin`. Es decir, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calcula el resultado en la celda compartida con los datos de `Year Difference` y ofrece la siguiente fórmula (se ha redondeado el resultado para obtener mayor claridad):  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 o Administrador de configuración de  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 Esto es a todas luces incorrecto. Sin embargo, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] calcula el resultado en una celda compartida de distinto modo si cambia el orden de resolución de los miembros calculados en la consulta MDX. La siguiente consulta MDX combinada invierte el orden de resolución de los miembros calculados:  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 Como se ha cambiado el orden de los miembros calculados, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] utiliza la fórmula `Year Difference` para evaluar la celda, como se muestra en la siguiente tabla.  
  
||Internet Sales Amount|Costo total del producto por Internet|Margen de beneficio|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60 %|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45 %|  
|**Year Difference**|($20,160.56)|$2,878.06|(0.15 %|  
  
 Puesto que la consulta utiliza la fórmula `Year Difference` con los datos de `Profit Margin` , la fórmula de la celda compartida es similar al siguiente cálculo:  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 o bien  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>Consideraciones adicionales  
 El orden de resolución puede ser un aspecto muy complicado, especialmente en cubos con un gran número de dimensiones que tienen miembros calculados, fórmulas de resúmenes personalizados o celdas calculadas. Cuando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] evalúa una consulta MDX, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiene en cuenta los valores del orden de resolución de todos los elementos implicados en un paso determinado, incluidas las dimensiones del cubo especificado en la consulta MDX.  
  
## <a name="see-also"></a>Vea también  
 [CalculationCurrentPass &#40;MDX&#41;](/sql/mdx/calculationcurrentpass-mdx)   
 [CalculationPassValue &#40;MDX&#41;](/sql/mdx/calculationpassvalue-mdx)   
 [Instrucción CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Manipular datos &#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  
