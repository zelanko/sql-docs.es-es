---
title: DBCC SHRINKFILE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 94ad5652920129790045e33c93e2a8fbb83816bd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduce el tamaño del archivo de datos o de registro para la base de datos actual, o vacía un archivo moviendo los datos del archivo especificado a otros archivos del mismo grupo, lo que permite quitar el archivo de la base de datos. Puede reducir un archivo a un tamaño menor que el tamaño especificado cuando se creó. Así se restablece el tamaño mínimo de archivo al valor nuevo.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*file_name*  
Es el nombre lógico del archivo que se va a reducir.
  
*file_id*  
Es el número de identificación (Id.) del archivo que se va a reducir. Para obtener un identificador de archivo, utilice la [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) función del sistema o consulta el [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) vista en la base de datos de catálogo.
  
*target_size*  
Es el tamaño para el archivo, en megabytes, expresado como un número entero. Si no se especifica, DBCC SHRINKFILE reduce el tamaño al predeterminado del archivo. El tamaño predeterminado es el que se especificó cuando se creó el archivo.
  
> [!NOTE]  
>  Puede reducir el tamaño predeterminado de un archivo vacío utilizando DBCC SHRINKFILE *target_size*. Por ejemplo, si crea un archivo de 5 MB y, a continuación, reduce el archivo a 3 MB mientras el archivo todavía está vacío, el tamaño de archivo predeterminado se establece en 3 MB. Esto solo se aplica para vaciar archivos que nunca han contenido datos.  
  
Esta opción no se admite para los contenedores del grupo de archivos FILESTREAM.  
Si *target_size* se especifica, DBCC SHRINKFILE intenta reducir el archivo al tamaño especificado. Las páginas utilizadas de la parte del archivo que se va a liberar se vuelven a ubicar en el espacio disponible de la parte del archivo que se va a mantener. Por ejemplo, si hay un archivo de datos de 10 MB, una operación DBCC SHRINKFILE con un *target_size* 8 hace todas las páginas usadas en los últimos 2 MB del archivo se asignen de nuevo en las páginas no asignadas en los primeros 8 MB del archivo. DBCC SHRINKFILE no reduce un archivo a un tamaño menor que el que se necesita para almacenar los datos en el archivo. Por ejemplo, si se utilizan 7 MB de un archivo de datos de 10 MB, una instrucción DBCC SHRINKFILE con un *target_size* de 6 reduce el archivo a 7 MB, no 6 MB.
  
