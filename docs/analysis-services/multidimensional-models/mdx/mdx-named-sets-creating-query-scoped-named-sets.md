---
title: Crear ámbito de consulta (MDX) de conjuntos con nombre | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b30ba12d229f0c045d7a08a71c97a98de67a2bd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025532"
---
# <a name="mdx-named-sets---creating-query-scoped-named-sets"></a>Conjuntos con nombre denominado conjuntos: crear ámbito de consulta MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Instrucción SELECT & #40; MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Crear ámbito de sesión denominado conjuntos & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  
