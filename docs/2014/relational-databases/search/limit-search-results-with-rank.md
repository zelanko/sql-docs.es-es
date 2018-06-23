---
title: Limitación de los resultados de la búsqueda con RANK | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- row ranking [full-text search]
- relevance ranking values [full-text search]
- full-text search [SQL Server], rankings
- index rankings [full-text search]
- ranked results [full-text search]
- rankings [full-text search]
- per-row rank values [full-text search]
ms.assetid: 06a776e6-296c-4ec7-9fa5-0794709ccb17
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cef510acee74d2ce261a1e000761f214571c16ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106728"
---
# <a name="limit-search-results-with-rank"></a>Limitar los resultados de la búsqueda con RANK
  Las funciones [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) y [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) devuelven una columna denominada RANK que contiene valores ordinales de 0 a 1000 (valores de intervalo). Estos valores se utilizan para clasificar las filas devueltas en función del grado de coincidencia con los criterios de selección. Los valores de clasificación solo indican un orden relativo de relevancia de las filas en el conjunto de resultados, con un valor inferior que indica la relevancia menor. Los valores reales carecen de relevancia y normalmente difieren cada vez que se ejecuta la consulta.  
  
> [!NOTE]  
>  Los predicados CONTAINS y FREETEXT no devuelven ningún valor de clasificación.  
  
 El número de elementos que coincide con una condición de búsqueda suele ser muy grande. Para evitar que las consultas CONTAINSTABLE o FREETEXTTABLE devuelvan demasiadas coincidencias, use el parámetro opcional *top_n_by_rank* , que solo devuelve un subconjunto de filas. *top_n_by_rank* es un valor entero, donde *n*especifica que solo se devuelvan las *n* coincidencias con la clasificación más alta, en orden descendente. Si se combina *top_n_by_rank* con otros parámetros, es posible que la consulta devuelva menos filas de las que en realidad coinciden con todos los predicados.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ordena las coincidencias por orden de clasificación y devuelve solo hasta el número especificado de filas. Esta opción puede aumentar significativamente el rendimiento. Por ejemplo, una consulta que por lo general devolvería 100.000 filas de una tabla de 1 millón se procesará de forma más rápida si solo se solicitan las 100 primeras filas.  
  
##  <a name="examples"></a> Ejemplos del uso de RANK para limitar los resultados de la búsqueda  
  
### <a name="example-a-searching-for-only-the-top-three-matches"></a>Ejemplo A: buscar solo las tres primeras coincidencias  
 En el ejemplo siguiente se usa CONTAINSTABLE para devolver las tres primeras coincidencias.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT K.RANK, AddressLine1, City  
FROM Person.Address AS A  
  INNER JOIN  
  CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("des*",  
    Rue WEIGHT(0.5),  
    Bouchers WEIGHT(0.9))',  
    3) AS K  
  ON A.AddressID = K.[KEY]  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
RANK        Address                          City  
----------- -------------------------------- ------------------------------  
172         9005, rue des Bouchers           Paris  
172         5, rue des Bouchers              Orleans  
172         5, rue des Bouchers              Metz  
  
(3 row(s) affected)  
```  
  
  
### <a name="example-b-searching-for-the-top-ten-matches"></a>Ejemplo B: buscar las diez primeras coincidencias  
 En el ejemplo siguiente se usa CONTAINSTABLE para devolver la descripción de los 5 productos más destacados, donde la columna `Description` contiene la palabra “aluminum” cerca de la palabra “light” o de la palabra “lightweight”.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
GO  
```  
  
  
##  <a name="how"></a> Cómo se clasifican los resultados de la consulta de búsqueda  
 La búsqueda de texto completo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede generar una puntuación (o valor de rango) opcional que indica la relevancia de los datos devueltos por una consulta de texto completo. Este valor de rango se calcula en cada fila y se puede utilizar como criterio de ordenación para ordenar el conjunto de resultados de una consulta determinada por relevancia. Los valores de clasificación solo indican un orden de importancia relativa de las filas en el conjunto de resultados. Los valores reales carecen de relevancia y normalmente difieren cada vez que se ejecuta la consulta. El valor de rango no tiene importancia en las consultas.  
  