EMPTYFILE  
Migra todos los datos desde el archivo especificado a otros archivos en el **mismo grupo de archivos**. En otras palabras, EmptyFile migrará los datos desde el archivo especificado a otros archivos en el mismo grupo de archivos. Emptyfile garantiza que no hay nuevos datos se agregarán al archivo. El archivo se puede quitar mediante la [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrucción.
Para los contenedores del grupo de archivos FILESTREAM, no se puede quitar el archivo mediante ALTER DATABASE hasta que el recopilador de elementos no utilizados de FILESTREAM haya ejecutado y eliminado todos los archivos innecesarios del contenedor del grupo de archivos que EMPTYFILE ha copiado en otro contenedor. Para obtener más información, consulte [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  Para obtener información acerca de cómo quitar un contenedor de FILESTREAM, vea la sección correspondiente en [modificar el archivo de base de datos y opciones de grupo de archivos &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
NOTRUNCATE  
Mueve las páginas asignadas del final de un archivo de datos a páginas no asignadas del principio del archivo con o sin especificar *porcentaje deseado*. El espacio disponible del final del archivo no se devuelve al sistema operativo y el tamaño físico del archivo no cambia. Por tanto, si se especifica NOTRUNCATE, parecerá que el archivo no se reduce.
NOTRUNCATE solo es aplicable a archivos de datos. No afecta a los archivos de registro.   Esta opción no se admite para los contenedores del grupo de archivos FILESTREAM.
  
TRUNCATEONLY  
Devuelve al sistema operativo todo el espacio disponible del final del archivo, pero no realiza ningún movimiento de página dentro del archivo. El archivo de datos solo se reduce hasta el último tamaño asignado.
*target_size* se omite si se especifica con TRUNCATEONLY.  
La opción TRUNCATEONLY no mueve la información en el registro, pero quita VLF inactivos del final del archivo de registro. Esta opción no se admite para los contenedores del grupo de archivos FILESTREAM.
  
WITH NO_INFOMSGS  
Suprime todos los mensajes de información.
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describen las columnas del conjunto de resultados.
  
|Nombre de columna|Description|  
|---|---|
|**DbId**|Número de identificación de la base de datos del archivo que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**FileId**|El número de identificación de archivo del archivo de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**CurrentSize**|El número de páginas de 8 KB que el archivo ocupa actualmente.|  
|**MinimumSize**|El número de páginas de 8 KB que el archivo podría ocupar, como mínimo. Esto corresponde al tamaño mínimo o tamaño de creación original de un archivo.|  
|**UsedPages**|El número de páginas de 8 KB que utiliza actualmente el archivo.|  
|**EstimatedPages**|El número de páginas de 8 KB al que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima que se puede reducir el archivo.|  
  
## <a name="remarks"></a>Comentarios  
DBCC SHRINKFILE se aplica a los archivos de la base de datos actual. Para obtener más información sobre cómo cambiar la base de datos actual, vea [usar &#40; Transact-SQL &#41; ](../../t-sql/language-elements/use-transact-sql.md).
  
Las operaciones DBCC SHRINKFILE pueden detenerse en cualquier momento del proceso y se mantiene el trabajo completado.
  
Cuando se produce un error en una operación DBCC SHRINKFILE, se produce un error.
  
 La base de datos que se está reduciendo no tiene por qué estar en modo de usuario único; otros usuarios pueden estar trabajando en la base de datos cuando el archivo se está reduciendo. No es necesario ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único para reducir las bases de datos del sistema.  
  
## <a name="shrinking-a-log-file"></a>Reducir un archivo de registro  
Para los archivos de registro, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] utiliza *target_size* para calcular el tamaño final del registro entero; por lo tanto, *target_size* es la cantidad de espacio libre en el registro después de la operación de reducción. El tamaño final del registro entero se traduce, entonces, en el tamaño final de cada archivo de registro. DBCC SHRINKFILE intenta reducir cualquier archivo de registro físico a su tamaño final de forma inmediata. Sin embargo, si parte del registro lógico está en los registros virtuales más allá del tamaño final, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] libera tanto espacio como sea posible y a continuación emite un mensaje informativo. El mensaje indica las acciones que se deben llevar a cabo para mover el registro lógico de los registros virtuales al final del archivo. Una vez realizadas estas acciones, se puede usar DBCC SHRINKFILE para liberar el espacio restante.
  
Como un archivo de registro solo puede reducirse al límite de un archivo de registro virtual, puede que no sea posible reducirlo a un tamaño menor que el de un archivo de registro virtual, aunque no esté siendo utilizado. El tamaño del archivo de registro virtual se elige dinámicamente el [!INCLUDE[ssDE](../../includes/ssde-md.md)] cuando se crean o se extienden los archivos de registro.
  
## <a name="best-practices"></a>Procedimientos recomendados  
Tenga en cuenta la siguiente información cuando vaya a reducir un archivo:
-   La reducción es más efectiva después de una operación que cree mucho espacio inutilizado, como por ejemplo una operación para truncar o eliminar tablas.  
-   La mayoría de las bases de datos requieren que haya espacio disponible para realizar las operaciones diarias normales. Si se reduce una base de datos en forma reiterada y su tamaño vuelve a aumentar, esto indica que el espacio que se redujo es necesario para las operaciones normales. En estos casos, no sirve reducir la base de datos reiteradamente.  
-   La reducción no mantiene el estado de fragmentación de los índices de la base de datos y generalmente aumenta la fragmentación hasta cierto punto. Esta es otra razón para no reducir la base de datos reiteradamente.  
-   Reduzca varios archivos en la misma base de datos de forma secuencial en lugar de simultáneamente. La contención en las tablas del sistema puede provocar retrasos debido al bloqueo.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
En esta sección se describe el modo de diagnosticar y corregir los problemas que pueden ocurrir al ejecutar el comando DBCC SHRINKFILE:
  
### <a name="the-file-does-not-shrink"></a>El archivo no se reduce  
Si la operación de reducción se ejecuta sin errores, pero parece que el archivo no ha cambiado de tamaño, compruebe que el archivo tiene espacio disponible para quitar realizando una de las siguientes operaciones:
- Ejecute la siguiente consulta.  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   Ejecute el [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) comando para devolver el espacio utilizado en el registro de transacciones.  
Si no hay suficiente espacio disponible, la operación de reducción no puede reducir más el tamaño del archivo.
  
Normalmente es el archivo de registro el que parece no reducirse. Esto suele deberse a que dicho archivo no se ha truncado. Puede truncar el registro estableciendo el modelo de recuperación de la base de datos en SIMPLE o realizando una copia de seguridad del registro y ejecutando a continuación la operación DBCC SHRINKFILE nuevamente.
  
### <a name="the-shrink-operation-is-blocked"></a>La operación de reducción está bloqueada  
Es posible que las operaciones de reducción estar bloqueado por una transacción que se está ejecutando un [nivel de aislamiento basado en las versiones de fila](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por ejemplo, si se está ejecutando una operación de eliminación grande con un nivel de aislamiento basado en versiones de fila cuando se ejecuta una operación DBCC SHRINK DATABASE, la operación de reducción esperará a que la operación de eliminación se haya completado antes de reducir los archivos. Cuando esto sucede, las operaciones DBCC SHRINKFILE y DBCC SHRINKDATABASE imprimen un mensaje informativo (5202 en el caso de SHRINKDATABASE y 5203 para SHRINKFILE) en el registro de errores de SQL Server cada cinco minutos durante la primera hora, y cada hora sucesivamente. Por ejemplo, si el registro de errores contiene el siguiente mensaje de error, se producirá el siguiente error:
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Esto significa que la operación de reducción está bloqueada por transacciones de instantánea que tienen marcas de tiempo anteriores a 109, que es la última transacción que ha completado la operación de reducción. También indica que la **transaction_sequence_num**, o **first_snapshot_sequence_num** columnas en la [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) vista de administración dinámica contiene un valor de 15. Si el **transaction_sequence_num**, o **first_snapshot_sequence_num** columnas de la vista contiene un número menor que la última transacción completada mediante una operación de reducción (109), el reducir operación esperará a que las transacciones finalicen.
  
Para resolver el problema, puede llevar a cabo una de las tareas siguientes:
-   Finalizar la transacción que está bloqueando la operación de reducción.
-   Finalizar la operación de reducción. Si finaliza la operación de reducción, se conservará todo el trabajo completado.  
-   No hacer nada y permitir que la operación de reducción espere a que finalice la transacción que la está bloqueando.  
  
## <a name="permissions"></a>Permissions  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-shrinking-a-data-file-to-a-specified-target-size"></a>A. Reducir un archivo de datos a un tamaño final especificado  
En el siguiente ejemplo se reduce el tamaño de un archivo de datos denominado `DataFile1` en el `UserDB` base de datos de usuario a 7 MB.
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="b-shrinking-a-log-file-to-a-specified-target-size"></a>B. Reducir un archivo de registro a un tamaño final especificado  
En el ejemplo siguiente se reduce el archivo de registro de la base de datos `AdventureWorks` a 1 MB. Para permitir que el comando DBCC SHRINKFILE reduzca el archivo, primero hay que truncar el archivo estableciendo el modelo de recuperación de la base de datos en SIMPLE.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. Truncar un archivo de datos  
En el ejemplo siguiente se trunca el archivo de datos principal en la base de datos `AdventureWorks`. Se consulta la vista de catálogo `sys.database_files` para obtener el valor de `file_id` del archivo de datos.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. Vaciar un archivo  
En el ejemplo siguiente se ilustra el procedimiento para vaciar un archivo de forma que se pueda quitar de la base de datos. Para los fines de este ejemplo, se crea primero un archivo de datos y se supone que el archivo contiene datos.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[Reducir un archivo](../../relational-databases/databases/shrink-a-file.md)
  
  
