---
title: Crear miembros calculados de ámbito de consulta (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6153b78b0dda1a72e2f7dfd790fa8bcecd0bb37
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074528"
---
# <a name="creating-query-scoped-calculated-members-mdx"></a>Crear miembros calculados en el ámbito de consulta (MDX)
  Si un miembro calculado solamente es necesario para una consulta de Expresiones multidimensionales (MDX) única, puede definir ese miembro calculado mediante la palabra clave WITH. Un miembro calculado que se ha creado con la palabra clave WITH deja de existir cuando cesa la ejecución de la consulta.  
  
 Como se trata en este tema, la sintaxis de la palabra clave WITH es bastante flexible, incluso permitiendo que un miembro calculado se base en otro miembro calculado.  
  
> [!NOTE]  
>  Para más información sobre los miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
## <a name="with-keyword-syntax"></a>Sintaxis de la palabra clave WITH  
 La siguiente sintaxis se utiliza para agregar la palabra clave WITH a una instrucción MDX SELECT:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 En la sintaxis de la palabra clave WITH, el valor `Member_Identifier` es el nombre completo del miembro calculado. El nombre completo incluye la dimensión o el nivel al que se asocia el miembro calculado. El valor `MDX_Expression` devuelve el valor del miembro calculado una vez que el valor de la expresión se ha evaluado. Los valores de las propiedades de celda intrínsecas para un miembro calculado se pueden especificar también proporcionando el nombre de la propiedad de celda en el valor `MemberProperty_Identifier` y el valor de la propiedad de celda en el valor `Scalar_Expression` .  
  
## <a name="with-keyword-examples"></a>Ejemplos de la palabra clave WITH  
 La siguiente consulta MDX define un miembro calculado, `[Measures].[Special Discount]`y calcula un descuento especial basado en la cantidad de descuento original.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 También puede crear miembros calculados en cualquier punto de una jerarquía. Por ejemplo, la siguiente consulta MDX define el miembro calculado `[BigSeller]` para un cubo Sales hipotético. Este miembro calculado determina si un establecimiento especificado tiene al menos 100,00 en ventas de unidades de cerveza y vino. Sin embargo, la consulta crea el miembro calculado `[BigSeller]` no como un miembro secundario de la dimensión `[Product]` , sino más bien como un miembro secundario del miembro `[Beer and Wine]` .  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 Los miembros calculados no tienen que depender solo de los miembros existentes en un cubo. El miembro calculado también puede basarse en otro miembro calculado definido en la misma expresión MDX. Por ejemplo, la siguiente consulta MDX utiliza el valor creado en el primer miembro calculado, `[Measures].[Special Discount]`, para generar el valor del segundo miembro calculado, `[Measures].[Special Discounted Amount]`.  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [Instrucción SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Crear miembros calculados de ámbito de sesión &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
