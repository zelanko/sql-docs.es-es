---
title: "Consulta con búsqueda de texto completo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
caps.latest.revision: 80
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5034ce123455c63718fb41b02450c14ca2f68a0b
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="query-with-full-text-search"></a>Consultar con búsqueda de texto completo

Escriba consultas de texto completo mediante los predicados de texto completo **CONTAINS** y **FREETEXT**, y las funciones de conjunto de filas **CONTAINSTABLE** y **FREETEXTTABLE** con la instrucción **SELECT**. En este tema, se proporcionan ejemplos de cada predicado y función, y lo ayuda a elegir cuál resulta más adecuado usar.

-   Use **CONTAINS** y **CONTAINSTABLE** para hacer coincidir palabras y frases.
-   Use **FREETEXT** y **FREETEXTTABLE** para hacer coincidir el significado, aunque no con la redacción exacta.

## <a name="examples_simple"></a> Ejemplos sencillos de cada predicado y función

### <a name="example---contains"></a>Ejemplo: CONTAINS  
 En este ejemplo se buscan todos los productos con un precio de `$80.99` que contengan la palabra `"Mountain"`.  
  
```tsql
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
### <a name="example---freetext"></a>Ejemplo: FREETEXT 
 En el siguiente ejemplo, se buscan todos los documentos que contengan palabras relacionadas con vital, safety y components.  
  
```tsql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>Ejemplo: CONTAINSTABLE  
 En el ejemplo siguiente se devuelven el identificador de descripción y la descripción de todos los productos para los que la columna **Description** contiene la palabra "aluminum" cerca de la palabra "light" o de la palabra "lightweight". Solo se devuelven las filas cuyo valor de rango sea igual o superior a 2.  
  
```tsql
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="example--freetexttable"></a>Ejemplo: FREETEXTTABLE  
 En el ejemplo siguiente se amplía una consulta FREETEXTTABLE para que devuelva primero las filas con clasificación superior y agregue la clasificación de cada fila a la lista de selección. Para especificar la consulta, debe saber que **ProductDescriptionID** es la columna de clave única de la tabla **ProductDescription** .  
  
```tsql 
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
A continuación se incluye una ampliación de la misma consulta en la que solo se devuelven las filas con un valor de rango de 10 o superior:  
  
