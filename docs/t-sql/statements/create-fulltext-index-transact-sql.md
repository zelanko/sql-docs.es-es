---
title: "CREAR el índice de texto completo (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
caps.latest.revision: 110
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92749ed0518de83be07c6a80f9e3306741507166
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un índice de texto completo en una tabla o una vista indizada de una base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Solo se permite un índice de texto completo por cada tabla o vista indizada, y cada índice de texto completo se aplica a una única tabla o vista indizada. El índice de texto completo puede contener hasta 1.024 columnas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name*  
 Es el nombre de la tabla o vista indizada que contiene la columna o columnas incluidas en el índice de texto completo.  
  
 *column_name*  
 Es el nombre de la columna incluida en el índice de texto completo. Solo las columnas de tipo **char**, **varchar**, **nchar**, **nvarchar**, **texto**,  **ntext**, **imagen**, **xml**, y **varbinary (max)** se pueden indizar para búsquedas de texto completo. Para especificar varias columnas, repita el *column_name* cláusula como sigue:  
  
 CREATE FULLTEXT INDEX ON *table_name* (*column_name1* [...] *column_name2* [...])...  
  
 COLUMNA de tipo *type_column_name*  
 Especifica el nombre de una columna de tabla, *type_column_name*, que se usa para contener el tipo de documento para un **varbinary (max)** o **imagen** documento. Esta columna, denominada columna de tipo, contiene una extensión de archivo proporcionada por el usuario (.doc, .pdf, .xls, etc.). La columna de tipo debe ser de tipo **char**, **nchar**, **varchar**o **nvarchar**.  
  
 Especificar la columna de tipo *type_column_name* solo si *column_name* especifica un **varbinary (max)** o **imagen** columna, en el que los datos son se almacenan como datos binarios; en caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error.  
  
