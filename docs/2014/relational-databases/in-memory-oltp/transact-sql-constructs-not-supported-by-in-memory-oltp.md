---
title: Construcciones Transact-SQL no admitidas por OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda74f247f9899b9e0a23d43143a5031574d8c13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155302"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>Construcciones Transact-SQL no admitidas por OLTP en memoria
  Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no admiten el área expuesta completa de [!INCLUDE[tsql](../../includes/tsql-md.md)]; sin embargo, las tablas basadas en disco y los procedimientos almacenados interpretados de [!INCLUDE[tsql](../../includes/tsql-md.md)] sí la admiten. Cuando se intenta usar una de las características no admitidas, el servidor devuelve un error.  
  
 El mensaje de error menciona el tipo de instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] (por ejemplo, característica, operación, opción) y el nombre de la característica o palabra clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La mayor parte de características no admitidas devolverán el error 10794, con un mensaje de error que indique la función no admitida. En las tablas siguientes se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto del mensaje de error, así como la acción correctiva para resolver el error.  
  
 Para obtener más información sobre las características admitidas con las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa, vea:  
  
-   [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [Compatibilidad de Transact-SQL con OLTP en memoria](transact-sql-support-for-in-memory-oltp.md)  
  
-   [Características admitidas de SQL Server](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [Procedimientos almacenados compilados de forma nativa](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>Bases de datos que utilizan OLTP en memoria  
 En la siguiente tabla se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto del mensaje de error que implica una base de datos OLTP en memoria.  
  
|Tipo|NOMBRE|Solución|  
|----------|----------|----------------|  
|Opción|AUTO_CLOSE|La opción de base de datos AUTO_CLOSE=ON no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Opción|ATTACH_REBUILD_LOG|La opción de base de datos ATTACH_REBUILD_LOG de CREATE no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|DATABASE SNAPSHOT|La creación de instantáneas de base de datos no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|Replicación con el sync_method 'database snapshot' o 'database snapshot character'|La replicación con sync_method 'database snapshot' o 'database snapshot character' no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB omite las tablas optimizadas para memoria en la base de datos.<br /><br /> DBCC CHECKTABLE producirá un error en las tablas optimizadas para memoria.|  
  
## <a name="memory-optimized-tables"></a>Tablas con optimización para memoria  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con una tabla optimizada para memoria, así como la acción correctiva para resolver el error.  
  
|Tipo|Name|Solución|  
|----------|----------|----------------|  
|Característica|ON|Las tablas con optimización para memoria no se pueden colocar en un grupo de archivos ni en un esquema de partición. Quite la cláusula ON de la instrucción `CREATE TABLE`.|  
|Tipo de datos|*Nombre del tipo de datos*|No se admite el tipo de datos indicado. Reemplace el tipo por uno de los tipos de datos admitidos. Para obtener más información, consulte [Supported Data Types](supported-data-types-for-in-memory-oltp.md).|  
|Característica|Columnas calculadas|Las tablas optimizadas para memoria no admiten columnas calculadas. Quite las columnas calculadas de la instrucción `CREATE TABLE`.|  
|Característica|Replicación|La replicación no es compatible con las tablas optimizadas para memoria.|  
|Característica|FILESTREAM|Las columnas de las tablas optimizadas para memoria no admiten el almacenamiento FILESTREAM. Quite la palabra clave `FILESTREAM` de la definición de columna.|  
|Característica|SPARSE|Las columnas de las tablas optimizadas para memoria no se pueden definir como columnas SPARSE. Quite la palabra clave `SPARSE` de la definición de columna.|  
|Característica|ROWGUIDCOL|Las columnas de las tablas optimizadas para memoria no admiten la opción ROWGUIDCOL. Quite la palabra clave `ROWGUIDCOL` de la definición de columna.|  
|Característica|FOREIGN KEY|Las tablas optimizadas para memoria no admiten restricciones FOREIGN KEY. Quite la restricción de la definición de tabla.<br /><br /> Para obtener información sobre cómo mitigar la falta de compatibilidad con las restricciones, vea [restricciones Foreign Key y comprobación de migración](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Característica|CHECK|Las tablas optimizadas para memoria no admiten restricciones CHECK. Quite la restricción de la definición de tabla.<br /><br /> Para obtener información sobre cómo mitigar la falta de compatibilidad con las restricciones, vea [restricciones Foreign Key y comprobación de migración](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Característica|UNIQUE|Las tablas optimizadas para memoria no admiten restricciones UNIQUE. Quite la restricción de la definición de tabla.<br /><br /> Para obtener información sobre cómo mitigar la falta de compatibilidad con las restricciones, vea [restricciones Foreign Key y comprobación de migración](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Característica|COLUMNSTORE|Las tablas optimizadas para memoria no admiten índices COLUMNSTORE. Especifique un índice NONCLUSTERED o NONCLUSTERED HASH en su lugar.|  
|Característica|índice clúster|Especifique un índice no clúster. Si se trata de un índice de clave principal, no se olvide de especificar `PRIMARY KEY NONCLUSTERED [HASH]`.|  
|Característica|Página de códigos distinta de 1252|Las columnas de las tablas optimizadas para memoria con tipos de datos `char` y `varchar` deben utilizar la página de códigos 1252. Use n(var)char en lugar de (var)char, o use una intercalación con la página de códigos 1252 (por ejemplo, Latin1_General_BIN2). Para obtener más información, consulte [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Característica|DDL dentro de transacciones|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar en el contexto de una transacción de usuario. No inicie ninguna transacción y asegúrese de que el parámetro de sesión IMPLICIT_TRANSACTIONS está establecido en OFF antes de ejecutar la instrucción CREATE o DROP.|  
|Característica|DDL, desencadenadores|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar si existe un desencadenador de base de datos o de servidor para la operación DDL. Quite los desencadenadores de servidor y de base de datos de CREATE/DROP TABLE y CREATE/DROP PROCEDURE.|  
|Característica|EVENT NOTIFICATION|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar si existe una notificación de evento de base de datos o de servidor para la operación DDL. Quite las notificaciones de eventos de servidor y de base de datos en CREATE TABLE o DROP TABLE y CREATE PROCEDURE o DROP PROCEDURE.|  
|Característica|FileTable|Las tablas con optimización para memoria no se pueden crear como tablas de archivos. Quite el argumento `AS FileTable` de la instrucción `CREATE TABLE`.|  
|Operación|Actualización de columnas de clave principal|Las columnas de clave principal de las tablas optimizadas para memoria y los tipos de tablas no se pueden actualizar. Si es necesario actualizar la clave principal, elimine la fila antigua e inserte la nueva fila con la clave principal actualizada.|  
|Operación|CREATE INDEX|Los índices de las tablas optimizadas para memoria deben especificarse insertados con la instrucción `CREATE TABLE`. Para agregar un índice a una tabla optimizada para memoria, quite y vuelva a crear la tabla incluyendo la especificación del nuevo índice.|  
|Operación|ALTER TABLE|No es posible modificar las tablas optimizadas para memoria. Quite y vuelva a crear la tabla usando la definición de tabla actualizada.|  
|Operación|CREATE FULLTEXT INDEX|Las tablas optimizadas para memoria no admiten índices de texto completo.|  
|Operación|Cambios en los esquemas|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no admiten cambios en los esquemas, por ejemplo, `sp_rename`.<br /><br /> Si se intenta realizar cambios de esquema, como cambiar el nombre de una tabla, generará el error 12320. Las operaciones que requieren un cambio en la versión de esquema, como cambiar el nombre, no se admiten con las tablas optimizadas para memoria.<br /><br /> Para cambiar el esquema, quite y vuelva a crear la tabla o el procedimiento usando una definición actualizada.|  
|Operación|CREATE TRIGGER|Las tablas optimizadas para memoria no admiten desencadenantes.|  
|Operación|TRUNCATE TABLE|Las tablas optimizadas para memoria no admiten la operación TRUNCATE. Para quitar todas las filas de una tabla, elimínelas con `DELETE FROM` *tabla* o quite y vuelva a la tabla.|  
|Operación|ALTER AUTHORIZATION|No es posible cambiar el propietario de una tabla optimizada para memoria o de un procedimiento almacenado compilado de forma nativa existente. Para cambiar el propietario, quite y vuelva a crear la tabla o el procedimiento.|  
|Operación|ALTER SCHEMA|No es posible cambiar el esquema de una tabla optimizada para memoria o de un procedimiento almacenado compilado de forma nativa existente. Para cambiar el propietario, quite y vuelva a crear la tabla o el esquema.|  
|Operación|DBCC CHECKTABLE|DBCC CHECKTABLE no es compatible con las tablas optimizadas para memoria.|  
|Característica|ANSI_PADDING OFF|Cuando se crean tablas optimizadas para memoria o procedimientos almacenados compilados de forma nativa, la opción de sesión `ANSI_PADDING` debe estar establecida en ON. Ejecute `SET ANSI_PADDING ON` antes de ejecutar la instrucción CREATE.|  
|Opción|DATA_COMPRESSION|Las tablas optimizadas para memoria no admiten la compresión de datos. Quite la opción de la definición de tabla.|  
|Característica|DTC|No se puede tener acceso a las tablas con optimización para memoria ni a los procedimientos almacenados compilados de forma nativa desde transacciones distribuidas. En su lugar, use transacciones SQL.|  
|Característica|Conjuntos de resultados activos múltiples (MARS)|Las tablas optimizadas para memoria no admiten Multiple Active Result Sets (MARS). Este error también puede indicar que se está usando un servidor vinculado. El servidor vinculado puede utilizar MARS. Las tablas optimizadas para memoria no admiten servidores vinculados. En su lugar, conéctese directamente al servidor y a la base de datos que hospedan las tablas optimizadas para memoria.|  
|Operación|Tablas con optimización para memoria como destino de MERGE|Las tablas con optimización para memoria no pueden ser el destino de una operación `MERGE`. En su lugar, use las instrucciones `INSERT`, `UPDATE` o `DELETE`.|  
  
## <a name="indexes-on-memory-optimized-tables"></a>Índices de las tablas con optimización para memoria  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con un índice de una tabla optimizada para memoria, así como la acción correctiva para resolver el error.  
  
|Tipo|NOMBRE|Solución|  
|----------|----------|----------------|  
|Característica|Índice filtrado|Las tablas optimizadas para memoria no admiten índices filtrados. Omita la cláusula `WHERE` en la especificación de índice.|  
|Característica|UNIQUE|Las tablas optimizadas para memoria no admiten índices únicos. Quite el argumento `UNIQUE` de la especificación de índice.|  
|Característica|Columnas que aceptan valores NULL|Todas las columnas existentes en la clave de un índice de una tabla optimizada para memoria se deben especificar como `NOT NULL`. Incluya la restricción `NOT NULL` con todas las columnas de las claves de índice.|  
|Característica|Intercalación distinta de bin2|Todas las columnas de caracteres existentes en la clave de un índice optimizado para memoria se deben declarar mediante una intercalación BIN2. Use la cláusula `COLLATE` para establecer la intercalación en la definición de columna. Para obtener más información, consulte [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Característica|Columnas incluidas|No es necesario especificar columnas incluidas en las tablas optimizadas para memoria. Todas las columnas de la tabla optimizada para memoria se incluyen de forma implícita en cada índice optimizado para memoria.|  
|Operación|ALTER INDEX|No se admite modificar los índices de las tablas optimizadas para memoria. En su lugar, quite la tabla y vuelva a crearla usando la especificación de índice actualizada.|  
|Operación|DROP INDEX|No es posible quitar los índices de las tablas optimizadas para memoria. En su lugar, quite la tabla y vuelva a crearla con los índices deseados.|  
|Opción de índice|*Opción de índice*|Los índices de las tablas optimizadas para memoria no admiten la opción de índice indicada. Quite la opción de la especificación de índice.|  
  
## <a name="nonclustered-hash-indexes"></a>Índices de hash no clúster  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con un índice de hash no clúster, así como la acción correctiva para resolver el error.  
  
|Tipo|Name|Solución|  
|----------|----------|----------------|  
|Opción|ASC/DESC|Los índices de hash no clúster no se ordenan. Quite las palabras clave `ASC` y `DESC` de la especificación de clave de índice.|  
  
## <a name="natively-compiled-stored-procedures"></a>procedimientos almacenados compilados de forma nativa  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con procedimientos almacenados compilados de forma nativa, así como la acción correctiva para resolver el error.  
  
|Tipo|Característica|Solución|  
|----------|-------------|----------------|  
|Característica|Variables de las tablas insertadas|Los tipos de tablas no pueden declararse insertadas con declaraciones de variable. Los tipos de tablas deben declararse de forma explícita mediante una instrucción `CREATE TYPE`.|  
|Característica|Cursores|Los procedimientos almacenados compilados de forma nativa no admiten cursores.<br /><br /> -Cuando se ejecuta el procedimiento desde el cliente, utilice RPC en lugar de la API de cursores. Con ODBC, evite la instrucción `EXECUTE` de [!INCLUDE[tsql](../../includes/tsql-md.md)]; en su lugar, especifique el nombre del procedimiento directamente.<br /><br /> -Cuando se ejecuta el procedimiento desde un [!INCLUDE[tsql](../../includes/tsql-md.md)] por lotes u otro procedimiento almacenado, evite el uso de un cursor con el procedimiento almacenado compilado de forma nativa.<br /><br /> -Cuando se cree un procedimiento almacenado compilado de forma nativa, en lugar de utilizar un cursor, utilice lógica basada en conjunto o un `WHILE` bucle.|  
|Característica|Valores predeterminados de parámetros no constantes|Cuando se usan los valores predeterminados de los parámetros en procedimientos almacenados compilados de forma nativa, dichos valores deben ser constantes. Quite los caracteres comodín de las declaraciones de parámetro.|  
|Característica|EXTERNAL|Los procedimientos almacenados CLR no se pueden compilar de forma nativa. Quite la cláusula AS EXTERNAL o la opción de NATIVE_COMPILATION de la instrucción CREATE PROCEDURE.|  
|Característica|Procedimientos almacenados numerados|Los procedimientos almacenados compilados de forma nativa no se pueden numerar. Quitar el `;` *número* desde el `CREATE PROCEDURE` instrucción.|  
|Característica|Instrucciones INSERT ... VALUES de varias filas|En un procedimiento almacenado compilado de forma nativa no se pueden insertar varias filas usando la misma instrucción `INSERT`. Cree instrucciones `INSERT` para cada fila.|  
|Característica|Expresiones de tabla común (CTE)|Los procedimientos almacenados compilados de forma nativa no admiten expresiones de tabla común (CTE). Vuelva a escribir la consulta.|  
|Característica|subconsulta|Las subconsultas (consultas anidadas dentro de otra consulta) no se admiten. Vuelva a escribir la consulta.|  
|Característica|COMPUTE|No se admite la cláusula `COMPUTE`. Quítela de la consulta.|  
|Característica|SELECT INTO|La cláusula `INTO` no se puede usar con la instrucción `SELECT`. Reescriba la consulta como `INSERT INTO` *tabla*`SELECT`.|  
|Característica|OUTPUT|No se admite la cláusula `OUTPUT`. Quítela de la consulta.|  
|Característica|Lista de columnas insertadas incompleta|En las instrucciones `INSERT`, deben especificarse valores para todas las columnas de la tabla.|  
|Función|*Función*|Los procedimientos almacenados compilados de forma nativa no admiten la función integrada. Quite la función del procedimiento almacenado. Para obtener más información acerca de las funciones integradas admitidas, consulte [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Característica|CASE|Los procedimientos almacenados compilados de forma nativa no admiten la instrucción `CASE` en las consultas. Cree consultas diferentes para mayúsculas y minúsculas. Para obtener más información, consulte [implementación de una instrucción CASE](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md).|  
|Característica|funciones definidas por el usuario|En los procedimientos almacenados compilados de forma nativa no se pueden usar funciones definidas por el usuario. Quite la referencia a la función de la definición de procedimiento.|  
|Característica|agregados definidos por el usuario|En los procedimientos almacenados compilados de forma nativa no se pueden usar funciones de agregado definidas por el usuario. Quite la referencia a la función del procedimiento.|  
|Característica|Metadatos en el modo de exploración|Los procedimientos almacenados compilados de forma nativa no admiten metadatos en el modo de exploración. Asegúrese de que la opción de sesión `NO_BROWSETABLE` está establecida en OFF.|  
|Característica|DELETE con la cláusula FROM|Los procedimientos almacenados compilados de forma nativa no admiten la cláusula `FROM` en instrucciones `DELETE` con un origen de tabla.<br /><br /> `DELETE` con la cláusula `FROM` se admite cuando se emplea para indicar la tabla en la que hay que realizar la eliminación.|  
|Característica|UPDATE con la cláusula FROM|Los procedimientos almacenados compilados de forma nativa no admiten la cláusula `FROM` en instrucciones `UPDATE`.|  
|Característica|Procedimientos temporales|Los procedimientos almacenados temporales no se pueden compilar de forma nativa. Cree un procedimiento almacenado compilado de forma nativa que sea permanente o un procedimiento almacenado interpretado de [!INCLUDE[tsql](../../includes/tsql-md.md)] que sea temporal.|  
|Nivel de aislamiento|READ UNCOMMITTED|Los procedimientos almacenados compilados de forma nativa no admiten el nivel de aislamiento READ UNCOMMITTED. Use un nivel de aislamiento compatible, como SNAPSHOT.|  
|Nivel de aislamiento|READ COMMITTED|Los procedimientos almacenados compilados de forma nativa no admiten el nivel de aislamiento READ UNCOMMITTED. Use un nivel de aislamiento compatible, como SNAPSHOT.|  
|Característica|tablas temporales|En los procedimientos almacenados compilados de forma nativa no se pueden usar tablas de tempdb. En su lugar, use una variable de tabla o una tabla optimizada para memoria con DURABILITY=SCHEMA_ONLY.|  
|Característica|MARS|Los procedimientos almacenados compilados de forma nativa no admiten Multiple Active Result Sets (MARS). Este error también puede indicar que se está usando un servidor vinculado. El servidor vinculado puede utilizar MARS. Los procedimientos almacenados compilados de forma nativa no admiten servidores vinculados. En su lugar, conéctese directamente al servidor y a la base de datos que hospedan los procedimientos almacenados compilados de forma nativa.|  
|Característica|DTC|No se puede tener acceso a las tablas con optimización para memoria ni a los procedimientos almacenados compilados de forma nativa desde transacciones distribuidas. En su lugar, use transacciones SQL.|  
|Característica|Intercalación distinta de bin2|Para realizar operaciones con cadenas de caracteres en los procedimientos almacenados compilados de forma nativa, como operaciones de comparación u ordenación, es necesario el uso de una intercalación BIN2. Use la cláusula COLLATE o use columnas y variables con una intercalación adecuada. Para obtener más información, consulte [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Característica|Truncamiento de cadenas de caracteres con intercalación SC.|Las cadenas de caracteres con una intercalación `_SC` usan la codificación UTF-16. La conversión de un valor n(var)char en un valor n(var)char más corto conlleva truncamiento. En los procedimientos almacenados compilados de forma nativa esto no es posible para los valores UTF-16. Evite el truncamiento de las cadenas UTF-16.|  
|Característica|EXECUTE WITH RECOMPILE|Los procedimientos almacenados compilados de forma nativa no admiten la opción `WITH RECOMPILE`.|  
|Característica|LEN y SUBSTRING con un argumento en una intercalación SC|Las cadenas de caracteres con una intercalación _SC usan la codificación UTF-16. Las funciones integradas LEN y SUBSTRING, cuando se utilizan dentro de procedimientos almacenados compilados de forma nativa, no admiten la codificación UTF-16. Utilice una intercalación diferente o evite usar estas funciones.|  
|Característica|Ejecución de la conexión de administrador dedicada|Los procedimientos almacenados compilados de forma nativa no se pueden ejecutar desde la conexión de administrador dedicada (DAC). En su lugar, use una conexión normal.|  
|Operación|ALTER PROCEDURE|Los procedimientos almacenados compilados de forma nativa no se pueden modificar. Para cambiar la definición de procedimiento, quite y vuelva a crear el procedimiento almacenado.|  
|Operación|punto de retorno|Los procedimientos almacenados compilados de forma nativa no se pueden invocar desde transacciones que tienen un punto de retorno activo. Quite el punto retorno de la transacción.|  
|Operación|ALTER AUTHORIZATION|No es posible cambiar el propietario de una tabla optimizada para memoria o de un procedimiento almacenado compilado de forma nativa existente. Para cambiar el propietario, quite y vuelva a crear la tabla o el procedimiento.|  
|Operador|OPENROWSET|No se admite este operador. Quite `OPENROWSET` del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENQUERY|No se admite este operador. Quite `OPENQUERY` del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENDATASOURCE|No se admite este operador. Quite `OPENDATASOURCE` del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENXML|No se admite este operador. Quite `OPENXML` del procedimiento almacenado compilado de forma nativa.|  
|Operador|CONTAINSTABLE|No se admite este operador. Quite `CONTAINSTABLE` del procedimiento almacenado compilado de forma nativa.|  
|Operador|FREETEXTTABLE|No se admite este operador. Quite `FREETEXTTABLE` del procedimiento almacenado compilado de forma nativa.|  
|Característica|Funciones con valores de tabla|En los procedimientos almacenados compilados de forma nativa no se puede hacer referencia a funciones con valores de tabla. Una solución posible para esta restricción es agregar la lógica de las funciones con valores de tabla al cuerpo del procedimiento.|  
|Operador|CHANGETABLE|No se admite este operador. Quite `CHANGETABLE` del procedimiento almacenado compilado de forma nativa.|  
|Operador|GOTO|No se admite este operador. Use otras construcciones de procedimiento, como WHILE.|  
|Operador|EXECUTE, INSERT EXEC|No se admite el anidamiento de procedimientos almacenados compilados de forma nativa. Las operaciones necesarias se pueden especificar insertadas, como parte de la definición de los procedimientos almacenados.|  
|Operador|OFFSET|No se admite este operador. Quite `OFFSET` del procedimiento almacenado compilado de forma nativa.|  
|Operador|UNION|No se admite este operador. Quite `UNION` del procedimiento almacenado compilado de forma nativa. Para combinar varios conjuntos de resultados en un solo conjunto se puede usar una variable de tabla.|  
|Operador|INTERSECT|No se admite este operador. Quite `INTERSECT` del procedimiento almacenado compilado de forma nativa. En algunos casos se puede usar INNER JOIN para obtener el mismo resultado.|  
|Operador|EXCEPT|No se admite este operador. Quite `EXCEPT` del procedimiento almacenado compilado de forma nativa.|  
|Operador|OUTER JOIN|No se admite este operador. Quite `OUTER JOIN` del procedimiento almacenado compilado de forma nativa. Para obtener más información, consulte [implementar Outer Join](implementing-an-outer-join.md).|  
|Operador|APPLY|No se admite este operador. Quite `APPLY` del procedimiento almacenado compilado de forma nativa.|  
|Operador|PIVOT|No se admite este operador. Quite `PIVOT` del procedimiento almacenado compilado de forma nativa.|  
|Operador|UNPIVOT|No se admite este operador. Quite `UNPIVOT` del procedimiento almacenado compilado de forma nativa.|  
|Operador|OR, IN|Los procedimientos almacenados compilados de forma nativa no admiten la disyunción (OR, IN) en la cláusula WHERE de las consultas. Cree consultas diferentes para todos los casos.|  
|Operador|CONTAINS|No se admite este operador. Quite `CONTAINS` del procedimiento almacenado compilado de forma nativa.|  
|Operador|FREETEXT|No se admite este operador. Quite `FREETEXT` del procedimiento almacenado compilado de forma nativa.|  
|Operador|NOT|No se admite este operador. Quite `NOT` del procedimiento almacenado compilado de forma nativa. En algunos casos, `NOT` se puede reemplazar por una desigualdad. Por ejemplo, `NOT a=b` se puede reemplazar por `a!=b`.|  
|Operador|TSEQUAL|No se admite este operador. Quite `TSEQUAL` del procedimiento almacenado compilado de forma nativa.|  
|Operador|LIKE|No se admite este operador. Quite `LIKE` del procedimiento almacenado compilado de forma nativa.|  
|Operador|NEXT VALUE FOR|En los procedimientos almacenados compilados de forma nativa no se puede hacer referencia a secuencias. Obtenga el valor usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado y, a continuación, páselo al procedimiento almacenado compilado de forma nativa. Para obtener más información, vea [Implementar IDENTITY en una tabla con optimización para memoria](implementing-identity-in-a-memory-optimized-table.md).|  
|Opción SET|*Opción*|En los procedimientos almacenados compilados de forma nativa no se pueden cambiar las opciones SET. Algunas opciones se pueden establecer con la instrucción BEGIN ATOMIC. Para obtener más información, vea la sección sobre bloques atomic en [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Operando|TABLESAMPLE|No se admite este operador. Quite `TABLESAMPLE` del procedimiento almacenado compilado de forma nativa.|  
|Opción|RECOMPILE|Los procedimientos almacenados compilados de forma nativa se compilan en el momento de su creación. Para volver a compilar un procedimiento almacenado compilado de forma nativa, quítelo y vuelva a crearlo. Quitar `RECOMPILE` desde la definición del procedimiento.|  
|Opción|ENCRYPTION|Esta opción no se admite. Quitar `ENCRYPTION` desde la definición del procedimiento.|  
|Opción|FOR REPLICATION|Los procedimientos almacenados compilados de forma nativa no se pueden crear para replicación. Quite `FOR REPLICATION` de la definición de procedimiento.|  
|Opción|FOR XML|Esta opción no se admite. Quite `FOR XML` del procedimiento almacenado compilado de forma nativa.|  
|Opción|FOR BROWSE|Esta opción no se admite. Quite `FOR BROWSE` del procedimiento almacenado compilado de forma nativa.|  
|Sugerencia de combinación|HASH, MERGE|Los procedimientos almacenados compilados de forma nativa solo admiten las combinaciones de bucles anidados. No se admiten las combinaciones de mezcla ni las combinaciones de hash. Quite la sugerencia de combinación.|  
|Sugerencia de consulta|*Sugerencia de consulta*|Esta sugerencia de consulta no está en los procedimientos almacenados compilados de forma nativa. Para conocer las sugerencias de consulta compatibles, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).|  
|Opción|DISTINCT|Esta opción no se admite. Quite `DISTINCT` de la consulta del procedimiento almacenado compilado de forma nativa.|  
|Opción|PERCENT|Esta opción no se admite con cláusulas `TOP`. Quite `PERCENT` de la consulta del procedimiento almacenado compilado de forma nativa.|  
|Opción|WITH TIES|Esta opción no se admite con cláusulas `TOP`. Quite `WITH TIES` de la consulta del procedimiento almacenado compilado de forma nativa.|  
|Aggregate, función|*Función de agregado*|Esta la cláusula no se admite. Para obtener más información acerca de las funciones de agregado en los procedimientos almacenados compilados de forma nativa, vea [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Función de categoría|*Función de categoría*|Los procedimientos almacenados compilados de forma nativa no admiten funciones de categoría. Quítelas de la definición de procedimiento.|  
|Función|*Función*|Esta función no se admite. Quítela del procedimiento almacenado compilado de forma nativa.|  
|.|*Instrucción*|Esta instrucción no se admite. Quítela del procedimiento almacenado compilado de forma nativa.|  
|Característica|MIN y MAX utilizados con las cadenas de caracteres y binarias|En los procedimientos almacenados compilados de forma nativa no se pueden usar las funciones de agregado `MIN` y `MAX` con valores de cadenas de caracteres y binarias.|  
|Característica|GROUP BY sin función de agregado|En los procedimientos almacenados compilados de forma nativa, cuando una consulta tiene una cláusula `GROUP BY`, la consulta también debe usar una función de agregado en la cláusula SELECT o HAVING. Agregue una función de agregado a la consulta.|  
|Característica|GROUP BY ALL|En los procedimientos almacenados compilados de forma nativa, ALL no se puede utilizar con cláusulas GROUP BY. Quite ALL de la cláusula GROUP BY.|  
|Característica|GROUP BY ()|No se admite la agrupación por una lista vacía. Quite la cláusula GROUP BY o incluya las columnas en la lista de agrupación.|  
|Característica|ROLLUP|En los procedimientos almacenados compilados de forma nativa, `ROLLUP` no se puede utilizar con cláusulas `GROUP BY`. Quitar `ROLLUP` desde la definición del procedimiento.|  
|Característica|CUBE|En los procedimientos almacenados compilados de forma nativa, `CUBE` no se puede utilizar con cláusulas `GROUP BY`. Quitar `CUBE` desde la definición del procedimiento.|  
|Característica|GROUPING SETS|En los procedimientos almacenados compilados de forma nativa, `GROUPING SETS` no se puede utilizar con cláusulas `GROUP BY`. Quitar `GROUPING SETS` desde la definición del procedimiento.|  
|Característica|BEGIN TRANSACTION, COMMIT TRANSACTION y ROLLBACK TRANSACTION|Utilice bloques ATÓMICOS para controlar las transacciones y tratar los errores. Para obtener más información, consulte [Atomic Blocks](atomic-blocks-in-native-procedures.md).|  
|Característica|Declaraciones de variable de tabla alineada.|Las variables de tabla deben hacer referencia explícitamente a los tipos definidos de tabla optimizada para memoria. Debe crear un tipo de tabla optimizada para memoria y usar ese tipo para la declaración de la variable, en lugar de especificar el tipo insertado.|  
|Característica|sp_recompile|No se permite recompilar los procedimientos almacenados compilados de forma nativa. Quite y vuelva a crear el procedimiento.|  
|Característica|EXECUTE AS CALLER|La cláusula `EXECUTE AS` es obligatoria. Pero `EXECUTE AS CALLER` no se admite. Use `EXECUTE AS OWNER`, `EXECUTE AS` *usuario*, o `EXECUTE AS SELF`.|  
|Característica|Tablas basadas en disco|No se puede tener acceso a las tablas basadas en disco desde procedimientos almacenados compilados de forma nativa. Quite las referencias a las tablas basadas en disco desde los procedimientos almacenados compilados de forma nativa. O bien, migre las tablas basadas en disco a la memoria optimizada.|  
|Característica|Vistas|No se puede tener acceso a las vistas desde procedimientos almacenados compilados de forma nativa. En lugar de a las vistas, haga referencia a las tablas base subyacentes.|  
|Característica|Funciones con valores de tabla|En los procedimientos almacenados compilados de forma nativa no se puede hacer tener acceso a funciones con valores de tabla. Quite las referencias a las funciones con valores de tabla desde los procedimientos almacenados compilados de forma nativa.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>Transacciones que tienen acceso a tablas con optimización para memoria  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con transacciones que tienen acceso a tablas optimizadas para memoria, así como la acción correctiva para resolver el error.  
  
|Tipo|NOMBRE|Solución|  
|----------|----------|----------------|  
|Característica|punto de retorno|No se pueden crear puntos de retorno explícitos en transacciones que tienen acceso a tablas optimizadas para memoria.|  
|Característica|Transacción enlazada|Las sesiones enlazadas no pueden participar en transacciones que tienen acceso a tablas optimizadas para memoria. No enlace la sesión antes de ejecutar el procedimiento.|  
|Característica|DTC|Las transacciones que tienen acceso a tablas optimizadas para memoria no pueden ser transacciones distribuidas.|  
  
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