### <a name="statistics-for-ranking"></a>Estadísticas de clasificación  
 Cuando se compila un índice, se recopilan estadísticas para usarlas en la clasificación. El proceso de creación de un catálogo de texto completo no produce directamente una única estructura de índice. En su lugar, el motor de búsqueda de texto completo para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea índices intermedios a medida que se indizan los datos. El motor de búsqueda de texto completo combina después dichos índices en un índice mayor, según sea necesario. Este proceso puede repetirse muchas veces. A continuación, el motor de búsqueda de texto completo realiza una "mezcla maestra" que combina todos los índices intermedios en un gran índice maestro.  
  
 En cada índice intermedio se recopilan estadísticas, que se mezclan cuando se mezclan los índices. Algunos valores estadísticos solo pueden generarse durante el proceso de mezcla maestra.  
  
 Mientras se clasifica un conjunto de resultados de consulta, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utiliza las estadísticas del índice intermedio más grande. Dependerá de si se han mezclado o no los índices intermedios. Como resultado, las estadísticas de clasificación serán más o menos precisas si no se han mezclado los índices intermedios. Por este motivo, una misma consulta puede devolver con el tiempo distintos resultados de rango, a medida que se agreguen, modifiquen y eliminen los datos de índices de texto completo, y se vayan combinando los índices de menor tamaño.  
  
 Para minimizar el tamaño del índice y la complejidad del cálculo, se suelen redondear las estadísticas.  
  
 En la siguiente lista se mencionan algunos términos y valores estadísticos de uso frecuente que son importantes para calcular la clasificación.  
  
 Property  
 Una columna indizada de texto completo de la fila.  
  
 Documento  
 Entidad que se devuelve en las consultas. En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se corresponde con una fila. Un documento puede tener varias propiedades, de igual forma que una fila puede tener varias columnas indizadas de texto completo.  
  
 Índice  
 Un único índice invertido de uno o varios documentos. Puede almacenarse completamente en la memoria o en disco. Muchas estadísticas de consultas son relativas al índice individual donde se produjo la coincidencia.  
  
 Catálogo de texto completo  
 Colección de índices intermedios que se considera como una sola entidad en las consultas. Los catálogos son la unidad de organización visible para el administrador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Palabra, token o elemento  
 Unidad coincidente en el motor de texto completo. Los flujos de texto de los documentos se acortan formando palabras o tokens, gracias a los separadores de palabras específicos del idioma.  
  
 Repetición  
 Desplazamiento de las palabras en una propiedad de documento, tal y como lo determina el separador de palabras. La primera palabra se encuentra en la repetición 1, la siguiente en la 2 y así sucesivamente. Para evitar falsos positivos en las consultas de frases y de proximidad, al final de las frases y de los párrafos se insertan mayores espacios de repetición.  
  
 TermFrequency  
 Número de repeticiones del valor de clave en una fila.  
  
 IndexedRowCount  
 Número total de filas indizadas. Se calcula a partir de los recuentos mantenidos en los índices intermedios. Este número puede ser más o menos preciso.  
  
 KeyRowCount  
 Número total de filas del catálogo de texto completo que contienen una determinada clave.  
  
 MaxOccurrence  
 Número máximo de repeticiones de una determinada propiedad de una fila, almacenadas en un catálogo de texto completo.  
  
 MaxQueryRank  
 El rango máximo, 1000, devuelto por el motor de búsqueda de texto completo.  
  
  
### <a name="rank-computation-issues"></a>Problemas de cálculo de rango  
 El proceso de cálculo de rango depende de varios factores.  Los separadores de palabras de cada uno de los idiomas acortan el texto de forma distinta. Por ejemplo, un separador de palabras podría separar la cadena "dog-house" en "dog" "house" y otro en "dog-house". Por este motivo, las coincidencias y las categorías variarán en función del idioma especificado, ya que no solo son distintas las palabras sino también la longitud del documento. La diferencia de longitud del documento puede afectar a las categorías de todas las consultas.  
  
 Las estadísticas como `IndexRowCount` pueden variar enormemente. Por ejemplo, si un catálogo tiene 2.000 millones de filas en el índice maestro, un nuevo documento se indizará en un índice intermedio de la memoria y los rangos de dicho documento basados en el número de documentos en el índice almacenado en la memoria podrían desviarse de los rangos de los documentos del índice maestro. Por este motivo, tras realizar un llenado que dé como resultado la indización o reindización de un gran número de filas, se recomienda mezclar los índices en un índice maestro mediante la instrucción ALTER FULLTEXT CATALOG ... REORGANIZE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El motor de búsqueda de texto completo también mezclará automáticamente los índices basándose en parámetros como el número y el tamaño de los índices intermedios.  
  
 Los valores de `MaxOccurrence` se normalizan en 1 de 32 intervalos. Esto significa que, por ejemplo, un documento de 50 palabras se trata igual que un documento de 100 palabras. A continuación se muestra la tabla utilizada para la normalización. Como las longitudes de los documentos se encuentran en el intervalo entre los valores de tabla adyacentes 32 y 128, en la práctica se considera que tienen la misma longitud, 128 (32 < `docLength` <= 128).  
  
