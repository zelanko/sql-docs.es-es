---
title: Generar (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7a6008129d6b0a4c59412428c31f6e5de625f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005907"
---
# <a name="generate-mdx"></a>Generate (MDX)


  Aplica un conjunto a cada miembro de otro conjunto y a continuación combina los conjuntos resultantes mediante unión. Alternativamente, esta función devuelve una cadena concatenada que se creó evaluando una expresión de cadena en un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser el nombre del miembro actual (CurrentMember.Name) de cada tupla del conjunto especificado.  
  
 *Delimiter*  
 Delimitador válido expresado como expresión de cadena.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un segundo conjunto, la función **Generate** devuelve un conjunto generado aplicando las tuplas del segundo conjunto a cada tupla del primer conjunto y combinando después los conjuntos resultantes por Unión. Si se especifica **All** , la función conserva los duplicados en el conjunto resultante.  
  
 Si se especifica una expresión de cadena, la función **Generate** devuelve una cadena generada mediante la evaluación de la expresión de cadena especificada en cada tupla del primer conjunto y, a continuación, la concatenación de los resultados. De forma opcional, la cadena se puede delimitar al separar cada resultado de la cadena concatenada resultante.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="set"></a>Set  
 En el ejemplo siguiente, la consulta devuelve un conjunto que contiene cuatro veces la medida Internet Sales Amount, porque hay cuatro miembros en el conjunto [Date].[Calendar Year].[Calendar Year].MEMBERS:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 Al quitar ALL, se modifica la consulta de modo que devuelva Internet Sales Amount una sola vez:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 El uso práctico más común de **Generating** es evaluar una expresión de conjunto compleja, como topcount, en un conjunto de miembros. La consulta de ejemplo siguiente muestra los 10 productos más vendidos de cada año natural (Calendar Year) en filas:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 Tenga en cuenta que se muestran otros 10 superiores para cada año y que el uso de **Generate** es la única manera de obtener este resultado. Basta con unir de forma cruzada los años naturales para que el conjunto de los 10 productos más vendidos muestre los 10 productos más vendidos de todo el tiempo, repetidos para cada año, tal y como se muestra en el ejemplo siguiente:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 En el ejemplo siguiente se muestra el uso de **Generate** para devolver una cadena:  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Esta forma de la función **Generate** puede ser útil al depurar cálculos, ya que permite devolver una cadena que muestra los nombres de todos los miembros de un conjunto. Esto puede ser más fácil de leer que la representación MDX estricta de un conjunto que devuelve [SetToStr &#40;función&#41;MDX](../mdx/settostr-mdx.md) .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
