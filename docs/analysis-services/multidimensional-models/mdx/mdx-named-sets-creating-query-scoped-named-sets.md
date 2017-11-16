---
title: "Crear ámbito de consulta (MDX) de conjuntos con nombre | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query-scoped named sets [MDX]
- WITH keyword
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06751ad71a12e537728167d4d8a9cdec0a870962
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-named-sets---creating-query-scoped-named-sets"></a>Conjuntos con nombre denominado conjuntos: crear ámbito de consulta MDX
  Si un conjunto con nombre solo es necesario para una consulta de Expresiones multidimensionales (MDX) única, puede definir ese conjunto con nombre mediante la palabra clave WITH. Un conjunto con nombre que se ha creado con la palabra clave WITH deja de existir cuando cesa la ejecución de la consulta.  
  
 Como se trata en este tema, la sintaxis de la palabra clave WITH es bastante flexible, incluso ajustando el uso de funciones para definir el conjunto con nombre.  
  
> [!NOTE]  
>  Para más información sobre los conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
## <a name="with-keyword-syntax"></a>Sintaxis de la palabra clave WITH  
 La siguiente sintaxis se utiliza para agregar la palabra clave WITH a una instrucción MDX SELECT:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 En la sintaxis de la palabra clave WITH, el parámetro `Set_Identifier` contiene el alias del conjunto con nombre. El parámetro `Set_Expression` contiene la expresión de conjunto a la que hará referencia el alias del conjunto con nombre.  
  
## <a name="with-keyword-example"></a>Ejemplo de la palabra clave WITH  
 La siguiente consulta MDX examina las ventas por unidad de diversos vinos Chardonnay y Chablis en **FoodMart 2000**, la base de datos de ejemplo de Microsoft SQL Server 2000 Analysis Services. Esta consulta, a pesar de parecer bastante sencilla en cuanto al conjunto de resultados, resulta lenta y difícil de controlar a la hora del mantenimiento.  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 Para facilitar el mantenimiento de la consulta de MDX anterior, puede crear un conjunto con nombre para la consulta mediante la palabra clave WITH. El siguiente código muestra cómo utilizar la palabra clave WITH para crear un conjunto con nombre, `[ChardonnayChablis]`, y cómo el conjunto con nombre acorta la instrucción SELECT y facilita su mantenimiento.  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### <a name="using-functions-together-with-the-with-keyword"></a>Usar funciones junto con la palabra clave WITH  
 Aunque puede definir explícitamente cada miembro de un conjunto definido, de este modo puede producir una instrucción larga. Para facilitar la creación y mantenimiento de un conjunto con nombre, puede utilizar funciones de MDX para definir los miembros.  
  
 Por ejemplo, el siguiente ejemplo de consulta MDX utiliza las funciones MDX [Filter](../../../mdx/filter-mdx.md), [CurrentMember](../../../mdx/currentmember-mdx.md)y [Name](../../../mdx/name-mdx.md) y la función InStr de VBA para crear el conjunto con nombre `[ChardonnayChablis]` . Esta versión del conjunto con nombre `[ChardonnayChablis]` es el mismo que la versión definida explícitamente que se ha mostrado anteriormente en este tema.  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Crear ámbito de sesión denominado conjuntos &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  

