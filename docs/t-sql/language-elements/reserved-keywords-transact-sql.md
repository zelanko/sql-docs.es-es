---
title: Palabras clave (Transact-SQL) reservadas | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f2a3e554a7a3b46242c44c38137609322e6d89f4
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="reserved-keywords-transact-sql"></a>Palabras clave reservadas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza palabras clave reservadas para definir, manipular y tener acceso a las bases de datos. Las palabras clave reservadas forman parte de la gramática del lenguaje [!INCLUDE[tsql](../../includes/tsql-md.md)] que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para analizar y comprender las instrucciones y lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Aunque resulta sintácticamente posible usar palabras clave reservadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como identificadores y nombres de objetos en scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)], solo se puede hacer usando identificadores delimitados.  
  
 En la tabla siguiente se enumeran las palabras clave reservadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|y|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION |FREETEXTTABLE|Replicación|  
|BACKUP|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|BY|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|ARRIBA|  
|CURSOR|NOT|TRAN|  
|DATABASE|NULL|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPTION|User|  
|DROP|O BIEN|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|por|  
|Ejecute|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 Además, el estándar ISO define una lista de palabras clave reservadas. Evite utilizar las palabras clave reservadas de ISO como identificadores y nombres de objetos. La lista de palabras clave reservadas de ODBC (que se muestra en la tabla siguiente) es igual que la de ISO.  
  
> [!NOTE]  
>  La lista de palabras clave reservadas de los estándares ISO puede ser unas veces más restrictiva que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y otras veces, menos. Por ejemplo, la lista de palabras clave reservadas de ISO contiene **INT**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene que distinguirla como una palabra clave reservada.  
  
 Se puede utilizar palabras clave reservadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] como identificadores o nombres de objetos de base de datos, tales como tablas, columnas, vistas, etc. Utilice identificadores entre comillas o identificadores delimitados. No está restringido el uso de palabras clave reservadas como nombres de variables y parámetros de procedimientos almacenados.  
  
## <a name="odbc-reserved-keywords"></a>Palabras clave reservadas de ODBC  
 Las siguientes palabras están reservadas para su uso en llamadas a funciones de ODBC. Estas palabras no limitan la gramática mínima de SQL; sin embargo, para asegurar la compatibilidad con los controladores que admiten la gramática principal de SQL, las aplicaciones deben evitar la utilización de estas palabras clave.  
  
 A continuación se muestra la lista actual de palabras clave reservadas de ODBC.  
  
