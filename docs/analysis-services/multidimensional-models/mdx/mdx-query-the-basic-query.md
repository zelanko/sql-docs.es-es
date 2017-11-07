---
title: "La consulta MDX básica (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], SELECT statement
- queries [MDX], about queries
- cellsets [MDX]
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: 4fa5a95a-fec9-4584-875c-dbf030c53e82
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8d80527166b6b6a1d49cbd4f3735689c429020e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query---the-basic-query"></a>Consulta MDX: la consulta básica
  La consulta de MDX (Expresiones multidimensionales) básica es la instrucción SELECT: la consulta utilizada con más frecuencia en MDX. Si comprende cómo una instrucción MDX SELECT debe especificar un conjunto de resultados, en qué consiste la sintaxis de la instrucción SELECT y cómo crear una consulta simple mediante la instrucción SELECT, tendrá un conocimiento sólido de cómo utilizar MDX para realizar consultas de datos multidimensionales.  
  
## <a name="specifying-a-result-set"></a>Especificar un conjunto de resultados  
 En MDX, la instrucción SELECT especifica un conjunto de resultados que contiene un subconjunto de datos multidimensionales que se han devuelto desde un cubo. Para especificar un conjunto de resultados, una consulta MDX debe contener la siguiente información:  
  
-   El número de ejes que desea que el conjunto de resultados contenga. Puede especificar hasta 128 ejes en una consulta de MDX.  
  
-   El conjunto de miembros o tuplas que se incluyen en cada eje de la consulta de MDX.  
  
-   El nombre del cubo que define el contexto de la consulta de MDX.  
  
-   El conjunto de miembros o tuplas que se incluyen en el eje segmentador. Para obtener más información sobre los ejes de consulta y segmentador, vea [Restringir la consulta con ejes de consulta y segmentador &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md).  
  
 Para identificar los ejes de consulta, el cubo que se consultará y el eje segmentador, la instrucción MDX SELECT utiliza las cláusulas siguientes:  
  
-   Una cláusula SELECT que determina los ejes de consulta de una instrucción MDX SELECT. Para obtener más información sobre la construcción de los ejes de consulta en una cláusula SELECT, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   Una cláusula FROM que determina qué cubo se consultará. Para obtener más información sobre la cláusula FROM, vea [SELECT &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
-   Una cláusula WHERE opcional que determina qué miembros o tuplas se utilizarán en el eje segmentador para restringir los datos devueltos. Para obtener más información sobre la construcción de un eje segmentador en una cláusula WHERE, vea [Especificar el contenido de un eje de división en sectores &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
> [!NOTE]  
>  Para obtener más información detallada sobre las distintas cláusulas de la instrucción SELECT, vea [SELECT &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="select-statement-syntax"></a>Sintaxis de la instrucción SELECT  
 En la sintaxis siguiente se muestra una instrucción SELECT básica que incluye el uso de las cláusulas SELECT, FROM y WHERE:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 La instrucción MDX SELECT admite una sintaxis opcional, como la palabra clave WITH, el uso de funciones de MDX para crear miembros calculados incluyéndolos en un eje o en un eje segmentador, y la capacidad de devolver los valores de propiedades específicas de celda como parte de la consulta. Para obtener más información sobre la instrucción MDX SELECT, vea [SELECT &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>Comparar la sintaxis de la instrucción MDX SELECT con SQL  
 El formato de la sintaxis de la instrucción MDX SELECT es similar al de la sintaxis de SQL. Sin embargo, hay varias diferencias fundamentales:  
  
-   La sintaxis MDX distingue conjuntos rodeando tuplas o miembros con llaves ({ }). Para obtener más información sobre la sintaxis de miembros, tuplas y conjuntos, vea [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
-   Las consultas de MDX pueden tener 0, 1, 2 ó hasta 128 ejes de consulta en la instrucción SELECT. Cada eje se comporta exactamente de la misma manera, a diferencia de en SQL, donde hay diferencias significativas entre el modo en que se comportan las filas y las columnas de una consulta.  
  
-   Al igual que con una consulta de SQL, la cláusula FROM da nombre al origen de los datos de la consulta de MDX. Sin embargo, la cláusula MDX FROM está restringida a un solo cubo. Se puede recuperar información de otros cubos, utilizando la función LookupCube valor por valor.  
  
-   La cláusula WHERE describe el eje segmentador de una consulta de MDX. Actúa como un eje invisible, un eje adicional en la consulta, dividiendo los valores que aparecen en las celdas del conjunto de resultados; a diferencia de la cláusula WHERE de SQL, que no afecta directamente a lo que aparece en el eje de las filas de la consulta. La funcionalidad de la cláusula WHERE de SQL está disponible a través de otras funciones de MDX como FILTER.  
  
## <a name="select-statement-example"></a>Ejemplo de instrucción SELECT  
 En el siguiente ejemplo se muestra una consulta de MDX básica que utiliza la instrucción SELECT. Esta consulta devuelve un conjunto de resultados que contiene las cifras de ventas e impuestos de 2002 y 2003 de la zona de ventas sudoeste.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 En este ejemplo, la consulta define la siguiente información del conjunto de resultados:  
  
-   La cláusula SELECT establece los ejes de la consulta en los miembros Sales Amount y Tax Amount de la dimensión Measures, y los miembros 2002 y 2003 de la dimensión Date.  
  
-   La cláusula FROM indica que el origen de datos es el cubo Adventure Works.  
  
-   La cláusula WHERE define el eje segmentador como el miembro Southwest de la dimensión Sales Territory.  
  
 Observe que el ejemplo de consulta utiliza también los alias de los ejes COLUMNS y ROWS. Las posiciones ordinales para estos ejes también podrían haberse utilizado. En el siguiente ejemplo se muestra cómo podría haberse escrito la consulta de MDX para que utilizara la posición ordinal de cada eje:  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Para obtener ejemplos detallados, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) y [Especificar el contenido de un eje de división en sectores &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave de MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Instrucción SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  