> [!NOTE]  
>  Durante la indización, el motor de texto completo utiliza la abreviatura en la columna de tipo de cada fila de la tabla para identificar qué filtro de búsqueda de texto completo que se usará para el documento en *column_name*. El filtro carga el documento como un flujo binario, quita la información del formato y envía el texto del documento al componente de separador de palabras. Para obtener más información, vea [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 IDIOMA *language_term*  
 Es el idioma de los datos almacenados en *column_name*.  
  
 *language_term* es opcional y se puede especificar como una cadena, entero o un valor hexadecimal correspondiente al identificador de configuración regional (LCID) de un idioma. Si no se especifica ningún valor, se utiliza el idioma predeterminado de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si *language_term* se especifica, se usará el idioma que representa al indizar los datos almacenados en **char**, **nchar**, **varchar**, **nvarchar**, **texto**, y **ntext** columnas. Este idioma es el idioma predeterminado utilizado en tiempo de consulta si *language_term* no se especifica como parte de un predicado de texto completo en la columna.  
  
 Cuando se especifica como una cadena, *language_term* corresponde al valor de columna de alias en la tabla del sistema syslanguages. La cadena debe incluirse entre comillas simples, como en **'***language_term***'**. Cuando se especifica como un entero, *language_term* es el LCID real que identifica el idioma. Cuando se especifica como un valor hexadecimal, *language_term* 0 x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda.  
  
 Si el valor está en formato DBCS (juego de caracteres de doble byte), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo convertirá a Unicode.  
  
 Recursos, como separadores de palabras y lematizadores, deben estar habilitados para el idioma especificado como *language_term*. Si estos recursos no admiten el idioma especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error.  
  
 Utilice el procedimiento almacenado sp_configure para tener acceso a la información sobre el idioma de texto completo predeterminado de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Para las columnas no BLOB y no XML que contienen datos de texto en varios idiomas o en los casos en que se desconoce el idioma del texto almacenado en la columna, podría ser apropiado usar el recurso de idioma neutro (0x0). Sin embargo, primero debería entender las posibles consecuencias de usar el recurso de idioma neutro (0x0). Para obtener información sobre las posibles soluciones y consecuencias de usar el recurso de idioma (0 x 0) neutro, consulte [elegir un idioma al crear un índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
 Para los documentos almacenados en columnas de tipo XML o BLOB, la codificación de idioma del documento se utilizará en el momento de la indización. Por ejemplo, en las columnas XML, el **XML: lang** atributo en documentos XML identifica el idioma. En el momento de la consulta, el valor especificado previamente en *language_term* se convierte en el idioma predeterminado usado para las consultas de texto completo, a menos que *language_term* se especifica como parte de una consulta de texto completo.  
  
 STATISTICAL_SEMANTICS  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Crea los índices adicionales de similitud de documentos y frases clave que forman parte de la indización semántica estadística. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 ÍNDICE de clave *index_name*  
 Es el nombre del índice de clave única en *table_name*. KEY INDEX debe ser una columna que no admita valores NULL con una sola clave única. Seleccione el índice de clave única más pequeño para la clave única de texto completo.  Para obtener el máximo rendimiento, recomendamos un tipo de datos entero para la clave de texto completo.  
  
 *fulltext_catalog_name*  
 Se trata del catálogo de texto completo utilizado para el índice de texto completo. El catálogo debe existir en la base de datos. Esta cláusula es opcional. Si no se especifica, se utiliza un catálogo predeterminado. Si no hay ningún catálogo predeterminado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error.  
  
 Grupo de archivos *filegroup_name*  
 Crea el índice de texto completo especificado en el grupo de archivos especificado. El grupo de archivos debe existir previamente. Si no se especifica la cláusula FILEGROUP, el índice de texto completo se coloca en el mismo grupo de archivos que la tabla base o la vista para una tabla sin particiones o en el grupo de archivos principal para una tabla con particiones.  
  
 CHANGE_TRACKING [=] {MANUAL | **AUTOMÁTICA** | DESACTIVAR [, NINGÚN RELLENADO]}  
 Especifica si los cambios (actualizaciones, eliminaciones o inserciones) realizados en columnas de tabla que están cubiertas por el índice de texto completo se propagarán por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al índice de texto completo. Los cambios realizados en los datos con WRITETEXT y UPDATETEXT no se reflejan en el índice de texto completo y no se recopilan con el seguimiento de cambios.  
  
 MANUAL  
 Especifica que se deben propagar manualmente los cambios controlados mediante una llamada a la instrucción ALTER FULLTEXT INDEX... START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción (*rellenado manual*). Puede utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para llamar a esta instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma periódica.  
  
 **AUTOMÁTICO**  
 Especifica que el seguimiento se propagarán automáticamente cuando se modifican los datos de la tabla base (*rellenado automático*). Aunque los cambios se propagan de forma automática, podrían no reflejarse de inmediato en el índice de texto completo. AUTO es el valor predeterminado.  
  
 OFF [ `,` NO POPULATION]  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mantiene una lista de los cambios realizados en los datos indizados. Si no se especifica NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena el índice por completo tras su creación.  
  
 La opción NO POPULATION se puede utilizar únicamente si CHANGE_TRACKING es OFF. Si se especifica NO POPULATION, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no rellena el índice tras su creación. El índice solamente se rellena después de que el usuario ejecuta el comando ALTER FULLTEXT INDEX con la cláusula START FULL POPULATION o START INCREMENTAL POPULATION.  
  
 LISTA DE PALABRAS IRRELEVANTES [=] {DESACTIVADO | **SYSTEM** | *stoplist_name* }  
 Asocia una lista de palabras irrelevantes de texto completo al índice. El índice no se rellena con ningún token que forme parte de la lista de palabras irrelevantes especificada. Si no se especifica STOPLIST, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asocia la lista de palabras irrelevantes de texto completo del sistema al índice.  
  
 OFF  
 Especifica que no se asocie al índice de texto completo ninguna lista de palabras irrelevantes.  
  
 **SISTEMA**  
 Especifica que la lista de palabras irrelevantes predeterminada de texto completo del sistema se debe usar para este índice de texto completo.  
  
 *stoplist_name*  
 Especifica el nombre de la lista de palabras irrelevantes que se va a asociar al índice de texto completo.  
  
 LISTA de propiedades de búsqueda [=] *property_list_name*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Asocia una lista de propiedades de búsqueda al índice.  
  
 OFF  
 Especifica que no se asocie al índice de texto completo ninguna lista de propiedades.  
  
 *property_list_name*  
 Especifica el nombre de la lista de propiedades de búsqueda que se va a asociar al índice de texto completo.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de los índices de texto completo, vea [crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).  
  
 En **xml** columnas, puede crear un índice de texto completo indiza el contenido de los elementos XML, pero omitiendo el marcado XML. Los valores de los atributos se incluyen en el índice de texto completo a menos que sean valores numéricos. Las etiquetas de elemento se utilizan como límites de token. Se admiten fragmentos y documentos con formato XML o HTML correcto que contengan varios idiomas. Para obtener más información, vea [Usar la búsqueda de texto completo con columnas XML](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
 Recomendamos que la columna de clave de índice sea de un tipo de datos entero. Esto proporciona optimizaciones en el momento de ejecución de la consulta.  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>Interacciones del seguimiento de cambios y del parámetro NO POPULATION  
 Que se rellene el índice de texto completo depende de si el seguimiento de cambios está habilitado y si se especifica WITH NO POPULATION en la instrucción ALTER FULLTEXT INDEX. En la tabla siguiente se resume el resultado de su interacción.  
  
|Seguimiento de cambios|WITH NO POPULATION|Resultado|  
|---------------------|------------------------|------------|  
|No se ha habilitado|No se ha especificado|Se realiza un rellenado completo en el índice.|  
|No se ha habilitado|Specified|No se produce el rellenado del índice hasta que se emite una instrucción ALTER FULLTEXT INDEX...START POPULATION.|  
|Habilitado|
          Specified|Se produce un error y no se altera el índice.|  
|Habilitado|No se ha especificado|Se realiza un rellenado completo en el índice.|  
  
 Para obtener más información acerca de cómo rellenar índices de texto completo, vea [rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener el permiso REFERENCES en el catálogo de texto completo y el permiso ALTER en la tabla o vista indizada, o ser un miembro del rol fijo de servidor sysadmin o los roles fijos de base de datos db_owner o db_ddladmin.  
  
 Si se especifica SET STOPLIST, el usuario debe tener el permiso REFERENCES en la lista de palabras irrelevantes especificada. El propietario de la lista de palabras irrelevantes puede conceder este permiso.  
  
> [!NOTE]  
>  Los usuarios tienen el permiso REFERENCE para la lista de palabras irrelevantes predeterminada que se incluye con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. Crear un índice único, un catálogo de texto completo y un índice de texto completo  
 En el ejemplo siguiente se crea un índice único en la columna `JobCandidateID` de la tabla `HumanResources.JobCandidate` de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A continuación, se crea un catálogo de texto completo predeterminado, `ft`. Por último, se crea un índice de texto completo en la columna `Resume` mediante el catálogo `ft` y la lista de palabras irrelevantes del sistema.  
  
```  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. Crear un índice de texto completo en varias columnas de la tabla  
 En el ejemplo siguiente se crea un catálogo de texto completo, `production_catalog`, en la base de datos de ejemplo `AdventureWorks`. A continuación, se crea un índice de texto completo que usa este nuevo catálogo. El índice de texto completo está en las columnas `ReviewerName`, `EmailAddress` y `Comments` de `Production.ProductReview`. Para cada columna, en el ejemplo se especifica el LCID de inglés, `1033`, que es el idioma de los datos de las columnas. Este índice de texto completo utiliza un índice de clave única existente, `PK_ProductReview_ProductReviewID`. Tal como se recomienda, esta clave de índice está en una columna de tipo entero, `ProductReviewID`.  
  
```  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. Crear un índice de texto completo con una lista de propiedades de búsqueda sin rellenarlo  
 En el ejemplo siguiente se crea un índice de texto completo en las columnas `Title`, `DocumentSummary` y `Document` de la tabla `Production.Document`. En el ejemplo se especifica el LCID de inglés, `1033`, que es el idioma de los datos de las columnas. Este índice de texto completo utiliza el catálogo de texto completo predeterminado y un índice de clave única existente, `PK_Document_DocumentID`. Tal como se recomienda, esta clave de índice está en una columna de tipo entero, `DocumentID`.  
  
 El ejemplo especifica la lista de palabras irrelevantes SYSTEM. También especifica una lista de propiedades de búsqueda, `DocumentPropertyList`; para obtener un ejemplo que crea esta lista de propiedades, vea [CREATE SEARCH PROPERTY LIST &#40; Transact-SQL &#41; ](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
 En el ejemplo se especifica que el seguimiento de cambios está desactivado sin rellenado. Posteriormente, durante las horas de menor actividad, en el ejemplo se utiliza una instrucción ALTER FULLTEXT INDEX para iniciar un rellenado completo en el nuevo índice y habilitar el seguimiento automático de cambios.  
  
```  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 Posteriormente, durante horas de menor actividad, el índice se rellena:  
  
```  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Sys.fulltext_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

