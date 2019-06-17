---
title: Consulta con búsqueda de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 280f4bc3c20fb65be24ace423f69982ad96bfbff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011111"
---
# <a name="query-with-full-text-search"></a>Consultar con búsqueda de texto completo
  Para definir búsquedas de texto completo, las consultas de texto completo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan los predicados (CONTAINS y FREETEXT) y las funciones (CONTAINSTABLE y FREETEXTTABLE) de texto completo. Estas funciones y predicados admiten la sintaxis [!INCLUDE[tsql](../../includes/tsql-md.md)] enriquecida, que es compatible con diversos formatos de términos de consulta. Para escribir consultas de texto completo, es necesario saber cuándo y cómo deben usarse estos predicados y funciones.  
  
##  <a name="OV_ft_predicates"></a> Información general sobre el texto predicados (CONTAINS y FREETEXT)  
 Los predicados de CONTAINS y FREETEXT devuelven un valor TRUE o FALSE. Se pueden utilizar exclusivamente para especificar los criterios de selección a la hora de determinar si una fila determinada coincide con la consulta de texto completo. Las filas que coinciden se devuelven en el conjunto de resultados. CONTAINS y FREETEXT se especifican en la cláusula WHERE o HAVING de una instrucción SELECT. Pueden combinarse con cualquier otro predicado [!INCLUDE[tsql](../../includes/tsql-md.md)] , como LIKE y BETWEEN.  
  
> [!NOTE]  
>  Para obtener información sobre la sintaxis y los argumentos de estos predicados, vea [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql) y [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql).  
  
 Al utilizar CONTAINS o FREETEXT, se puede especificar una única columna, una lista de columnas o todas las columnas de la tabla que se van a buscar. También se puede especificar el lenguaje cuyos recursos se utilizarán en la consulta de texto completo para la lematización y separación de palabras, las consultas del diccionario de sinónimos y la eliminación de palabras irrelevantes.  
  
 CONTAINS y FREETEXT son útiles para diferentes tipos de coincidencias, tal y como se detalla a continuación:  
  