```tsql  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  

## <a name="pick-the-best-predicate-or-function"></a>Elección el mejor predicado o función

`CONTAINS`/`CONTAINSTABLE` y `FREETEXT`/`FREETEXTTABLE` resultan de utilidad para diferentes tipos de coincidencias. La siguiente tabla lo ayudará a elegir el mejor predicado o función para la consulta.

Vea [Ejemplos sencillos de cada predicado y función](#examples_simple) y [Ejemplos de tipos de búsquedas específicos](#examples_specific) para consultar ejemplos. Vea también [Elementos que se pueden buscar](#supported).

| |CONTAINS/CONTAINSTABLE|FREETEXT/FREETEXTTABLE|
|---|---|---|
|**Tipo de consulta**|Coincidencia de palabras y frases individuales con coincidencias precisas o aproximadas (menos precisas).|Coincidencia de significado en lugar coincidencias literales con las palabras, frases u oraciones especificadas (la *cadena freetext*).<br/><br/>Se generarán coincidencias si se encuentra algún término o las formas de algún término en el índice de texto completo de una columna especificada.|
|**Más opciones de consulta**|Puede especificar la proximidad de las palabras que se encuentran a cierta distancia la una de la otra.<br/><br/>Puede devolver coincidencias ponderadas.<br/><br/>Puede usar una operación lógica para combinar condiciones de búsqueda. Para obtener más información, vea la sección [Uso de operadores booleanos (AND, OR y NOT)](#Using_Boolean_Operators) más adelante en este tema.|N/A|

## <a name="compare-predicates-and-functions"></a>Comparación de predicados y funciones

Los predicados `CONTAINS`/`FREETEXT` y las funciones de conjunto de filas `CONTAINSTABLE`/`FREETEXTTABLE` tienen una sintaxis y opciones diferentes. La siguiente tabla lo ayudará a elegir el mejor predicado o función para la consulta.

Vea [Ejemplos sencillos de cada predicado y función](#examples_simple) y [Ejemplos de tipos de búsquedas específicos](#examples_specific) para consultar ejemplos. Vea también [Elementos que se pueden buscar](#supported).

| |Predicados<br/>CONTAINS/FREETEXT|Funciones<br/>CONTAINSTABLE/FREETEXTTABLE|
|---|---|---|
|**Uso**|Use los **predicados** de texto completo CONTAINS y FREETEXT en la cláusula WHERE o HAVING de una instrucción SELECT.|Use las **funciones** de texto completo CONTAINSTABLE y FREETEXTTABLE a modo de nombre de nombre de tabla normal en la cláusula FROM de una instrucción SELECT.|
|**Más opciones de consulta**|Puede combinarlas con cualquier otro predicado de [!INCLUDE[tsql](../../includes/tsql-md.md)], como LIKE y BETWEEN.<br/><br/>Puede especificar una única columna, una lista de columnas o todas las columnas de la tabla que se vayan a buscar.<br/><br/>Opcionalmente, también puede especificar el lenguaje cuyos recursos se usarán en la consulta de texto completo para la lematización y la separación de palabras, las consultas del diccionario de sinónimos y la eliminación de palabras irrelevantes.|Tiene que especificar la tabla base para la búsqueda al usar cualquiera de estas funciones. Al igual que en los predicados, puede especificar una única columna, una lista de columnas o todas las columnas de la tabla en la que se va a buscar y, de forma opcional, el lenguaje cuyos recursos se utilizarán en la consulta de texto completo.<br/><br/>Normalmente, debe combinar los resultados de CONTAINSTABLE o FREETEXTTABLE con la tabla base. Para ello, necesita conocer el nombre de la columna de clave única. Esta columna, que existe en todas las tablas habilitadas para texto completo, se usa para aplicar las filas únicas de la tabla ( *columna de clave**única*). Para obtener más información sobre la columna de clave, vea [Create and Manage Full-Text Indexes](../../relational-databases/search/create-and-manage-full-text-indexes.md) (Crear y administrar índices de texto completo).|
|**Resultado**|Los predicados CONTAINS y FREETEXT devuelven un valor TRUE o FALSE que indica si una determinada fila coincide con la consulta de texto completo. Las filas que coinciden se devuelven en el conjunto de resultados.|Estas funciones devuelven una tabla con ninguna, una o varias filas que coinciden con la consulta de texto completo. La tabla devuelta solo contiene las filas de la tabla base que coinciden con los criterios de selección especificados en la condición de búsqueda de texto completo de la función.<br/><br/>Las consultas que usan una de estas funciones también devuelven un valor de clasificación por relevancia (RANK) y una clave de texto completo (KEY) para cada fila devuelta, tal y como se muestra a continuación.<br/><ul><li>Columna **KEY** La columna KEY devuelve valores únicos de las filas devueltas. La columna KEY se puede utilizar para especificar los criterios de selección.</li><li>Columna **RANK** La columna RANK contiene un *valor de clasificación* para cada fila que indica el grado de coincidencia de la fila con los criterios de selección. Cuanto mayor sea el valor de clasificación del texto o documento de una fila, mayor importancia tendrá la fila en la consulta de texto completo especificada. Tenga en cuenta que puede haber filas distintas con la misma clasificación. Puede limitar el número de coincidencias que se van a devolver con el parámetro opcional *top_n_by_rank* . Para obtener más información, vea [Limitar los resultados de la búsqueda con RANK](../../relational-databases/search/limit-search-results-with-rank.md).</li></ul>|
|**Opciones adicionales**|Se puede utilizar un nombre de cuatro partes en el predicado CONTAINS o FREETEXT para consultar columnas indizadas de texto completo de las tablas de destino en un servidor vinculado. Para preparar un servidor remoto para recibir consultas de texto completo, es necesario crear un índice de texto completo en las tablas y columnas de destino en el servidor remoto y, posteriormente, agregar el servidor remoto como un servidor vinculado.|N/A|
|**Más información**|Para obtener más información sobre la sintaxis y los argumentos de estos predicados, vea [CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [FREETEXT](../../t-sql/queries/freetext-transact-sql.md).|Para obtener más información sobre la sintaxis y los argumentos de estos predicados, vea [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) y [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md).|

##  <a name="supported"></a> Elementos que se pueden buscar

En la siguiente tabla, se describen los tipos de palabras y frases que se pueden buscar.
  
|Formato de los términos de la consulta|Description|Es compatible con|  
|----------------------|-----------------|------------------|  
|Una o varias palabras o frases específicas<br/>(*término simple*)|Por ejemplo, "croissant" es una palabra y "café au lait" es una frase. Las palabras y frases como estas se denominan términos simples.<br /><br /> En la búsqueda de texto completo, una *palabra* (o *token*) es una cadena cuyos límites se identifican mediante los separadores de palabras adecuados, siguiendo las normas lingüísticas del idioma especificado. Una *frase* válida está formada por varias palabras con o sin signos de puntuación entre ellas.<br /><br /> Para obtener más información, vea la sección [Buscar palabras o frases específicas (término simple)](#Simple_Term)más adelante en este tema.|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) buscan una coincidencia exacta para la frase.<br /><br /> [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) y [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) dividen la frase en palabras independientes.|  
|Una palabra o frase cuyas palabras empiezan por un texto determinado<br/>(*término de prefijo*)|Con un solo término de prefijo, cualquier palabra inicial con el término especificado formará parte del conjunto de resultados. Por ejemplo, el término "auto*" coincide con "automático", "automóvil", etc.<br /><br /> En una frase, cada palabra de la misma se considera un término de prefijo. Por ejemplo, el término en inglés "auto tran\*" coincide con "automatic transmission" y "automobile transducer", pero no con "automatic motor transmission".<br /><br /> Un *término de prefijo* hace referencia a una cadena que se anexa al principio de una palabra para generar una palabra derivada o una forma con inflexión.<br /><br /> Para obtener más información, vea la sección [Realizar búsquedas de prefijos (término de prefijo)](#Prefix_Term)más adelante en este tema.|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  
|Formas con inflexión de una palabra determinada<br/>(*término de generación: con inflexión*)|Por ejemplo, busque la forma con inflexión de la palabra "drive". Si hay varias filas en la tabla que incluyan las palabras "drive", "drives", "drove", "driving" y "driven", todas estarían en el conjunto de resultados porque cada una de estas palabras se puede generar a partir de la palabra "drive".<br /><br /> Las *formas con inflexión* son los distintos tiempos y conjugaciones de un verbo o las formas singular y plural de un nombre. <br /><br /> Para obtener más información, vea la sección [Buscar la forma con inflexión de una palabra determinada (término de generación)](#Inflectional_Generation_Term)más adelante en este tema.|[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) y [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) buscan términos con inflexión de todas las palabras especificadas de forma predeterminada.<br /><br /> [CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) admiten un argumento INFLECTIONAL opcional.|  
|Formas sinónimas de una palabra determinada<br/>(*término de generación: diccionario de sinónimos*)|Por ejemplo, si una entrada, "{car, automobile, truck, van}", se agrega a un diccionario de sinónimos, puede buscar la forma sinónima de la palabra "car". Todas las filas de la tabla consultada que incluyen las palabras "automobile", "truck", "van" o "car" aparecen en el conjunto de resultados porque cada una de estas palabras pertenece al conjunto de expansión de sinónimos de la palabra "car".<br /><br />Un *diccionario de sinónimos* define los sinónimos especificados por el usuario para los términos.<br /><br />  Para obtener información sobre la estructura de archivos de sinónimos, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).|[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) y [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) usan el diccionario de sinónimos de forma predeterminada.<br /><br /> [CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) admiten un argumento THESAURUS opcional.|  
|Una palabra o frase que esté cerca de otra palabra o frase<br/>(*término de proximidad*)|Por ejemplo, quizá desee buscar las filas en las que la palabra "ice" esté relacionada con la palabra "hockey" o en las que la frase "ice skating" esté relacionadas con la frase "ice hockey".<br /><br /> Un *término de proximidad* indica palabras o frases cercanas entre sí. Asimismo, puede especificar el número máximo de términos de no búsqueda que separen los términos de búsqueda primero y último. Además, puede buscar palabras o frases en cualquier orden o en el orden en el que las especifique.<br /><br /> Para obtener más información, vea [Buscar palabras cerca de otra palabra con NEAR](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md).|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) y [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  
|Palabras o frases que usan valores ponderados<br/>(*término ponderado*)|Por ejemplo, en una consulta en la que se buscan varios términos, puede asignar a cada palabra de búsqueda un valor ponderado que indique su importancia en relación con otras palabras en la condición de búsqueda. Los resultados para este tipo de consulta devuelven las filas más relevantes primero, según la ponderación relativa que ha asignado a las palabras de búsqueda. Los conjuntos de resultados contienen documentos o filas con cualquiera de los términos especificados (o el contenido entre ellos); sin embargo, algunos resultados se consideran más importantes que otros debido a la variación en los valores ponderados asociados a los diferentes términos buscados.<br /><br /> Un *valor de ponderación* indica el grado de importancia de cada palabra y frase dentro de un conjunto de palabras y frases. El valor 0,0 es el peso más pequeño disponible, y el valor 1,0 es el peso más grande.<br /><br /> Para obtener más información, vea la sección [Buscar palabras o frases con valores ponderados (término ponderado)](#Weighted_Term)más adelante en este tema.|[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  

## <a name="examples_specific"></a> Ejemplos de tipos de búsquedas específicos

###  <a name="Simple_Term"></a> Búsqueda de una palabra o frase específica (término simple)  
 Puede usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) para buscar una frase específica en una tabla. Por ejemplo, si quiere buscar en la tabla **ProductReview** de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] todos los comentarios sobre un producto que contengan la frase "learning curve", puede usar el predicado CONTAINS del siguiente modo:  
  
```tsql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 La condición de búsqueda, en este caso "learning curve", puede ser bastante compleja y estar formada por uno o varios términos.  
  
