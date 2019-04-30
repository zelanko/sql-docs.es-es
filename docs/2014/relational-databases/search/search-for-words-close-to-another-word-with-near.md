---
title: Buscar palabras cerca de otra palabra con NEAR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3493657fb537057f7c0ff8e126582ceb6faccc11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238391"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Buscar palabras cerca de otra palabra con NEAR
  Puede usar un término de proximidad (NEAR) en un predicado [CONTAINS](/sql/t-sql/queries/contains-transact-sql) o en una función [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para buscar palabras o frases que están cerca unas de otras. También puede especificar el número máximo de términos de no búsqueda que separan el primero y el último término de búsqueda. Además, puede buscar palabras o frases en cualquier orden o puede buscar palabras y frases en el orden en el que las especifique. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite tanto el anterior [término de proximidad genérico](#Generic_NEAR), que está en desuso y el [término de proximidad personalizado](#Custom_NEAR), que es nuevo en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
##  <a name="Custom_NEAR"></a> El término de proximidad personalizado  
 El término de proximidad personalizado presenta las siguientes capacidades nuevas:  
  
-   Puede especificar el número máximo de términos de no búsqueda, o *distancia máxima*, que separa el primero y el último término de búsqueda para que haya una coincidencia.  
  
-   Si especifica el número máximo de términos, también puede especificar que las coincidencias deben contener los términos de búsqueda en el orden especificado.  
  
 Para que se considere una coincidencia, una cadena de texto debe:  
  
-   Empezar con uno de los términos de búsqueda especificados y terminar con el otro término de búsqueda especificado.  
  
-   Contener todos los términos de búsqueda especificados.  
  
-   El número de términos de no búsqueda, incluidas las palabras irrelevantes, que hay entre el primero y el último término de búsqueda debe ser menor o igual que la distancia máxima, si se especifica.  
  
 La sintaxis básica es:  
  
 NEAR (  
  
 {  
  
 *término_búsqueda* [,... *n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
  
> [!NOTE]  
>  Para obtener más información sobre la sintaxis de <término_proximidad_personalizado>, vea [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 Por ejemplo, podría buscar 'John' a dos términos de 'Smith', de la manera siguiente:  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 Algunos ejemplos de cadenas que coinciden son "`John Jacob Smith`" y "`Smith, John`". La cadena "`John Jones knows Fred Smith`" contiene tres términos de no búsqueda activos, por lo que no es una coincidencia.  
  
 Para exigir que los términos se encuentren en el orden especificado, cambiaría el término de proximidad del ejemplo a `NEAR((John, Smith),2, TRUE).` Esto busca "`John`" a dos términos de "`Smith`" pero solo cuando "`John`" precede a "`Smith`". En un idioma que se lee de izquierda a derecha, como el inglés, un ejemplo de cadena coincidente es "`John Jacob Smith`.  
  
 Tenga en cuenta que en un idioma que se lee de derecha a izquierda, como el árabe o el hebreo, el Motor de búsqueda de texto completo aplica en orden inverso los términos especificados. Asimismo, el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] invierte automáticamente el orden de presentación de las palabras especificadas en los idiomas que se leen de derecha a izquierda.  
  
> [!NOTE]  
>  Para obtener más información, vea "[Consideraciones adicionales sobre las búsquedas de proximidad](#Additional_Considerations)," más adelante en este tema.  
  
### <a name="how-maximum-distance-is-measured"></a>Cómo se mide la distancia máxima  
 Una distancia máxima concreta, como 10 ó 25, determina cuántos términos de no búsqueda, incluidas las palabras irrelevantes, puede haber entre el primero y el último término de búsqueda en una cadena determinada. Por ejemplo, `NEAR((dogs, cats, "hunting mice"), 3)` devolverían la siguiente fila, en la que el número total de términos de no búsqueda es tres ("`enjoy`", "`but`" y "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 El mismo término de proximidad no devolvería la siguiente fila, ya que los cuatro términos de no búsqueda ("`enjoy`", "`but`", "`usually`" y "`avoid`") superan la distancia máxima:  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### <a name="combining-a-custom-proximity-term-with-other-terms"></a>Combinar un término de proximidad personalizado con otros términos  
 Puede combinar un término de proximidad personalizado con algunos otros términos. Puede usar AND (&), OR (|) o AND NOT (&!) para combinar un término de proximidad personalizado con otro término de proximidad personalizado, un término simple o un término de prefijo. Por ejemplo:  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 Por ejemplo,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 No se puede combinar un término de proximidad personalizado con un término de proximidad genérico (*término1* NEAR *término2*), un término de generación (ISABOUT …) o un término ponderado (FORMSOF …).  
  
### <a name="example-using-the-custom-proximity-term"></a>Ejemplo: Usar el término de proximidad personalizado  
 En el siguiente ejemplo se buscan todos los resúmenes de documento que contienen el palabra "reflector" en el mismo documento que la palabra "bracket" en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks2012` .  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  

  
##  <a name="Additional_Considerations"></a> Consideraciones adicionales para las búsquedas de proximidad  
 En esta sección se describen las consideraciones que afectan tanto a las búsquedas de proximidad genéricas como a las personalizadas:  
  
-   Apariciones superpuestas de términos de búsqueda  
  
     Todas las búsquedas de proximidad siempre buscan únicamente apariciones no superpuestas. Las apariciones superpuestas de términos de búsqueda nunca se consideran coincidencias. Por ejemplo, considere el siguiente término de proximidad, que busca "`A`" y "`AA`" en este orden con una distancia máxima de dos términos:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     Las posibles coincidencias son "`AAA`", "`A.AA`" y "`A..AA`". Las filas que simplemente contienen "`AA`" no coincidirían.  
  
    > [!NOTE]  
    >  Puede especificar términos que se superponen, por ejemplo `NEAR("mountain bike", "bike trails")` o `(NEAR(comfort*, comfortable), 5)`. La especificación de un término superpuesto aumenta la complejidad de la consulta incrementando las posibles permutaciones de coincidencia. Si especifica un número grande de términos superpuestos, la consulta puede quedarse sin recursos y producir un error. En tal caso, simplifique la consulta e inténtelo de nuevo.  
  
-   Tanto NEAR genérico como NEAR personalizado (independientemente de que se especifique una distancia máxima o no) indican la distancia lógica entre los términos, no la distancia absoluta entre ellos. Por ejemplo, los términos dentro de frases diferentes o las sentencias dentro de un párrafo se tratan como más alejados que los términos de la misma frase o sentencia, sin tener en cuenta su proximidad real, suponiéndose que están menos relacionados. Igualmente, los términos en párrafos diferentes se consideran todavía más alejados. Si una coincidencia abarca el final de una frase, un párrafo o un capítulo, el intervalo utilizado para clasificar un documento aumenta en 8, 128 ó 1024, respectivamente.  
  
-   Impacto de los términos de proximidad en la clasificación por la función CONTAINSTABLE  
  
     Cuando se utiliza NEAR en la función CONTAINSTABLE, el número de aciertos en un documento con respecto a su longitud, así como la distancia entre el primero y el último término de búsqueda de cada uno de los aciertos, afecta a la clasificación de cada documento. En el caso de un término de proximidad genérico, si los términos de búsqueda con coincidencia están a >50 términos lógicos, el rango devuelto de un documento es 0. Si se trata de un término de proximidad personalizado que no especifica un entero como la distancia máxima, un documento que solo contenga aciertos cuyo intervalo sea >100 términos lógicos recibirá una clasificación de 0. Para obtener más información acerca de la clasificación de búsquedas de proximidad personalizadas, vea [Limit Search Results with RANK](limit-search-results-with-rank.md).  
  
-   La opción de servidor **transformar palabras irrelevantes**   
  
     El valor de **transformar palabras irrelevantes** afecta a cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata las palabras irrelevantes si se especifican en búsquedas por proximidad. Para más información, vea [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  

  
##  <a name="Generic_NEAR"></a> El término de proximidad genérico desusado  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Se recomienda que use el [término de proximidad personalizado](#Custom_NEAR).  
  
 Un término de proximidad genérico indica que todos los términos de búsqueda especificados deben estar en un documento para que se devuelva una coincidencia, independientemente del número de términos de no búsqueda (la *distancia*) que haya entre los términos de búsqueda. La sintaxis básica es:  
  
 { *search_term* { NEAR | ~ } *search_term* } [ ,...*n* ]  
  
 Por ejemplo, en los ejemplos siguientes deben aparecer las palabras 'fox' y 'chicken', en cualquier orden, para que se genere una coincidencia:  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  Para obtener información sobre la sintaxis de <término_proximidad_genérico>, vea [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 Para obtener más información, vea "[Consideraciones adicionales sobre las búsquedas de proximidad](#Additional_Considerations)," más adelante en este tema.  
  
### <a name="combining-a-generic-proximity-term-with-other-terms"></a>Combinar un término de proximidad genérico con otros términos  
 Puede usar AND (&), OR (|) o AND NOT (&!) para combinar un término de proximidad genérico con otro término de proximidad genérico, un término simple o un término de prefijo. Por ejemplo:  
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 No se puede combinar un término de proximidad genérico con un término de proximidad personalizado, como `NEAR((term1,term2),5)`, un término ponderado (ISABOUT …) o un término de generación (FORMSOF …).  
  
### <a name="example-using-the-generic-proximity-term"></a>Ejemplo: Usar el término de proximidad genérico  
 En el siguiente ejemplo se utiliza el término de proximidad genérico para buscar la palabra "reflector" en el mismo documento que la palabra "bracket".  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 Tenga en cuenta que también puede invertir los términos de CONTAINSTABLE para obtener el mismo resultado:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 Puede utilizar el carácter de tilde (~) en el lugar de la palabra clave NEAR de la consulta anterior y obtener el mismo resultado:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 En las condiciones de búsqueda se pueden especificar más de dos palabras o frases. Por ejemplo, es posible escribir:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 Esto significa que "reflector" debe estar en el mismo documento que "bracket" y "bracket" debe estar en el mismo documento que "installation".  
  

  
## <a name="see-also"></a>Vea también  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [Consultar con búsqueda de texto completo](query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