-   Utilice CONTAINS (o CONTAINSTABLE) para obtener coincidencias precisas o aproximadas (menos precisas) de palabras o frases, para obtener la proximidad de las palabras que se encuentran a cierta distancia de otra o para obtener coincidencias ponderadas. Al utilizar CONTAINS, debe establecer al menos una condición de búsqueda que especifique el texto que está buscando y las condiciones que determinan las coincidencias.  
  
     Puede utilizar una operación lógica entre las condiciones de búsqueda. Para obtener más información, consulte [uso de operadores booleanos: AND, OR y AND NOT (en CONTAINS y CONTAINSTABLE)](#Using_Boolean_Operators), más adelante en este tema.  
  
-   Use FREETEXT (o FREETEXTTABLE) para buscar coincidencias de significado en lugar de coincidencias literales con las palabras, frases o sintagmas especificados (la *cadena Freetext*). Se generarán coincidencias si se encuentra algún término o las formas de algún término en el índice de texto completo de una columna especificada.  
  
 Se puede utilizar un nombre de cuatro partes en el predicado CONTAINS o FREETEXT para consultar columnas indizadas de texto completo de las tablas de destino en un servidor vinculado. Para preparar un servidor remoto para recibir consultas de texto completo, es necesario crear un índice de texto completo en las tablas y columnas de destino en el servidor remoto y, posteriormente, agregar el servidor remoto como un servidor vinculado.  
  
> [!NOTE]  
>  Los predicados de texto completo no se permiten en la [cláusula OUTPUT](/sql/t-sql/queries/output-clause-transact-sql) cuando el nivel de compatibilidad de la base de datos se establece en 100.  
  
 
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. Usar CONTAINS con <simple_term>  
 En este ejemplo se buscan todos los productos con un precio de `$80.99` que contengan la palabra `"Mountain"`.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>b. Usar FREETEXT para buscar palabras que contengan los valores de carácter especificados  
 En el siguiente ejemplo se buscan todos los documentos que contienen las palabras relacionadas con vital, safety, components.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> Información general de las funciones de texto completo (CONTAINSTABLE y FREETEXTTABLE)  
 Las referencias a las funciones CONTAINSTABLE y FREETEXTTABLE se establecen como un nombre de tabla normal en la cláusula FROM de una instrucción SELECT. Devuelven una tabla con ninguna, una o varias filas que coinciden con la consulta de texto completo. La tabla devuelta solo contiene las filas de la tabla base que coinciden con los criterios de selección especificados en la condición de búsqueda de texto completo de la función.  
  
> [!NOTE]  
>  Para obtener información sobre la sintaxis y los argumentos de estas funciones, vea [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql) y [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql).  
  
 Las consultas que utilizan una de estas funciones devuelven un valor de clasificación por relevancia (RANK) y una clave de texto completo (KEY) para cada fila, tal y como se muestra a continuación:  
  
-   Columna KEY  
  
     La columna KEY devuelve valores únicos de las filas devueltas. La columna KEY se puede utilizar para especificar los criterios de selección.  
  
-   Columna RANK  
  
     La columna RANK contiene un *valor de clasificación* para cada fila que indica el grado de coincidencia de la fila con los criterios de selección. Cuanto mayor sea el valor de clasificación del texto o documento de una fila, mayor importancia tendrá la fila en la consulta de texto completo especificada. Tenga en cuenta que puede haber filas distintas con la misma clasificación. Puede limitar el número de coincidencias que se van a devolver con el parámetro opcional *top_n_by_rank* . Para obtener más información, vea [Limitar los resultados de la búsqueda con RANK](limit-search-results-with-rank.md).  
  
 Cuando utilice una de estas funciones, debe especificar la tabla base en la que se realizará la búsqueda de texto completo. Al igual que en los predicados, puede especificar una única columna, una lista de columnas o todas las columnas de la tabla en la que se va a buscar y, de forma opcional, el lenguaje cuyos recursos se utilizarán en la consulta de texto completo.  
  
 CONTAINSTABLE es útil para los mismos tipos de coincidencias que CONTAINS, mientras que FREETEXTTABLE es útil para los mismos tipos de coincidencias que FREETEXT. Para obtener más información, vea [Información general de los predicados de texto completo (CONTAINS y FREETEXT)](#OV_ft_predicates), anteriormente en este tema. Cuando se ejecutan consultas que utilizan las funciones CONTAINSTABLE y FREETEXTTABLE, se deben combinar de forma explícita las filas que se devuelven con las filas de la tabla base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Normalmente, es necesario combinar el resultado de CONTAINSTABLE o FREETEXTTABLE con la tabla base. En esos casos, necesita conocer el nombre de la columna de clave única. Esta columna, que existe en todas las tablas habilitadas para texto completo, se usa para aplicar las filas únicas de la tabla (*columna de clave**única*). Para obtener más información, vea [Administrar índices de texto completo](../indexes/indexes.md).  
  
 
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="a-using-containstable"></a>A. Usar CONTAINSTABLE  
 En el ejemplo siguiente se devuelven el identificador de descripción y la descripción de todos los productos para los que la columna **Description** contiene la palabra "aluminum" cerca de la palabra "light" o de la palabra "lightweight". Solo se devuelven las filas cuyo valor de rango sea igual o superior a 2.  
  
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
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>b. Usar FREETEXTTABLE  
 En el ejemplo siguiente se amplía una consulta FREETEXTTABLE para que devuelva primero las filas con clasificación superior y agregue la clasificación de cada fila a la lista de selección. Para especificar la consulta, debe saber que **ProductDescriptionID** es la columna de clave única para el `ProductDescription` tabla.  
  
```  
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
  
```  
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
  
 
  
##  <a name="Using_Boolean_Operators"></a> Usar los operadores booleanos - y, OR y no - en CONTAINS y CONTAINSTABLE  
 El predicado CONTAINS y la función CONTAINSTABLE usan las mismas condiciones de búsqueda. Ambos admiten que se combinen varias condiciones de búsqueda mediante el uso de operadores booleanos: AND, OR y no-para realizar operaciones lógicas. Por ejemplo, puede utilizar AND para buscar filas que contienen "latte" y "New York-style bagel". También puede, por ejemplo, utilizar AND NOT para buscar las filas que contienen "bagel" pero no contienen "cream cheese".  
  
> [!NOTE]  
>  Por el contrario, FREETEXT y FREETEXTTABLE tratan los términos booleanos como las palabras que se van a buscar.  
  
 Para obtener información sobre la combinación de CONTAINS con otros predicados que usan los operadores lógicos AND, OR y NOT, vea [Condiciones de búsqueda &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se utiliza la tabla ProductDescription de la base de datos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] . La consulta usa el predicado CONTAINS para buscar las descripciones en las que el identificador de la descripción no es igual a 5 y la descripción contiene las palabras "Aluminum" y "spindle". La condición de búsqueda usa el operador booleano AND.  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> Consideraciones adicionales para consultas de texto completo  
 Al escribir consultas de texto completo hay que tener en cuenta también lo siguiente:  
  
-   La opción LANGUAGE  
  
     Muchos términos de consulta dependen en gran medida del comportamiento del separador de palabras. Para asegurarse de que usa el archivo del separador de palabras (y lematizador) y del diccionario de sinónimos correcto, se recomienda especificar la opción LANGUAGE. Para obtener más información, vea [Elegir un idioma al crear un índice de texto completo](choose-a-language-when-creating-a-full-text-index.md).  
  
-   Palabras irrelevantes  
  
     Al definir una consulta de texto completo, el motor de texto completo descarta las palabras irrelevantes de los criterios de búsqueda. Las palabras irrelevantes son aquellas como "a", "and", "is" o "the", que suelen aparecer con frecuencia pero que normalmente no ayudan en la búsqueda de un texto determinado. Las palabras irrelevantes se muestran en una lista de palabras irrelevantes. Cada índice de texto completo está asociado a una lista de palabras irrelevantes concreta, que determina qué palabras irrelevantes se omiten de la consulta o del índice en el momento de la indización. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](full-text-search.md).  
  
-   El diccionario de sinónimos  
  
     Las consultas FREETEXT y FREETEXTTABLE usan de forma predeterminada el diccionario de sinónimos. CONTAINS y CONTAINSTABLE admiten un argumento THESAURUS opcional.  
  
-   Distinción de mayúsculas y minúsculas  
  
     Las consultas de búsqueda de texto completo no distinguen mayúsculas de minúsculas. Sin embargo, en japonés, hay muchas ortografías fonéticas en las que el concepto de normalización ortográfica implica no distinguir las mayúsculas de las minúsculas (por ejemplo, las letras kana no tienen mayúsculas y minúsculas). Este tipo de normalización ortográfica no se admite.  
  

  
##  <a name="varbinary"></a> Consultar varbinary (max) y las columnas xml  
 Si una columna `varbinary(max)`, `varbinary` o `xml` está indizada con texto completo, se puede consultar usando los predicados de texto completo (CONTAINS y FREETEXT) y las funciones (CONTAINSTABLE y FREETEXTTABLE), igual que cualquier otra columna indizada de texto completo.  
  
> [!IMPORTANT]  
>  La búsqueda de texto completo también funciona con las columnas de imagen. Sin embargo, el tipo de datos `image` se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar este tipo de datos en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente lo utilizan. En su lugar, use el tipo de datos `varbinary(max)`.  
  
### <a name="varbinarymax-or-varbinary-data"></a>datos varbinary(máximo) o varbinary  
 Una sola columna `varbinary(max)` o `varbinary` puede almacenar muchos tipos de documentos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite cualquier tipo de documento para el que tenga un filtro instalado que esté disponible en el sistema operativo. La extensión de archivo del documento identifica el tipo de cada documento. Por ejemplo, para la extensión de archivo .doc, la búsqueda de texto completo utiliza el filtro que admite los documentos de Microsoft Word. Para obtener una lista de los tipos de documentos disponibles, consulte la vista de catálogo [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) .  
  
 Observe que el motor de búsqueda de texto completo puede aprovechar los filtros existentes que se instalan en el sistema operativo. Para poder utilizar los separadores de palabras, los lematizadores y los filtros del sistema operativo, debe cargarlos en la instancia del servidor, como sigue:  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 Para crear un índice de texto completo en una columna `varbinary(max)`, el motor de búsqueda de texto completo necesita acceso a las extensiones de archivo de los documentos en la columna `varbinary(max)`. Esta información debe estar almacenada en una columna de la tabla, denominada columna de tipo, que debe estar asociada a la columna `varbinary(max)` en el índice de texto completo. Al indizar un documento, el motor de búsqueda de texto completo usa la extensión de archivo de la columna de tipo para identificar qué filtro usar.  
  
 
  
### <a name="xml-data"></a>Datos xml  
 Una columna del tipo de datos `xml` solo almacena los documentos y fragmentos XML, y solo se usa el filtro XML para los documentos. Por consiguiente, una columna de tipo es innecesaria. En las columnas `xml`, el índice de texto completo indiza el contenido de los elementos XML, pero omite el formato XML. Los valores de los atributos se incluyen en el índice de texto completo a menos que sean valores numéricos. Las etiquetas de elemento se utilizan como límites de token. Se admiten fragmentos y documentos con formato XML o HTML correcto que contengan varios idiomas.  
  
 Para obtener más información sobre cómo consultar con un `xml` columna, vea [usar la búsqueda de texto completo con columnas XML](../xml/use-full-text-search-with-xml-columns.md).  
  
 
  
##  <a name="supported"></a> Formatos admitidos de términos de consulta  
 En esta sección se resume la compatibilidad que proporcionan los predicados de texto completo y las funciones de valores de conjunto de filas para cada formato de consulta.  
  
> [!NOTE]  
>  Para obtener la sintaxis de un término de consulta determinado, haga clic en los vínculos correspondientes de la columna **Es compatible con** de la siguiente tabla.  
  
|Formato de los términos de la consulta|Descripción|Es compatible con|  
|----------------------|-----------------|------------------|  
|Una o varias palabras o frases específicas (*término simple*)|En la búsqueda de texto completo, una palabra (o *token*) es una cadena cuyos límites se identifican mediante los separadores de palabras adecuados, siguiendo las reglas lingüísticas del idioma especificado. Una frase válida está formada por varias palabras con o sin signos de puntuación entre ellas.<br /><br /> Por ejemplo, "croissant" es una palabra y "esté?? AU lait"es una frase. Las palabras y frases como estas se denominan términos simples.<br /><br /> Para obtener más información, vea la sección [Buscar palabras o frases específicas (término simple)](#Simple_Term)más adelante en este tema.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) buscan una coincidencia exacta para la frase.<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) y [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) dividen la frase en palabras independientes.|  
|Una palabra o frase cuyas palabras empiezan con un texto determinado (*término de prefijo*)|Un término de prefijo hace referencia a una cadena que se anexa al principio de una palabra para generar una palabra derivada o una forma con inflexión.<br /><br /> Con un solo término de prefijo, cualquier palabra inicial con el término especificado formará parte del conjunto de resultados. Por ejemplo, el término "auto*" coincide con "automático", "automóvil", etc.<br /><br /> En una frase, cada palabra de la misma se considera un término de prefijo. Por ejemplo, el término en inglés "auto tran\*" coincide con "automatic transmission" y "automobile transducer", pero no con "automatic motor transmission".<br /><br /> Para obtener más información, vea la sección [Realizar búsquedas de prefijos (término de prefijo)](#Prefix_Term)más adelante en este tema.|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Formas con inflexión de una palabra determinada (*generación con inflexión término*)|Las formas con inflexión son los distintos tiempos y conjugaciones de un verbo o las formas singular y plural de un nombre. Por ejemplo, busque la forma con inflexión de la palabra "drive". Si hay varias filas en la tabla que incluyan las palabras "drive", "drives", "drove", "driving" y "driven", todas estarían en el conjunto de resultados porque cada una de estas palabras se puede generar a partir de la palabra "drive".<br /><br /> Para obtener más información, vea la sección [Buscar la forma con inflexión de una palabra determinada (término de generación)](#Inflectional_Generation_Term)más adelante en este tema.|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) y [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) buscan términos con inflexión de todas las palabras especificadas de forma predeterminada.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) admiten un argumento INFLECTIONAL opcional.|  
|Sinónimas de una palabra determinada (*término de generación: diccionario de sinónimos*)|Un diccionario de sinónimos define los sinónimos especificados por el usuario para los términos. Por ejemplo, si una entrada, "{car, automobile, truck, van}", se agrega a un diccionario de sinónimos, puede buscar la forma sinónima de la palabra "car". Todas las filas de la tabla consultada que incluyen las palabras "automobile", "truck", "van" o "car" aparecen en el conjunto de resultados porque cada una de estas palabras pertenece al conjunto de expansión de sinónimos de la palabra "car".<br /><br /> Para obtener información sobre la estructura de archivos de sinónimos, vea [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) y [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) usan el diccionario de sinónimos de forma predeterminada.<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) admiten un argumento THESAURUS opcional.|  
|Una palabra o frase que esté cerca de otra palabra o frase (*término de proximidad*)|Un término de proximidad indica palabras o frases relacionadas entre sí. Asimismo, puede especificar el número máximo de términos de no búsqueda que separen los términos de búsqueda primero y último. Además, puede buscar palabras o frases en cualquier orden o en el orden en el que las especifique.<br /><br /> Por ejemplo, quizá desee buscar las filas en las que la palabra "ice" esté relacionada con la palabra "hockey" o en las que la frase "ice skating" esté relacionadas con la frase "ice hockey".<br /><br /> Para obtener más información, vea [Buscar palabras cerca de otra palabra con NEAR](search-for-words-close-to-another-word-with-near.md).|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|Palabras o frases que usan valores ponderados (*término ponderado*)|Valor de ponderación que indica el grado de importancia de cada palabra y frase dentro de un conjunto de palabras y frases. El valor 0,0 es el peso más pequeño disponible, y el valor 1,0 es el peso más grande.<br /><br /> Por ejemplo, en una consulta en la que se buscan varios términos, puede asignar a cada palabra de búsqueda un valor ponderado que indique su importancia en relación con otras palabras en la condición de búsqueda. Los resultados para este tipo de consulta devuelven las filas más relevantes primero, según la ponderación relativa que ha asignado a las palabras de búsqueda. Los conjuntos de resultados contienen documentos o filas con cualquiera de los términos especificados (o el contenido entre ellos); sin embargo, algunos resultados se consideran más importantes que otros debido a la variación en los valores ponderados asociados a los diferentes términos buscados.<br /><br /> Para obtener más información, vea la sección [Buscar palabras o frases con valores ponderados (término ponderado)](#Weighted_Term)más adelante en este tema.|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> Buscar palabra o frase (término Simple) específica  
 Puede usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)o [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) para buscar una frase específica en una tabla. Por ejemplo, si desea buscar en la tabla `ProductReview` de la base de datos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] todos los comentarios acerca de un producto que contengan la frase "learning curve", puede utilizar el predicado CONTAINS del siguiente modo:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 La condición de búsqueda, en este caso "learning curve", puede ser bastante compleja y estar formada por uno o varios términos.  
  
 
  
###  <a name="Prefix_Term"></a> Realizar búsquedas de prefijos (término de prefijo)  
 Puede usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql) o [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para buscar palabras o frases con un prefijo especificado. Se devuelven todas las entradas de la columna que contenga el texto que comience por el prefijo especificado. Por ejemplo, para buscar todas las filas que contengan el prefijo `top`-, como en `top``ple`, `top``ping`y `top`. La consulta sería la siguiente:  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Se devuelve todo el texto que coincida con el texto especificado antes del asterisco (*). Si no se delimitan el texto completo y el asterisco con comillas dobles, como en `CONTAINS (DESCRIPTION, 'top*')`, en la búsqueda de texto completo no se considerará que el asterisco es un comodín.  
  
 Cuando el término prefijo es una frase, cada token de los que componen la frase se considera como un término prefijo separado. Se devuelven todas las filas que contienen palabras que empiezan con los términos prefijos. Por ejemplo, el término de prefijo "light bread*" buscará filas que contengan el texto "light breaded", "lightly breaded" o "light bread", pero no devolverá "lightly toasted bread".  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> Buscar formas con inflexión de una palabra determinada (término de generación)  
 Puede usar [CONTAINS](/sql/t-sql/queries/contains-transact-sql), [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql), [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)o [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) para buscar todos los tiempos y conjugaciones de un verbo o las formas tanto singular como plural de un nombre (búsqueda con inflexión). O bien, los sinónimos de una palabra especificada (búsqueda de diccionario de sinónimos).  
  
 En el siguiente ejemplo se busca cualquier forma de "foot" ("foot", "feet", etc.) en la columna `Comments` de la tabla `ProductReview` de la base de datos `AdventureWorks` .  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  La búsqueda de texto completo usa lematizadores, que permiten buscar los distintos tiempos y conjugaciones de un verbo o las formas tanto singular como plural de un nombre. Para obtener más información sobre los lematizadores, vea [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  

  
###  <a name="Weighted_Term"></a> Buscar palabras o frases con valores ponderados (término ponderado)  
 Puede usar [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) para buscar palabras o frases, y especificar un valor de ponderación. La ponderación, medida como número comprendido entre 0,0 y 1,0, indica la importancia de cada palabra y frase en un conjunto de palabras y frases. Una ponderación de 0,0 es la más baja y una ponderación de 1,0, la más alta.  
  
 En el ejemplo siguiente se muestra una consulta que busca las direcciones de todos los clientes, mediante valores ponderados, en las que cualquier texto que comience por la cadena "Bay" contenga "Street" o "View". Los resultados asignan un rango superior a las filas que contengan más palabras de las especificadas.  
  
```  
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
  

  
##  <a name="tokens"></a> Ver el resultado de la tokenización de un separador de palabras, diccionario de sinónimos y combinación de la lista de palabras irrelevantes  
 Después de aplicar una combinación determinada de separador de palabras, diccionario de sinónimos y lista de palabras irrelevantes a la entrada de una cadena de consulta, puede ver el resultado de la tokenización mediante la vista de administración dinámica **sys.dm_fts_parser**. Para obtener más información, vea [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 
  
## <a name="see-also"></a>Vea también  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Crear consultas de búsqueda de texto completo &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [Mejorar el rendimiento de las consultas de texto completo](improve-the-performance-of-full-text-queries.md)  
  
  
