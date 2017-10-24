---
title: FREETEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREETEXT
- FREETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXT predicate (Transact-SQL)
- words in predicate [full-text search]
- column searches [full-text search]
ms.assetid: 2f199d3c-440e-4bcf-bdb5-82bb3994005d
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48c7ce4788a0c5da0b22e80ab1dc366091c25f97
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="freetext-transact-sql"></a>FREETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Es un predicado utilizado en el [!INCLUDE[tsql](../../includes/tsql-md.md)] [cláusula WHERE](../../t-sql/queries/where-transact-sql.md) de un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción SELECT para realizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] búsqueda de texto completo en texto completo indizadas las columnas que contienen tipos de datos basados en caracteres. Este predicado busca valores que coincidan con el significado y no solo con la redacción exacta de las palabras en la condición de búsqueda. Cuando se utiliza FREETEXT, el motor de consultas de texto completo realiza internamente las siguientes acciones en el *freetext_string*, asigna cada términos un peso y busca las coincidencias:  
  
-   Separa la cadena en palabras individuales basándose en límites de palabras (separación de palabras).  
  
-   Genera formas no flexionadas de las palabras (lematización).  
  
-   Identifica una lista de expansiones o reemplazos de los términos basándose en coincidencias en el diccionario de sinónimos.  
  
