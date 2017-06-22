---
title: Construcciones Transact-SQL no admitidas por OLTP en memoria | Microsoft Docs
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 66f9964d94ebcbab021c9dcf69ae50663196a597
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>Construcciones Transact-SQL no admitidas por OLTP en memoria
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Las tablas con optimización para memoria, los procedimientos almacenados compilados de forma nativa y las funciones definidas por el usuario no admiten el área expuesta completa de [!INCLUDE[tsql](../../includes/tsql-md.md)] , pero las tablas basadas en disco, los procedimientos almacenados interpretados de [!INCLUDE[tsql](../../includes/tsql-md.md)] y las funciones definidas por el usuario sí la admiten. Cuando se intenta usar una de las características no admitidas, el servidor devuelve un error.  
  
 El mensaje de error menciona el tipo de instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] (por ejemplo, característica, operación, opción) y el nombre de la característica o palabra clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La mayor parte de características no admitidas devolverán el error 10794, con un mensaje de error que indique la función no admitida. En las tablas siguientes se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto del mensaje de error, así como la acción correctiva para resolver el error.  
  
 Para obtener más información sobre las características admitidas con las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa, vea:  
  
-   [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [Compatibilidad de Transact-SQL con OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
-   [Características de SQL Server no admitidas para OLTP en memoria](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>Bases de datos que utilizan OLTP en memoria  
 En la siguiente tabla se enumeran las características de [!INCLUDE[tsql](../../includes/tsql-md.md)] no compatibles y las palabras clave que pueden aparecer en el texto del mensaje de error que implica una base de datos OLTP en memoria. La tabla también muestra la resolución del error.  
  
|Tipo|Nombre|Solución|  
|----------|----------|----------------|  
|Opción|AUTO_CLOSE|La opción de base de datos AUTO_CLOSE=ON no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Opción|ATTACH_REBUILD_LOG|La opción de base de datos ATTACH_REBUILD_LOG de CREATE no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|DATABASE SNAPSHOT|La creación de instantáneas de base de datos no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|Replicación con el sync_method 'database snapshot' o 'database snapshot character'|La replicación con sync_method 'database snapshot' o 'database snapshot character' no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Característica|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB omite las tablas con optimización para memoria en la base de datos.<br /><br /> DBCC CHECKTABLE producirá un error en las tablas con optimización para memoria.|  
  
## <a name="memory-optimized-tables"></a>Tablas con optimización para memoria  
 En la siguiente tabla se enumeran las características de [!INCLUDE[tsql](../../includes/tsql-md.md)] no compatibles y las palabras clave que pueden aparecer en el texto del mensaje de error que implica una tabla con optimización para memoria. La tabla también muestra la resolución del error.  
  
|Tipo|Nombre|Solución|  
|----------|----------|----------------|  
|Característica|ON|Las tablas con optimización para memoria no se pueden colocar en un grupo de archivos ni en un esquema de partición. Quite la cláusula ON de la instrucción **CREATE TABLE** .<br /><br /> Todas las tablas con optimización para memoria se asignan al grupo de archivos con optimización para memoria.|  
|Tipo de datos|*Nombre del tipo de datos*|No se admite el tipo de datos indicado. Reemplace el tipo por uno de los tipos de datos admitidos. Para obtener más información, vea [Tipos de datos admitidos para OLTP en memoria](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).|  
|Característica|Columnas calculadas|Las tablas con optimización para memoria no admiten columnas calculadas. Quite las columnas calculadas de la instrucción **CREATE TABLE** .<br/><br/>**Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.<br/>A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, se admiten columnas calculadas en tablas e índices optimizados para memoria.|  
|Característica|Replicación|La replicación no es compatible con las tablas con optimización para memoria.|  
|Característica|FILESTREAM|Las columnas de las tablas con optimización para memoria no admiten el almacenamiento FILESTREAM. Quite la palabra clave **FILESTREAM** de la definición de columna.|  
|Característica|SPARSE|Las columnas de las tablas con optimización para memoria no se pueden definir como columnas SPARSE. Quite la palabra clave **SPARSE** de la definición de columna.|  
|Característica|ROWGUIDCOL|Las columnas de las tablas con optimización para memoria no admiten la opción ROWGUIDCOL. Quite la palabra clave **ROWGUIDCOL** de la definición de columna.|  
|Característica|FOREIGN KEY|En tablas con optimización para memoria, las restricciones FOREIGN KEY solo se admiten para claves externas que hacen referencia a las claves principales. Quite la restricción de la definición de tabla si la clave externa hace referencia a una restricción única.|  
|Característica|índice clúster|Especifique un índice no clúster. Si se trata de un índice de clave principal, no se olvide de especificar **PRIMARY KEY NONCLUSTERED [HASH]**.|  
|Característica|DDL dentro de transacciones|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar en el contexto de una transacción de usuario. No inicie ninguna transacción y asegúrese de que el parámetro de sesión IMPLICIT_TRANSACTIONS está establecido en OFF antes de ejecutar la instrucción CREATE o DROP.|  
|Característica|DDL, desencadenadores|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar si existe un desencadenador de base de datos o de servidor para la operación DDL. Quite los desencadenadores de servidor y de base de datos de CREATE/DROP TABLE y CREATE/DROP PROCEDURE.|  
|Característica|EVENT NOTIFICATION|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no se pueden crear ni quitar si existe una notificación de evento de base de datos o de servidor para la operación DDL. Quite las notificaciones de eventos de servidor y de base de datos en CREATE TABLE o DROP TABLE y CREATE PROCEDURE o DROP PROCEDURE.|  
|Característica|FileTable|Las tablas con optimización para memoria no se pueden crear como tablas de archivos. Quite el argumento **AS FileTable** de la instrucción **CREATE TABLE** .|  
|Operación|Actualización de columnas de clave principal|Las columnas de clave principal de las tablas con optimización para memoria y los tipos de tablas no se pueden actualizar. Si es necesario actualizar la clave principal, elimine la fila antigua e inserte la nueva fila con la clave principal actualizada.|  
|Operación|CREATE INDEX|Los índices de las tablas con optimización para memoria deben especificarse insertados con la instrucción **CREATE TABLE** o con la instrucción **ALTER TABLE** .|  
|Operación|CREATE FULLTEXT INDEX|Las tablas con optimización para memoria no admiten índices de texto completo.|  
|Operación|Cambios en los esquemas|Las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa no admiten cambios en los esquemas, por ejemplo, **sp_rename**.<br /><br /> El intento de realizar algunos cambios de esquema generará el error 12320. No se admiten las operaciones que requieren un cambio en la versión de esquema, como cambiar el nombre, con tablas con optimización para memoria.<br /><br /> Se permiten algunos cambios de esquema que usen ALTER TABLE y ALTER PROCEDURE.<br/><br/>**Se aplica a:** [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)].<br/>A partir de [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)], sp_rename se admite.| 
|Operación|TRUNCATE TABLE|Las tablas con optimización para memoria no admiten la operación TRUNCATE. Para quitar todas las filas de una tabla, elimínelas con **DELETE FROM***table* , o bien quite y vuelva a crear la tabla.|  
|Operación|ALTER AUTHORIZATION|No es posible cambiar el propietario de una tabla con optimización para memoria o de un procedimiento almacenado compilado de forma nativa existente. Para cambiar el propietario, quite y vuelva a crear la tabla o el procedimiento.|  
|Operación|ALTER SCHEMA|Transferencia de un elemento protegible entre esquemas.|  
|Operación|DBCC CHECKTABLE|DBCC CHECKTABLE no es compatible con las tablas con optimización para memoria.|  
|Característica|ANSI_PADDING OFF|Cuando se crean tablas con optimización para memoria o procedimientos almacenados compilados de forma nativa, la opción de sesión **ANSI_PADDING** debe estar establecida en ON. Ejecute **SET ANSI_PADDING ON** antes de ejecutar la instrucción CREATE.|  
|Opción|DATA_COMPRESSION|Las tablas con optimización para memoria no admiten la compresión de datos. Quite la opción de la definición de tabla.|  
|Característica|DTC|No se puede tener acceso a las tablas con optimización para memoria ni a los procedimientos almacenados compilados de forma nativa desde transacciones distribuidas. En su lugar, use transacciones SQL.|  
|Operación|Tablas con optimización para memoria como destino de MERGE|Las tablas con optimización para memoria no pueden ser el destino de una operación **MERGE** . En su lugar, use las instrucciones **INSERT**, **UPDATE**o **DELETE** .|  
  
## <a name="indexes-on-memory-optimized-tables"></a>Índices de las tablas con optimización para memoria  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con un índice de una tabla con optimización para memoria, así como la acción correctiva para resolver el error.  
  
|Tipo|Nombre|Solución|  
|----------|----------|----------------|  
|Característica|Índice filtrado|Las tablas con optimización para memoria no admiten índices filtrados. Omita la cláusula **WHERE** en la especificación de índice.|  
|Característica|Columnas incluidas|No es necesario especificar columnas incluidas en las tablas con optimización para memoria. Todas las columnas de la tabla con optimización para memoria se incluyen de forma implícita en cada índice con optimización para memoria.|  
|Operación|DROP INDEX|No es posible quitar los índices de las tablas con optimización para memoria. Puede eliminar los índices mediante ALTER TABLE.<br /><br /> Para obtener más información, vea [Modificar tablas con optimización para memoria](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).|  
|Opción de índice|*Opción de índice*|Solo se admite una opción de índice (BUCKET_COUNT) para los índices HASH.|  
  
## <a name="nonclustered-hash-indexes"></a>Índices de hash no clúster  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con un índice de hash no clúster, así como la acción correctiva para resolver el error.  
  
|Tipo|Nombre|Solución|  
|----------|----------|----------------|  
|Opción|ASC/DESC|Los índices de hash no clúster no se ordenan. Quite las palabras clave **ASC** y **DESC** de la especificación de clave de índice.|  
  
## <a name="natively-compiled-stored-procedures-and-user-defined-functions"></a>Procedimientos almacenados compilados de forma nativa y funciones definidas por el usuario  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con procedimientos almacenados compilados de forma nativa y funciones definidas por el usuario, así como la acción correctiva para resolver el error.  
  
|Tipo|Característica|Solución|  
|----------|-------------|----------------|  
|Característica|Variables de las tablas insertadas|Los tipos de tablas no pueden declararse insertadas con declaraciones de variable. Los tipos de tablas deben declararse de forma explícita mediante una instrucción **CREATE TYPE** .|  
|Característica|Cursores|Los procedimientos almacenados compilados de forma nativa no admiten cursores.<br /><br /> Cuando ejecute el procedimiento desde el cliente, utilice RPC en lugar de la API de cursores. Con ODBC, evite la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . **EXECUTE**; en su lugar, especifique el nombre del procedimiento directamente.<br /><br /> Cuando ejecute el procedimiento desde un lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] o desde otro procedimiento almacenado, evite usar un cursor con el procedimiento almacenado compilado de forma nativa.<br /><br /> Cuando cree un procedimiento almacenado compilado de forma nativa, en lugar de un cursor, use la lógica basada en conjunto o un bucle **WHILE** .|  
|Característica|Valores predeterminados de parámetros no constantes|Cuando se usan los valores predeterminados de los parámetros en procedimientos almacenados compilados de forma nativa, dichos valores deben ser constantes. Quite los caracteres comodín de las declaraciones de parámetro.|  
|Característica|EXTERNAL|Los procedimientos almacenados CLR no se pueden compilar de forma nativa. Quite la cláusula AS EXTERNAL o la opción de NATIVE_COMPILATION de la instrucción CREATE PROCEDURE.|  
|Característica|Procedimientos almacenados numerados|Los procedimientos almacenados compilados de forma nativa no se pueden numerar. Quite **;***number* de la instrucción **CREATE PROCEDURE** .|  
|Característica|Instrucciones INSERT … VALUES de varias filas|En un procedimiento almacenado compilado de forma nativa no se pueden insertar varias filas usando la misma instrucción **INSERT** . Cree instrucciones **INSERT** para cada fila.|  
|Característica|Expresiones de tabla común (CTE)|Los procedimientos almacenados compilados de forma nativa no admiten expresiones de tabla común (CTE). Vuelva a escribir la consulta.|  
|Característica|COMPUTE|No se admite la cláusula **COMPUTE** . Quítela de la consulta.|  
|Característica|SELECT INTO|La cláusula **INTO** no se puede usar con la instrucción **SELECT** . Vuelva a escribir la consulta como **p INTO***Table***SELECT**.|  
|Característica|Lista de columnas insertadas incompleta|En general, en las instrucciones INSERT, deben especificarse valores para todas las columnas de la tabla.<br /><br /> Sin embargo, se admiten las restricciones DEFAULT y las columnas IDENTITY(1,1) en tablas optimizadas para memoria. Estas columnas pueden omitirse de la lista de columnas INSERT. En el caso de columnas IDENTITY, la omisión es obligatoria.|  
|Característica|*Función*|Los procedimientos almacenados compilados de forma nativa no admiten algunas funciones integradas. Quite la función rechazada del procedimiento almacenado. Para obtener más información sobre las funciones integradas admitidas, vea<br />[Características admitidas en los módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)o<br />[Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Característica|CASE|Los procedimientos almacenados compilados de forma nativa no admiten la instrucción **CASE** en las consultas. Cree consultas diferentes para mayúsculas y minúsculas. Para obtener más información, vea [Implementación de una expresión CASE de un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md).|  
|Característica|INSERT EXECUTE|Quite la referencia.|  
|Característica|Ejecute|Solo se admite para ejecutar procedimientos almacenados de forma nativa y funciones definidas por el usuario.|  
|Característica|agregados definidos por el usuario|En los procedimientos almacenados compilados de forma nativa no se pueden usar funciones de agregado definidas por el usuario. Quite la referencia a la función del procedimiento.|  
|Característica|Metadatos en el modo de exploración|Los procedimientos almacenados compilados de forma nativa no admiten metadatos en el modo de exploración. Asegúrese de que la opción de sesión **NO_BROWSETABLE** está establecida en OFF.|  
|Característica|DELETE con la cláusula FROM|Los procedimientos almacenados compilados de forma nativa no admiten la cláusula **FROM** en instrucciones **DELETE** con un origen de tabla.<br /><br /> **DELETE** con la cláusula **FROM** se admite cuando se emplea para indicar la tabla en la que hay que realizar la eliminación.|  
|Característica|UPDATE con la cláusula FROM|Los procedimientos almacenados compilados de forma nativa no admiten la cláusula **FROM** en instrucciones **UPDATE** .|  
|Característica|Procedimientos temporales|Los procedimientos almacenados temporales no se pueden compilar de forma nativa. Cree un procedimiento almacenado compilado de forma nativa que sea permanente o un procedimiento almacenado interpretado de [!INCLUDE[tsql](../../includes/tsql-md.md)] que sea temporal.|  
|Nivel de aislamiento|READ UNCOMMITTED|Los procedimientos almacenados compilados de forma nativa no admiten el nivel de aislamiento READ UNCOMMITTED. Use un nivel de aislamiento compatible, como SNAPSHOT.|  
|Nivel de aislamiento|READ COMMITTED|Los procedimientos almacenados compilados de forma nativa no admiten el nivel de aislamiento READ COMMITTED. Use un nivel de aislamiento compatible, como SNAPSHOT.|  
|Característica|tablas temporales|En los procedimientos almacenados compilados de forma nativa no se pueden usar tablas de tempdb. En su lugar, use una variable de tabla o una tabla con optimización para memoria con DURABILITY=SCHEMA_ONLY.|  
|Característica|DTC|No se puede tener acceso a las tablas con optimización para memoria ni a los procedimientos almacenados compilados de forma nativa desde transacciones distribuidas. En su lugar, use transacciones SQL.|  
|Característica|EXECUTE WITH RECOMPILE|Los procedimientos almacenados compilados de forma nativa no admiten la opción **WITH RECOMPILE** .|  
|Característica|Ejecución de la conexión de administrador dedicada|Los procedimientos almacenados compilados de forma nativa no se pueden ejecutar desde la conexión de administrador dedicada (DAC). En su lugar, use una conexión normal.|  
|Operación|punto de retorno|Los procedimientos almacenados compilados de forma nativa no se pueden invocar desde transacciones que tienen un punto de retorno activo. Quite el punto retorno de la transacción.|  
|Operación|ALTER AUTHORIZATION|No es posible cambiar el propietario de una tabla con optimización para memoria o de un procedimiento almacenado compilado de forma nativa existente. Para cambiar el propietario, quite y vuelva a crear la tabla o el procedimiento.|  
|Operador|OPENROWSET|No se admite este operador. Quite **OPENROWSET** del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENQUERY|No se admite este operador. Quite **OPENQUERY** del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENDATASOURCE|No se admite este operador. Quite **OPENDATASOURCE** del procedimiento almacenado compilado de forma nativa.|  
|Operador|OPENXML|No se admite este operador. Quite **OPENXML** del procedimiento almacenado compilado de forma nativa.|  
|Operador|CONTAINSTABLE|No se admite este operador. Quite **CONTAINSTABLE** del procedimiento almacenado compilado de forma nativa.|  
|Operador|FREETEXTTABLE|No se admite este operador. Quite **FREETEXTTABLE** del procedimiento almacenado compilado de forma nativa.|  
|Característica|Funciones con valores de tabla|En los procedimientos almacenados compilados de forma nativa no se puede hacer referencia a funciones con valores de tabla. Una solución posible para esta restricción es agregar la lógica de las funciones con valores de tabla al cuerpo del procedimiento.|  
|Operador|CHANGETABLE|No se admite este operador. Quite **CHANGETABLE** del procedimiento almacenado compilado de forma nativa.|  
|Operador|GOTO|No se admite este operador. Use otras construcciones de procedimiento, como WHILE.|  
|Operador|OFFSET|No se admite este operador. Quite **OFFSET** del procedimiento almacenado compilado de forma nativa.|  
|Operador|INTERSECT|No se admite este operador. Quite **INTERSECT** del procedimiento almacenado compilado de forma nativa. En algunos casos se puede usar INNER JOIN para obtener el mismo resultado.|  
|Operador|EXCEPT|No se admite este operador. Quite **EXCEPT** del procedimiento almacenado compilado de forma nativa.|  
|Operador|APPLY|No se admite este operador. Quite **APPLY** del procedimiento almacenado compilado de forma nativa.<br/><br/>**Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.<br/>A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, el operador APPLY se admite en los módulos compilados de forma nativa.|  
|Operador|PIVOT|No se admite este operador. Quite **PIVOT** del procedimiento almacenado compilado de forma nativa.|  
|Operador|UNPIVOT|No se admite este operador. Quite **UNPIVOT** del procedimiento almacenado compilado de forma nativa.|  
|Operador|CONTAINS|No se admite este operador. Quite **CONTAINS** del procedimiento almacenado compilado de forma nativa.|  
|Operador|FREETEXT|No se admite este operador. Quite **FREETEXT** del procedimiento almacenado compilado de forma nativa.|  
|Operador|TSEQUAL|No se admite este operador. Quite **TSEQUAL** del procedimiento almacenado compilado de forma nativa.|  
|Operador|LIKE|No se admite este operador. Quite **LIKE** del procedimiento almacenado compilado de forma nativa.|  
|Operador|NEXT VALUE FOR|En los procedimientos almacenados compilados de forma nativa no se puede hacer referencia a secuencias. Obtenga el valor usando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado y, a continuación, páselo al procedimiento almacenado compilado de forma nativa. Para obtener más información, vea [Implementar IDENTITY en una tabla con optimización para memoria](../../relational-databases/in-memory-oltp/implementing-identity-in-a-memory-optimized-table.md).|  
|Opción SET|*Opción*|En los procedimientos almacenados compilados de forma nativa no se pueden cambiar las opciones SET. Algunas opciones se pueden establecer con la instrucción BEGIN ATOMIC. Para obtener más información, vea la sección sobre bloques atomic en [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Operando|TABLESAMPLE|No se admite este operador. Quite **TABLESAMPLE** del procedimiento almacenado compilado de forma nativa.|  
|Opción|RECOMPILE|Los procedimientos almacenados compilados de forma nativa se compilan en el momento de su creación. Quite **RECOMPILE** de la definición de procedimiento.<br /><br /> Si ejecuta sp_recompile en un procedimiento almacenado compilado de forma nativa, hará que se vuelva a compilar en la siguiente ejecución.|  
|Opción|ENCRYPTION|Esta opción no se admite. Quite **ENCRYPTION** de la definición de procedimiento.|  
|Opción|FOR REPLICATION|Los procedimientos almacenados compilados de forma nativa no se pueden crear para replicación. Quite **FOR REPLICATION** de la definición de procedimiento.|  
|Opción|FOR XML|Esta opción no se admite. Quite **FOR XML** del procedimiento almacenado compilado de forma nativa.|  
|Opción|FOR BROWSE|Esta opción no se admite. Quite **FOR BROWSE** del procedimiento almacenado compilado de forma nativa.|  
|Sugerencia de combinación|HASH, MERGE|Los procedimientos almacenados compilados de forma nativa solo admiten las combinaciones de bucles anidados. No se admiten las combinaciones de mezcla ni las combinaciones de hash. Quite la sugerencia de combinación.|  
|Sugerencia de consulta|*Sugerencia de consulta*|Esta sugerencia de consulta no está en los procedimientos almacenados compilados de forma nativa. Para conocer las sugerencias de consulta compatibles, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).|  
|Opción|PERCENT|Esta opción no se admite con cláusulas **TOP** . Quite **PERCENT** de la consulta del procedimiento almacenado compilado de forma nativa.|  
|Opción|WITH TIES|Esta opción no se admite con cláusulas **TOP** . Quite **WITH TIES** de la consulta del procedimiento almacenado compilado de forma nativa.|  
|Aggregate, función|*Función de agregado*|Esta la cláusula no se admite. Para obtener más información acerca de las funciones de agregado en los procedimientos almacenados compilados de forma nativa, vea [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Función de categoría|*Función de categoría*|Los procedimientos almacenados compilados de forma nativa no admiten funciones de categoría. Quítelas de la definición de procedimiento.|  
|Función|*Función*|Esta función no se admite. Quítela del procedimiento almacenado compilado de forma nativa.|  
|.|*Instrucción*|Esta instrucción no se admite. Quítela del procedimiento almacenado compilado de forma nativa.|  
|Característica|MIN y MAX utilizados con las cadenas de caracteres y binarias|En los procedimientos almacenados compilados de forma nativa no se pueden usar las funciones de agregado **MIN** y **MAX** con valores de cadenas de caracteres y binarias.|  
|Característica|GROUP BY ALL|En los procedimientos almacenados compilados de forma nativa, ALL no se puede utilizar con cláusulas GROUP BY. Quite ALL de la cláusula GROUP BY.|  
|Característica|GROUP BY ()|No se admite la agrupación por una lista vacía. Quite la cláusula GROUP BY o incluya las columnas en la lista de agrupación.|  
|Característica|ROLLUP|En los procedimientos almacenados compilados de forma nativa,**ROLLUP** no se puede utilizar con cláusulas **GROUP BY** . Quite **ROLLUP** de la definición de procedimiento.|  
|Característica|CUBE|En los procedimientos almacenados compilados de forma nativa,**CUBE** no se puede utilizar con cláusulas **GROUP BY** . Quite **CUBE** de la definición de procedimiento.|  
|Característica|GROUPING SETS|En los procedimientos almacenados compilados de forma nativa,**GROUPING SETS** no se puede utilizar con cláusulas **GROUP BY** . Quite **GROUPING SETS** de la definición de procedimiento.|  
|Característica|BEGIN TRANSACTION, COMMIT TRANSACTION y ROLLBACK TRANSACTION|Utilice bloques ATÓMICOS para controlar las transacciones y tratar los errores. Para obtener más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).|  
|Característica|Declaraciones de variable de tabla alineada.|Las variables de tabla deben hacer referencia explícitamente a los tipos definidos de tabla con optimización para memoria. Debe crear un tipo de tabla con optimización para memoria y usar ese tipo para la declaración de la variable, en lugar de especificar el tipo insertado.|  
|Característica|Tablas basadas en disco|No se puede tener acceso a las tablas basadas en disco desde procedimientos almacenados compilados de forma nativa. Quite las referencias a las tablas basadas en disco desde los procedimientos almacenados compilados de forma nativa. O bien, migre las tablas basadas en disco a la memoria optimizada.|  
|Característica|Vistas|No se puede tener acceso a las vistas desde procedimientos almacenados compilados de forma nativa. En lugar de a las vistas, haga referencia a las tablas base subyacentes.|  
|Característica|Funciones con valores de tabla|En los procedimientos almacenados compilados de forma nativa no se puede hacer tener acceso a funciones con valores de tabla. Quite las referencias a las funciones con valores de tabla desde los procedimientos almacenados compilados de forma nativa.|  
|Opción|PRINT|Quitar referencia|  
|Característica|DDL|No se admite ninguna DDL.|  
|Opción|STATISTICS XML|No compatible. Al ejecutar una consulta con STATISTICS XML habilitada, el contenido XML se devuelve sin la parte del procedimiento almacenado compilado de forma nativa.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>Transacciones que tienen acceso a tablas con optimización para memoria  
 En la tabla siguiente se enumeran las características y las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden aparecer en el texto de un mensaje de error relacionado con transacciones que tienen acceso a tablas con optimización para memoria, así como la acción correctiva para resolver el error.  
  
|Tipo|Nombre|Solución|  
|----------|----------|----------------|  
|Característica|punto de retorno|No se pueden crear puntos de retorno explícitos en transacciones que tienen acceso a tablas con optimización para memoria.|  
|Característica|Transacción enlazada|Las sesiones enlazadas no pueden participar en transacciones que tienen acceso a tablas con optimización para memoria. No enlace la sesión antes de ejecutar el procedimiento.|  
|Característica|DTC|Las transacciones que tienen acceso a tablas con optimización para memoria no pueden ser transacciones distribuidas.|  
  
## <a name="see-also"></a>Vea también  
 [Migrar a OLTP en memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  