###  <a name="Prefix_Term"></a> Búsqueda de una palabra con prefijo (término de prefijo)  
 Puede usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md) o [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para buscar palabras o frases con un prefijo especificado. Se devuelven todas las entradas de la columna que contenga el texto que comience por el prefijo especificado. Por ejemplo, para buscar todas las filas que contengan el prefijo `top`-, como en `top``ple`, `top``ping`y `top`. La consulta sería la siguiente:  
  
```tsql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Se devuelve todo el texto que coincida con el texto especificado antes del asterisco (*). Si no se delimitan el texto completo y el asterisco con comillas dobles, como en `CONTAINS (DESCRIPTION, 'top*')`, en la búsqueda de texto completo no se considerará que el asterisco es un comodín.  
  
 Cuando el término prefijo es una frase, cada token de los que componen la frase se considera como un término prefijo separado. Se devuelven todas las filas que contienen palabras que empiezan con los términos prefijos. Por ejemplo, el término de prefijo "light bread*" buscará filas que contengan el texto "light breaded", "lightly breaded" o "light bread", pero no devolverá "lightly toasted bread".  
  
###  <a name="Inflectional_Generation_Term"></a> Búsqueda de las formas con inflexión de una palabra específica (término de generación)  
Puede usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) para buscar todos los tiempos y conjugaciones de un verbo o las formas tanto singular como plural de un nombre (búsqueda con inflexión). O bien, los sinónimos de una palabra especificada (búsqueda de diccionario de sinónimos).  
  
En el siguiente ejemplo se busca cualquier forma de "foot" ("foot", "feet", etc.) en la columna `Comments` de la tabla `ProductReview` de la base de datos `AdventureWorks` .  
  
```tsql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
La búsqueda de texto completo usa *lematizadores*, que permiten buscar los distintos tiempos y conjugaciones de un verbo o las formas tanto singular como plural de un nombre. Para obtener más información sobre los lematizadores, vea [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
   
###  <a name="Weighted_Term"></a> Búsqueda de palabras o frases mediante valores ponderados (término ponderado)  
Puede usar [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para buscar palabras o frases, y especificar un valor de ponderación. La ponderación, medida como número comprendido entre 0,0 y 1,0, indica la importancia de cada palabra y frase en un conjunto de palabras y frases. Una ponderación de 0,0 es la más baja y una ponderación de 1,0, la más alta.  
  
En el ejemplo siguiente se muestra una consulta que busca las direcciones de todos los clientes, mediante valores ponderados, en las que cualquier texto que comience por la cadena "Bay" contenga "Street" o "View". Los resultados asignan un rango superior a las filas que contengan más palabras de las especificadas.  
  
```tsql  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Se puede usar un término ponderado junto con cualquier término simple, de prefijo, de generación o de proximidad.  

##  <a name="Using_Boolean_Operators"></a> Uso de operadores booleanos (AND, OR y NOT)
 
El predicado CONTAINS y la función CONTAINSTABLE usan las mismas condiciones de búsqueda. Ambos admiten que se combinen varios términos de búsqueda con los operadores booleanos AND, OR y NOT para realizar operaciones lógicas. Por ejemplo, puede usar AND para buscar filas que contienen "latte" y "New York-style bagel". También puede, por ejemplo, utilizar AND NOT para buscar las filas que contienen "bagel" pero no contienen "cream cheese".  
  
Por el contrario, FREETEXT y FREETEXTTABLE tratan los términos booleanos como las palabras que se van a buscar.  
  
 Para obtener información sobre la combinación de CONTAINS con otros predicados que usan los operadores lógicos AND, OR y NOT, vea [Condiciones de búsqueda &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, se usa el predicado CONTAINS para buscar las descripciones en las que el identificador de la descripción no es igual a 5 y la descripción contiene las palabras "Aluminum" y "spindle". La condición de búsqueda usa el operador booleano AND. En el siguiente ejemplo, se usa la tabla ProductDescription de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```tsql  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
##  <a name="Additional_Considerations"></a> Más opciones de consulta

 Al escribir consultas de texto completo, también puede especificar las siguientes opciones.
  
-   El **idioma**, con la opción **LANGUAGE**. Muchos términos de consulta dependen en gran medida del comportamiento del separador de palabras. Para asegurarse de que usa el archivo del separador de palabras (y lematizador) y del diccionario de sinónimos correcto, se recomienda especificar la opción LANGUAGE. Para obtener más información, vea [Elegir un idioma al crear un índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  

-   **Distinción de mayúsculas y minúsculas**. Las consultas de búsqueda de texto completo no distinguen mayúsculas de minúsculas. Sin embargo, en japonés, hay muchas ortografías fonéticas en las que el concepto de normalización ortográfica implica no distinguir las mayúsculas de las minúsculas (por ejemplo, las letras kana no tienen mayúsculas y minúsculas). Este tipo de normalización ortográfica no se admite.  

-   **Palabras irrelevantes**. Al definir una consulta de texto completo, el motor de texto completo descarta las palabras irrelevantes de los criterios de búsqueda. Las palabras irrelevantes son aquellas como "a", "and", "is" o "the", que suelen aparecer con frecuencia pero que normalmente no ayudan en la búsqueda de un texto determinado. Las palabras irrelevantes se muestran en una lista de palabras irrelevantes. Cada índice de texto completo está asociado a una lista de palabras irrelevantes concreta, que determina qué palabras irrelevantes se omiten de la consulta o del índice en el momento de la indización. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **Diccionario de sinónimos**. Las consultas FREETEXT y FREETEXTTABLE usan de forma predeterminada el diccionario de sinónimos. CONTAINS y CONTAINSTABLE admiten un argumento THESAURUS opcional. Para obtener más información, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).
  
##  <a name="tokens"></a> Comprobación de los resultados de la tokenización

Después de aplicar una combinación determinada de separador de palabras, diccionario de sinónimos y lista de palabras irrelevantes a una consulta, puede ver los resultados de la tokenización mediante la vista de administración dinámica **sys.dm_fts_parser**. Para obtener más información, vea [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Crear consultas de búsqueda de texto completo &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [Mejorar el rendimiento de las consultas de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
 