> [!NOTE]  
>  Para obtener información acerca de las formas de búsquedas de texto completo que son compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FREETEXT ( { column_name | (column_list) | * }   
          , 'freetext_string' [ , LANGUAGE language_term ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_name*  
 Es el nombre de una o varias columnas indizadas de texto completo de la tabla especificada en la cláusula FROM. Las columnas pueden ser de tipo **char**, **varchar**, **nchar**, **nvarchar**, **texto**, **ntext**, **imagen**, **xml**, **varbinary**, o **varbinary (max)**.  
  
 *column_list*  
 Indica que se pueden especificar varias columnas, separadas por una coma. *column_list* debe ir entre paréntesis. A menos que *language_term* se especifica, el idioma de todas las columnas de *column_list* debe ser el mismo.  
  
 \*  
 Especifica que todas las columnas que se han registrado para la búsqueda de texto completo se deben usar para buscar el determinado *freetext_string*. Si más de una tabla está en la cláusula FROM, \* debe calificar el nombre de tabla. A menos que *language_term* se especifica, el idioma de todas las columnas de la tabla debe ser el mismo.  
  
 *freetext_string*  
 Es el texto que desea buscar en el *column_name*. Se puede escribir cualquier texto, incluidas palabras, frases y oraciones. Se generarán coincidencias si se encuentra algún término o las formas de algún término en el índice de texto completo.  
  
 A diferencia de CONTAINS y CONTAINSTABLE buscar condición where y es una palabra clave, cuando se utiliza en *freetext_string* la palabra 'y' se considera una palabra irrelevante, o [palabra irrelevante](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)y se descartarán.  
  
 No se permite el uso de WEIGHT, FORMSOF, caracteres comodín, NEAR y otros elementos sintácticos. *freetext_string* desinencias, base coincidirá y pasa el diccionario de sinónimos.  
  
 *freetext_string* es **nvarchar**. Se realiza una conversión implícita cuando se usa otro tipo de datos de carácter como entrada. En el siguiente ejemplo, la variable `@SearchWord`, definida como una variable de tipo `varchar(30)`, provoca una conversión implícita en el predicado `FREETEXT`.  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 Dado que "examen de parámetros" no funciona con la conversión, utilice **nvarchar** para mejorar el rendimiento. En el ejemplo, declare `@SearchWord` como `nvarchar(30)`.  
  
```  
  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
  
```  
  
 También puede usar la sugerencia de consulta OPTIMIZE FOR para los casos en que se genera un plan que no es óptimo.  
  
 IDIOMA *language_term*  
 Es el idioma cuyos recursos se utilizarán en la separación de palabras, la lematización, los diccionarios de sinónimos y la eliminación de palabras irrelevantes como parte de la consulta. Este parámetro es opcional y puede especificarse como un valor hexadecimal, un entero o una cadena correspondiente al identificador de configuración regional (LCID) de un idioma. Si *language_term* se especifica, se aplicará el idioma que representa a todos los elementos de la condición de búsqueda. Si no se especifica ningún valor, se utiliza el idioma de texto completo de la columna.  
  
 Si se almacenan juntos documentos de idiomas diferentes como objetos binarios grandes (BLOB) en una sola columna, el identificador de configuración regional (LCID) de un documento determinado determina qué idioma se usa para indizar su contenido. Al consultar este tipo de columna, especificar *LENGUAJE**language_term* puede aumentar la probabilidad de encontrar una coincidencia acertada.  
  
 Cuando se especifica como una cadena, *language_term* corresponde a la **alias** valor de columna [sys.syslanguages &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) vista de compatibilidad.  La cadena debe incluirse entre comillas simples, como en '*language_term*'. Cuando se especifica como un entero, *language_term* es el LCID real que identifica el idioma. Cuando se especifica como un valor hexadecimal, *language_term* 0 x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda.  
  
 Si el valor está en formato de caracteres de doble byte (DBCS), set, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirá a Unicode.  
  
 Si el idioma especificado no es válido o no hay recursos instalados que se corresponden con dicho idioma, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error. Para usar los recursos de idioma neutro, especifique 0 x 0 como *language_term*.  
  
## <a name="general-remarks"></a>Notas generales  
 Los predicados y las funciones de texto completo operan en una única tabla, que se obtiene del predicado FROM. Para buscar en varias tablas, utilice una tabla combinada en la cláusula FROM a fin de buscar en un conjunto de resultados que sea el producto de dos o más tablas.  
  
Las consultas de texto completo que utilizan FREETEXT son menos precisas que las consultas de texto completo que utilizan CONTAINS. El motor de búsqueda de texto completo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica las palabras y las frases importantes. No se proporciona ningún significado especial para cualquiera de las palabras clave reservadas o caracteres comodín que suelen tienen significado cuando se especifica en el \<contains_search_condition > parámetro del predicado CONTAINS.
  
 Predicados de texto completo no están permitidos en el [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) cuando el nivel de compatibilidad de base de datos se establece en 100.  
  
> [!NOTE]  
>  La función FREETEXTTABLE es útil para los mismos tipos de coincidencias que el predicado FREETEXT. Puede hacer referencia a esta función como un nombre de tabla normal en el [cláusula FROM](../../t-sql/queries/from-transact-sql.md) de una instrucción SELECT. Para obtener más información, vea [FREETEXTTABLE &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/freetexttable-transact-sql.md).  
  
## <a name="querying-remote-servers"></a>Consultar servidores remotos  
 Puede usar un nombre de cuatro partes en el [CONTAINS](../../t-sql/queries/contains-transact-sql.md) o predicado FREETEXT para consultar el texto completo indizadas columnas de las tablas de destino en un servidor vinculado. Para preparar un servidor remoto para recibir consultas de texto completo, es necesario crear un índice de texto completo en las tablas y columnas de destino en el servidor remoto y, posteriormente, agregar el servidor remoto como un servidor vinculado.  
  
## <a name="comparison-of-like-to-full-text-search"></a>Comparación de LIKE con la búsqueda de texto completo  
 A diferencia de la búsqueda de texto completo, el predicado [LIKE](../../t-sql/language-elements/like-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] funciona solamente en patrones de caracteres. Además, no es posible utilizar el predicado de LIKE para consultar datos binarios con formato. Por otro lado, una consulta LIKE contra una cantidad grande de datos de texto no estructurados es mucho más lenta que una consulta de texto completo equivalente contra los mismos datos. Una consulta LIKE realizada en millones de filas de datos de texto puede tardar minutos en devolver resultados, mientras que una consulta de texto completo en los mismos datos puede tardar únicamente segundos, en función del número de filas que se devuelvan.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-freetext-to-search-for-words-containing-specified-character-values"></a>A. Usar FREETEXT para buscar palabras que contengan los valores de carácter especificados  
 En el siguiente ejemplo se buscan todos los documentos que contienen las palabras relacionadas con vital, safety, components.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components' );  
GO  
```  
  
### <a name="b-using-freetext-with-variables"></a>B. Usar FREETEXT con variables  
 En el siguiente ejemplo se utiliza una variable en lugar de un término de búsqueda específico.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30);  
SET @SearchWord = N'high-performance';  
SELECT Description   
FROM Production.ProductDescription   
WHERE FREETEXT(Description, @SearchWord);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la búsqueda de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Crear y administrar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [Crear catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Crear consultas de búsqueda de texto completo &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

