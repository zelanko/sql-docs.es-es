---
title: FREETEXTTABLE (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1f2d3c0c014db5a0cd5aab0dee22e6622fd24f20
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Es una función utilizada en el [cláusula FROM](../../t-sql/queries/from-transact-sql.md) de un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción SELECT para realizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] búsqueda de texto completo en texto completo indizadas las columnas que contienen tipos de datos basados en caracteres. Esta función devuelve una tabla de cero, uno o más filas para las columnas que contienen valores que coinciden con el significado y no solo literalmente, del texto especificado *freetext_string*. Se hace referencia a FREETEXTTABLE como si fuera un nombre de tabla normal.  
  
 FREETEXTTABLE es útil para los mismos tipos de coincidencias que la [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md),  
  
 Las consultas que usan FREETEXTTABLE devuelven un valor de clasificación por relevancia (RANK) y una clave de texto completo (KEY) para cada fila.  
  
> [!NOTE]  
>  Para obtener información sobre las formas de búsqueda de texto completo que se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Consulta con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
(http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table*  
 Es el nombre de la tabla que se ha marcado para consultas de texto completo. *tabla* o *vista*puede ser un uno, dos o nombre de objeto de base de datos de tres partes. Al consultar una vista, puede incluirse solo una tabla base indizada de texto completo.  
  
 *tabla* no se puede especificar un nombre de servidor y no se puede usar en las consultas en los servidores vinculados.  
  
 *column_name*  
 Es el nombre de una o varias columnas indizadas de texto completo de la tabla especificada en la cláusula FROM. Las columnas pueden ser de tipo **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** o **varbinary(max)**.  
  
 *column_list*  
 Indica que se pueden especificar varias columnas, separadas por una coma. *column_list* debe ir entre paréntesis. A menos que se especifique *language_term*, el idioma de todas las columnas de *column_list* debe ser el mismo.  
  
 \*  
 Especifica que todas las columnas que se hayan registrado para la búsqueda de texto completo se tienen que usar para buscar la *cadena_freetext* determinada. A menos que *language_term* se especifica, el idioma de todas las columnas indizadas de texto completo en la tabla debe ser el mismo.  
  
 *cadena_freetext*  
 Es el texto que se va a buscar en *column_name*. Se puede escribir cualquier texto, incluidas palabras, frases y oraciones. Se generarán coincidencias si se encuentra algún término o las formas de algún término en el índice de texto completo.  
  
 A diferencia de la CONTAINS buscar condición where y es una palabra clave, cuando se utiliza en *freetext_string* la palabra 'y' se considera una palabra irrelevante, o [palabra irrelevante](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)y se descartarán.  
  
 No se permite el uso de WEIGHT, FORMSOF, caracteres comodín, NEAR y otros elementos sintácticos. *cadena_freetext* se separa en palabras, de las que se extraen las desinencias y se pasan por el diccionario de sinónimos.  
  
 IDIOMA *language_term*  
 Es el idioma cuyos recursos se utilizarán en la separación de palabras, la lematización, los diccionarios de sinónimos y la eliminación de palabras irrelevantes como parte de la consulta. Este parámetro es opcional y puede especificarse como un valor hexadecimal, un entero o una cadena correspondiente al identificador de configuración regional (LCID) de un idioma. Si *language_term* se especifica, se aplicará el idioma que representa a todos los elementos de la condición de búsqueda. Si no se especifica ningún valor, se utiliza el idioma de texto completo de la columna.  
  
 Si se almacenan juntos documentos de idiomas diferentes como objetos binarios grandes (BLOB) en una sola columna, el identificador de configuración regional (LCID) de un documento determinado determina qué idioma se usa para indizar su contenido. Al consultar este tipo de columna, especificar *LANGUAGE**language_term* puede aumentar la probabilidad de encontrar una coincidencia acertada.  
  
 Cuando se especifica como una cadena, *language_term* corresponde al valor de columna **alias** de la vista de compatibilidad [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  La cadena debe estar delimitada con comillas sencillas, como en '*language_term*'. Cuando se especifica como un entero, *language_term* es el LCID real que identifica el idioma. Cuando se especifica como un valor hexadecimal, *language_term* es 0x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda.  
  
 Si el valor está en formato DBCS (juego de caracteres de doble byte), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirá a Unicode.  
  
 Si el idioma especificado no es válido o no hay recursos instalados que se correspondan con dicho idioma, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error. Para usar recursos de idioma neutro, especifique 0x0 como *language_term*.  
  
 *top_n_by_rank*  
 Especifica que solamente el *n*coincidencias con una clasificación más altas, en orden descendente, se devuelven. Sólo se aplica cuando un valor entero, *n*, se especifica. Si se combina *top_n_by_rank* con otros parámetros, es posible que la consulta devuelva menos filas de las que en realidad coinciden con todos los predicados. *top_n_by_rank* le permite aumentar el rendimiento de las consultas por recuperar solo las coincidencias más relevantes.  
  
## <a name="remarks"></a>Comentarios  
 Los predicados y las funciones de texto completo operan en una única tabla, que se obtiene del predicado FROM. Para buscar en varias tablas, utilice una tabla combinada en la cláusula FROM a fin de buscar en un conjunto de resultados que sea el producto de dos o más tablas.  
  
 FREETEXTTABLE utiliza las mismas condiciones de búsqueda que el predicado FREETEXT.  
  
 Al igual que CONTAINSTABLE, la tabla devuelta tiene columnas denominadas **clave** y **rango**, que se hace referencia en la consulta para obtener las filas apropiadas y utilizar los valores de clasificación de filas.  
  
## <a name="permissions"></a>Permissions  
 Solo los usuarios que dispongan de los privilegios SELECT adecuados para la tabla especificada o las columnas de la tabla a las que se haga referencia pueden llamar a FREETEXTTABLE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
 En el ejemplo siguiente se crea y rellena una tabla simple de dos columnas, enumerar los 3 condados y los colores de sus marcas. La TI crea y llena un catálogo de texto completo y un índice en la tabla. La **FREETEXTTABLE** se muestra la sintaxis.  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. Usar FREETEXT en INNER JOIN  
 En el ejemplo siguiente se devuelve el nombre y la descripción de todas las categorías relacionadas con `sweet`, `candy`, `bread`, `dry` o `meat`.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. Especificar las coincidencias con una clasificación más alta y el idioma  
 En el ejemplo siguiente es idéntico y muestra el uso de la `LANGUAGE` *language_term* y *top_n_by_rank* parámetros.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  El LENGUAJE *language_term* parámet*r* no es necesaria para usar el *top_n_by_rank* parámetro *.*  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la búsqueda de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Creación y administración de catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [Crear catálogo de texto completo & #40; Transact-SQL & #41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [Consultar con búsqueda de texto completo](../../relational-databases/search/query-with-full-text-search.md)   
 [Crear consultas de búsqueda de texto completo &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [Rowset Functions &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [Opción de configuración del servidor Calcular rango previamente](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
