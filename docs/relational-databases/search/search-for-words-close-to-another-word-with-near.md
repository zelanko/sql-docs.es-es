---
title: Buscar palabras cerca de otra palabra con NEAR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 00e3df715e7a608c47eff977448d20f6364a467c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Buscar palabras cerca de otra palabra con NEAR
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede usar el *término de proximidad* **NEAR** en un predicado [CONTAINS](../../t-sql/queries/contains-transact-sql.md) o en una función [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para buscar palabras o frases que están cerca unas de otras. 
  
##  <a name="Custom_NEAR"></a> Introducción a NEAR  
**NEAR** tiene las características siguientes:  
-   Puede especificar el número máximo de términos de no búsqueda que separan el primero y el último término de búsqueda.

-   Puede buscar palabras o frases en cualquier orden o puede buscar palabras y frases en un orden específico.
  
-   Puede especificar el número máximo de términos de no búsqueda, o *distancia máxima*, que separa el primero y el último término de búsqueda para que haya una coincidencia.  

-   Si especifica el número máximo de términos, también puede especificar que las coincidencias deben contener los términos de búsqueda en el orden especificado.

 
 Para que se considere una coincidencia, una cadena de texto debe:  
  
-   Empezar con uno de los términos de búsqueda especificados y terminar con el otro término de búsqueda especificado.  
  
-   Contener todos los términos de búsqueda especificados.  
  
-   El número de términos de no búsqueda, incluidas las palabras irrelevantes, que hay entre el primero y el último término de búsqueda debe ser menor o igual que la distancia máxima, si esta se especifica.  
  
## <a name="syntax-of-near"></a>Sintaxis de NEAR
La sintaxis básica de **NEAR** es:  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,…*n* ]  
  
 |  
  
 (*search_term* [ ,…*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

Para más información sobre la sintaxis, vea [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  

## <a name="examples"></a>Ejemplos
### <a name="example-1"></a>Ejemplo 1
 Por ejemplo, podría buscar 'John' a dos términos de 'Smith', de la manera siguiente:  
  
```sql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 Algunos ejemplos de cadenas que coinciden son "`John Jacob Smith`" y "`Smith, John`". La cadena "`John Jones knows Fred Smith`" contiene tres términos de no búsqueda activos, por lo que no es una coincidencia.  
  
 Para exigir que los términos se encuentren en el orden especificado, cambiaría el término de proximidad del ejemplo a `NEAR((John, Smith),2, TRUE).` Esto busca "`John`" a dos términos de "`Smith`" pero solo cuando "`John`" precede a "`Smith`". En un idioma que se lee de izquierda a derecha, como el inglés, un ejemplo de cadena coincidente es "`John Jacob Smith`.  
  
 Tenga en cuenta que en un idioma que se lee de derecha a izquierda, como el árabe o el hebreo, el Motor de búsqueda de texto completo aplica en orden inverso los términos especificados. Asimismo, el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] invierte automáticamente el orden de presentación de las palabras especificadas en los idiomas que se leen de derecha a izquierda.   

### <a name="example-2"></a>Ejemplo 2
 En el siguiente ejemplo se buscan todos los resúmenes de documento que contienen el palabra "reflector" en el mismo documento que la palabra "bracket" en la tabla `Production.Document` de la base de datos de ejemplo `AdventureWorks` .  
  
```sql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>Cómo se mide la distancia máxima  
 Una distancia máxima concreta, como 10 ó 25, determina cuántos términos de no búsqueda, incluidas las palabras irrelevantes, puede haber entre el primero y el último término de búsqueda en una cadena determinada. Por ejemplo, `NEAR((dogs, cats, "hunting mice"), 3)` devolverían la siguiente fila, en la que el número total de términos de no búsqueda es tres ("`enjoy`", "`but`" y "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 El mismo término de proximidad no devolvería la siguiente fila, ya que los cuatro términos de no búsqueda ("`enjoy`", "`but`", "`usually`" y "`avoid`") superan la distancia máxima:  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>Combinar NEAR con otros términos  
 Puede combinar NEAR con algunos otros términos. Puede usar AND (&), OR (|) o AND NOT (&!) para combinar un término de proximidad personalizado con otro término de proximidad personalizado, un término simple o un término de prefijo. Por ejemplo:  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NEAR((*term3*, *term4*),2)')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR NEAR((*term3*, *term4*),2, TRUE)')  
  
 Por ejemplo,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 No se puede combinar NEAR con un término de generación (ISABOUT …) o un término ponderado (FORMSOF …).  
  
##  <a name="Additional_Considerations"></a> Más información sobre las búsquedas de proximidad  
   
-   Apariciones superpuestas de términos de búsqueda  
  
     Todas las búsquedas de proximidad siempre buscan únicamente apariciones no superpuestas. Las apariciones superpuestas de términos de búsqueda nunca se consideran coincidencias. Por ejemplo, considere el siguiente término de proximidad, que busca "`A`" y "`AA`" en este orden con una distancia máxima de dos términos:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     Las posibles coincidencias son "`AAA`", "`A.AA`" y "`A..AA`". Las filas que simplemente contienen "`AA`" no coincidirían.  
  
    > [!NOTE]  
    >  Puede especificar términos que se superponen, por ejemplo `NEAR("mountain bike", "bike trails")` o `(NEAR(comfort*, comfortable), 5)`. La especificación de un término superpuesto aumenta la complejidad de la consulta incrementando las posibles permutaciones de coincidencia. Si especifica un número grande de términos superpuestos, la consulta puede quedarse sin recursos y producir un error. En tal caso, simplifique la consulta e inténtelo de nuevo.  
  
-   NEAR (independientemente de que se especifique una distancia máxima o no) indica la distancia lógica entre los términos, no la distancia absoluta entre ellos. Por ejemplo, los términos dentro de frases diferentes o las sentencias dentro de un párrafo se tratan como más alejados que los términos de la misma frase o sentencia, sin tener en cuenta su proximidad real, suponiéndose que están menos relacionados. Igualmente, los términos en párrafos diferentes se consideran todavía más alejados. Si una coincidencia abarca el final de una frase, un párrafo o un capítulo, el intervalo utilizado para clasificar un documento aumenta en 8, 128 ó 1024, respectivamente.  
  
-   Impacto de los términos de proximidad en la clasificación por la función CONTAINSTABLE  
  
    Cuando se utiliza NEAR en la función CONTAINSTABLE, el número de aciertos en un documento con respecto a su longitud, así como la distancia entre el primero y el último término de búsqueda de cada uno de los aciertos, afecta a la clasificación de cada documento. En el caso de un término de proximidad genérico, si los términos de búsqueda con coincidencia están a >50 términos lógicos, el rango devuelto de un documento es 0. Si se trata de un término de proximidad personalizado que no especifica un entero como la distancia máxima, un documento que solo contenga aciertos cuyo intervalo sea >100 términos lógicos recibirá una clasificación de 0. Para obtener más información acerca de la clasificación de búsquedas de proximidad personalizadas, vea [Limit Search Results with RANK](../../relational-databases/search/limit-search-results-with-rank.md).  
  
-   La opción de servidor **transformar palabras irrelevantes**   
  
     El valor de **transformar palabras irrelevantes** afecta a cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata las palabras irrelevantes si se especifican en búsquedas por proximidad. Para más información, vea [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).   
  
## <a name="see-also"></a>Ver también  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