```  
{ 16, 32, 128, 256, 512, 725, 1024, 1450, 2048, 2896, 4096, 5792, 8192, 11585,   
16384, 23170, 28000, 32768, 39554, 46340, 55938, 65536, 92681, 131072, 185363,   
262144, 370727, 524288, 741455, 1048576, 2097152, 4194304 };  
  
```  
  
  
### <a name="ranking-of-containstable"></a>Categoría de CONTAINSTABLE  
 La clasificación de[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) usa el algoritmo siguiente:  
  
```  
StatisticalWeight = Log2( ( 2 + IndexedRowCount ) / KeyRowCount )  
Rank = min( MaxQueryRank, HitCount * 16 * StatisticalWeight / MaxOccurrence )  
```  
  
 Las coincidencias de frases se clasifican del mismo modo que las claves individuales, excepto en que `KeyRowCount` (número de filas que contienen la frase) se calcula y puede ser impreciso y superior al número real.  
  
 **Categoría de NEAR**  
  
 CONTAINSTABLE admite las consultas de dos o más términos de búsqueda que estén próximos, mediante la opción NEAR. El valor de rango de cada fila devuelta se basa en varios parámetros. Un factor de rango importante es el número total de coincidencias (o *aciertos*) en relación con la longitud del documento. Por ejemplo, si un documento de 100 palabras y un documento de 900 palabras contienen las mismas coincidencias, el de 100 palabras tiene un rango superior.  
  
 La longitud total de cada acierto en una fila también contribuirá al rango de esa fila en función de la distancia entre los términos de búsqueda primero y último de ese acierto. Cuanto menor sea la distancia, más contribuye el acierto al valor de rango de la fila. Si en una consulta de texto completo no se especifica un entero como la distancia máxima, un documento que solo tenga aciertos cuyas distancias sean mayores de 100 términos lógicos tendrá un rango de 0.  
  
 **Categoría de ISABOUT**  
  
 CONTAINSTABLE permite consultar los términos ponderados utilizando la opción ISABOUT. ISABOUT es lo que se denomina consulta de espacio vectorial en la terminología tradicional de recuperación de información. El algoritmo de clasificación predeterminado que se utiliza es Jaccard, una fórmula muy conocida. La clasificación se calcula para cada término de la consulta y se combina del modo que se describe a continuación.  
  
```  
ContainsRank = same formula used for CONTAINSTABLE ranking of a single term (above).  
Weight = the weight specified in the query for each term. Default weight is 1.  
WeightedSum = Σ[key=1 to n] ContainsRankKey * WeightKey  
Rank =  ( MaxQueryRank * WeightedSum ) / ( ( Σ[key=1 to n] ContainsRankKey^2 )   
      + ( Σ[key=1 to n] WeightKey^2 ) - ( WeightedSum ) )  
  
```  
  
  
### <a name="ranking-of-freetexttable"></a>Categoría de FREETEXTTABLE  
 La clasificación de[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) se basa en la fórmula de clasificación OKAPI BM25. Las consultas FREETEXTTABLE agregarán palabras a la consulta a través de la generación de formas con inflexión de las palabras originales de la consulta; estas palabras se tratan como palabras independientes sin ninguna relación especial con las palabras a partir de las cuales se generan. Los sinónimos que se generan con la característica de diccionario de sinónimos se tratan como términos independientes del mismo peso. Cada palabra de la consulta contribuye al rango.  
  
```  
Rank = Σ[Terms in Query] w ( ( ( k1 + 1 ) tf ) / ( K + tf ) ) * ( ( k3 + 1 ) qtf / ( k3 + qtf ) ) )  
Where:   
w is the Robertson-Sparck Jones weight.   
In simplified form, w is defined as:   
w = log10 ( ( ( r + 0.5 ) * ( N – R + r + 0.5 ) ) / ( ( R – r + 0.5 ) * ( n – r + 0.5 ) )  
N is the number of indexed rows for the property being queried.   
n is the number of rows containing the word.   
K is ( k1 * ( ( 1 – b ) + ( b * dl / avdl ) ) ).   
dl is the property length, in word occurrences.   
avdl is the average length of the property being queried, in word occurrences.   
k1, b, and k3 are the constants 1.2, 0.75, and 8.0, respectively.   
tf is the frequency of the word in the queried property in a specific row.   
qtf is the frequency of the term in the query.   
```  
  
  
## <a name="see-also"></a>Vea también  
 [Consultar con búsqueda de texto completo](query-with-full-text-search.md)  
  
  