||||  
|-|-|-|  
|**ABSOLUTA**|**EXEC**|**OVERLAPS**|  
|**ACCIÓN**|**EXECUTE**|**PAD**|  
|**ADA**|**EXISTS**|**PARCIAL**|  
|**ADD**|**EXTERNAL**|**PASCAL**|  
|**ALL**|**EXTRACT**|**POSICIÓN**|  
|**ASIGNAR**|**FALSE**|**PRECISIÓN**|  
|**ALTER**|**FETCH**|**PREPARAR**|  
|**AND**|**FIRST**|**PRESERVE**|  
|**ANY**|**FLOAT**|**PRIMARY**|  
|**SON**|**FOR**|**PRIOR**|  
|**AS**|**EXTERNA**|**PRIVILEGES**|  
|**ASC**|**FORTRAN**|**PROCEDURE**|  
|**ASERCIÓN**|**SE ENCONTRÓ**|**PUBLIC**|  
|**AT**|**FROM**|**READ**|  
|**AUTHORIZATION**|**FULL**|**REAL**|  
|**AVG**|**GET**|**REFERENCIAS**|  
|**BEGIN**|**GLOBAL**|**RELATIVA**|  
|**BETWEEN**|**GO**|**RESTRICT**|  
|**BIT**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**BOTH**|**GROUP**|**ROLLBACK**|  
|**BY**|**TENER**|**ROWS**|  
|**CASCADE**|**HORA**|**SCHEMA**|  
|**CASCADED**|**IDENTIDAD**|**SCROLL**|  
|**CASE**|**INMEDIATA**|**SECOND**|  
|**CAST**|**IN**|**SECCIÓN**|  
|**CATÁLOGO**|**INCLUIR**|**SELECT**|  
|**CHAR**|**INDEX**|**SESIÓN**|  
|**CHAR_LENGTH**|**INDICADOR**|**SESSION_USER**|  
|**CARÁCTER**|**INICIALMENTE**|**SET**|  
|**CHARACTER_LENGTH**|**INTERNA**|**TAMAÑO**|  
|**COMPROBAR**|**INPUT**|**SMALLINT**|  
|**CLOSE**|**MINÚSCULAS**|**ALGUNOS**|  
|**COALESCE**|**INSERT**|**SPACE**|  
|**COLLATE**|**INT**|**SQL**|  
|**INTERCALACIÓN**|**INTEGER**|**SQLCA**|  
|**COLUMN**|**INTERSECT**|**SQLCODE**|  
|**COMMIT**|**INTERVAL**|**SQLERROR**|  
|**CONNECT**|**INTO**|**SQLSTATE**|  
|**CONEXIÓN**|**ES**|**OBJETO SQLWARNING**|  
|**CONSTRAINT**|**AISLAMIENTO**|**SUBSTRING**|  
|**RESTRICCIONES**|**COMBINACIÓN**|**SUM**|  
|**CONTINUE**|**KEY**|**SYSTEM_USER**|  
|**CONVERT**|**LANGUAGE**|**TABLE**|  
|**CORRESPONDIENTE**|**LAST**|**TEMPORARY**|  
|**COUNT**|**A LA IZQUIERDA**|**THEN**|  
|**CREAR**|**LEFT**|**TIEMPO**|  
|**CROSS**|**LEVEL**|**MARCA DE TIEMPO**|  
|**CURRENT**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**LOCAL**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**LOWER**|**TO**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**FINALES**|  
|**CURRENT_USER**|**MAX**|**TRANSACCIÓN**|  
|**CURSOR**|**MIN**|**TRANSLATE**|  
|**FECHA**|**MINUTO**|**TRADUCCIÓN**|  
|**DAY**|**MÓDULO**|**TRIM**|  
|**DEALLOCATE**|**MONTH**|**TRUE**|  
|**DEC**|**NOMBRES DE**|**UNIÓN**|  
|**DECIMAL**|**NACIONAL**|**UNIQUE**|  
|**DECLARAR**|**NATURAL**|**UNKNOWN**|  
|**DEFAULT**|**NCHAR**|**UPDATE**|  
|**DEFERRABLE**|**NEXT**|**UPPER**|  
|**DEFERRED**|**NO**|**USO DE**|  
|**DELETE**|**NONE**|**USER**|  
|**DESC**|**NOT**|**USO DE**|  
|**DESCRIBIR**|**NULL**|**VALUE**|  
|**DESCRIPTOR**|**NULLIF**|**VALUES**|  
|**DIAGNOSTICS**|**NUMÉRICO**|**VARCHAR**|  
|**DESCONECTAR**|**OCTET_LENGTH**|**VARIABLE**|  
|**DISTINCT**|**OF**|**VIEW**|  
|**DOMINIO**|**ON**|**CUANDO**|  
|**DOBLE**|**SOLO**|**WHENEVER**|  
|**DROP**|**OPEN**|**WHERE**|  
|**ELSE**|**OPCIÓN**|**CON**|  
|**END**|**O BIEN**|**WORK**|  
|**END-EXEC**|**ORDER**|**ESCRIBIR**|  
|**ESCAPE**|**EXTERNA**|**YEAR**|  
|**EXCEPT**|**OUTPUT**|**ZONE**|  
|**(EXCEPCIÓN)**|||  
  
## <a name="future-keywords"></a>Futuras palabras clave  
 Las siguientes palabras clave podrían quedar reservadas en futuras versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a medida que se implementen nuevas características. Procure evitar el uso de estas palabras como identificadores.  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE|  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|ESPACIO|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|TIMESTAMP|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|No|TIMEZONE_MINUTE|  
|CURRENT_PATH|Ninguno|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|VALUE|  
|DEPTH|PAD|VAR_POP|  
|DEREF|Parámetro|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|REAL|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|FLOAT|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|GRATUITO|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>Vea también  
 [SET QUOTED_IDENTIFIER &#40; Transact-SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
