---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: 62
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: e6022b5609c2d4b4d362f90088bee4e84ad874c7
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
ms.locfileid: "34236416"
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduce el tamaño de los archivos de datos y de registro de la base de datos especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id* | 0  
 Es el nombre o id. de la base de datos que se va a reducir. Si se especifica 0, se utiliza la base de datos actual.  
  
 *target_percent*  
 Es el porcentaje de espacio disponible que se desea dejar en el archivo de la base de datos después de reducir la base de datos.  
  
 NOTRUNCATE  
 Compacta los datos de archivos de datos moviendo páginas asignadas del final de un archivo a páginas no asignadas del principio del archivo. *target_percent* es opcional. Esta opción no es compatible con Azure SQL Data Warehouse. 
  
 El espacio disponible del final del archivo no se devuelve al sistema operativo y el tamaño físico del archivo no cambia. Por tanto, si se especifica NOTRUNCATE, parecerá que la base de datos no se reduce.  
  
 NOTRUNCATE solo es aplicable a archivos de datos. No afecta al archivo de registro.  
  
 TRUNCATEONLY  
 Devuelve al sistema operativo todo el espacio disponible del final del archivo, pero no realiza ningún movimiento de página dentro del archivo. El archivo de datos solo se reduce hasta el último tamaño asignado. *target_percent* se omite si se especifica con TRUNCATEONLY. Esta opción no es compatible con Azure SQL Data Warehouse.
  
 TRUNCATEONLY afecta al archivo de registro. Para truncar solo el archivo de datos, use DBCC SHRINKFILE.  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describen las columnas del conjunto de resultados.
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**DbId**|Número de identificación de la base de datos del archivo que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**FileId**|Número de identificación del archivo que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**CurrentSize**|El número de páginas de 8 KB que el archivo ocupa actualmente.|  
|**MinimumSize**|El número de páginas de 8 KB que el archivo podría ocupar, como mínimo. Esto corresponde al tamaño mínimo o tamaño de creación original de un archivo.|  
|**UsedPages**|El número de páginas de 8 KB que utiliza actualmente el archivo.|  
|**EstimatedPages**|El número de páginas de 8 KB al que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima que se puede reducir el archivo.|  
  
>[!NOTE]
> El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no presenta filas para los archivos que no se reducen.  
  
## <a name="remarks"></a>Notas  

>[!NOTE]
> Actualmente, Azure SQL Data Warehouse no admite DBCC SHRINKDATABASE. No se recomienda ejecutar este comando, ya que se trata de una operación de uso intensivo de E/S y puede dejar el almacén de datos sin conexión. Además, después de ejecutar este comando habrá implicaciones económicas para sus instantáneas del almacén de datos. 

Para reducir todos los archivos de datos y de registro de una base de datos específica, ejecute el comando DBCC SHRINKDATABASE. Para reducir un archivo de datos o de registro de cada vez para una base de datos específica, ejecute el comando [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).
  
Para ver la cantidad actual de espacio disponible (sin asignar) en la base de datos, ejecute [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
Las operaciones SHRINKDATABASE pueden detenerse en cualquier momento del proceso y se conserva el trabajo completado hasta ese momento.
  
El tamaño de la base de datos no puede ser menor que el tamaño mínimo de la base de datos. El tamaño mínimo es el tamaño especificado cuando se creó la base de datos o el último tamaño establecido explícitamente mediante una operación de cambio de tamaño de archivo, como DBCC SHRINKFILE o ALTER DATABASE. Por ejemplo, si se creó una base de datos con un tamaño de 10 MB y ha crecido hasta llegar a 100 MB, solo podrá reducirla hasta un tamaño de 10 MB, aunque todos los datos de la base de datos se hayan eliminado.
  
Ejecutar DBCC SHRINKDATABASE sin especificar la opción NOTRUNCATE o la opción TRUNCATEONLY equivale a ejecutar una operación DBCC SHRINKDATABASE con la opción NOTRUNCATE seguida de una operación DBCC SHRINKDATABASE con TRUNCATEONLY.
  
La base de datos que se comprime no tiene que estar en modo de usuario único; otros usuarios pueden estar trabajando en la base de datos cuando ésta se está reduciendo. Esto incluye las bases de datos del sistema.
  
No se puede reducir una base de datos mientras se está realizando una copia de seguridad de la misma. Asimismo, no se puede realizar una copia de seguridad de una base de datos mientras se está realizando una operación de reducción de ésta.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Cómo funciona DBCC SHRINKDATABASE  
DBCC SHRINKDATABASE reduce los archivos de datos de uno en uno, pero reduce los archivos de registro como si todos estuvieran en una agrupación de registros contiguos.  Los archivos se reducen siempre desde el final.
  
Suponga que una base de datos llamada **mydb** tiene un archivo de datos y dos archivos de registro. Los archivos de datos y de registro tienen 10 MB cada uno, y el archivo de datos contiene 6 MB de datos.
  
Para cada archivo, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula un tamaño de destino. Este es el tamaño al que se debe reducir el archivo. Cuando DBCC SHRINKDATABASE se especifica con *target_percent*, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula el tamaño final para que quede *target_percent* de espacio disponible en el archivo tras la reducción. Por ejemplo, si establece el valor de *target_percent* en 25 para reducir **mydb**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que el tamaño final del archivo de datos será de 8 MB (6 MB de datos más 2 MB de espacio disponible). Por tanto, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] pasa los datos de los últimos 2 MB del archivo de datos al espacio disponible de los primeros 8 MB del archivo de datos y, después, reduce el archivo.
  
Suponga que el archivo de datos de **mydb** contiene 7 MB de datos. Si se especifica un *target_percent* de 30, este archivo de datos se puede reducir al porcentaje libre de 30. En cambio, si se especifica un *target_percent* de 40, no se reduce el archivo de datos porque el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no reducirá ningún archivo a un tamaño menor que el que los datos ocupan actualmente. O lo que es lo mismo: 40 % de espacio disponible deseado + 70 % de datos en el archivo (7 MB de 10 MB) es mayor que 100 %. Como el porcentaje de espacio disponible deseado más el porcentaje actual ocupado por los datos supera el 100 % (en un 10 %), un *target_size* superior a 30 no reducirá el archivo de datos.
  
En los archivos de registro, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa el parámetro *target_percent* para calcular el tamaño final de todo el registro, de forma que *target_percent* es la cantidad de espacio disponible en el registro después de la operación de reducción. El tamaño final del registro entero se traduce al tamaño final de cada archivo de registro.
  
DBCC SHRINKDATABASE intenta reducir cualquier archivo de registro físico a su tamaño final de forma inmediata. Si ninguna parte del registro lógico se encuentra en los registros virtuales más allá del tamaño final del archivo de registro, el archivo se trunca de manera correcta y DBCC SHRINKDATABASE finaliza sin mensajes. Sin embargo, si parte del registro lógico está en los registros virtuales más allá del tamaño final, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] libera tanto espacio como sea posible y a continuación emite un mensaje informativo. El mensaje indica las acciones que se deben llevar a cabo para mover el registro lógico de los registros virtuales al final del archivo. Después de que se realizan estas acciones, se puede utilizar DBCC SHRINKDATABASE para liberar el espacio restante.
  
Como un archivo de registro solo puede reducirse al límite de un archivo de registro virtual, puede que no sea posible reducirlo a un tamaño menor que el de un archivo de registro virtual, aunque no esté siendo utilizado. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige dinámicamente el tamaño del archivo de registro virtual cuando se crean o se extienden archivos de registro.
  
## <a name="best-practices"></a>Procedimientos recomendados  
Tenga en cuenta la siguiente información cuando vaya a reducir una base de datos:
-   La reducción es más efectiva después de una operación que cree mucho espacio inutilizado, como por ejemplo una operación para truncar o eliminar tablas.  
-   La mayoría de las bases de datos requieren que haya espacio disponible para realizar las operaciones diarias normales. Si se reduce una base de datos en forma reiterada y su tamaño vuelve a aumentar, esto indica que el espacio que se redujo es necesario para las operaciones normales. En estos casos, no sirve reducir la base de datos reiteradamente.  
-   La reducción no mantiene el estado de fragmentación de los índices de la base de datos y generalmente aumenta la fragmentación hasta cierto punto. Esta es otra razón para no reducir la base de datos reiteradamente.  
-   A menos que tenga un requisito específico, no establezca la opción de base de datos AUTO_SHRINK en ON.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 Es posible bloquear las operaciones de reducción mediante una transacción que se ejecuta con un [nivel de aislamiento basado en versiones de fila](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por ejemplo, si se está ejecutando una operación de eliminación grande con un nivel de aislamiento basado en versiones de fila cuando se ejecuta una operación DBCC SHRINK DATABASE, la operación de reducción esperará a que la operación de eliminación se haya completado antes de reducir los archivos. Cuando esto sucede, las operaciones DBCC SHRINKFILE y DBCC SHRINKDATABASE imprimen un mensaje informativo (5202 en el caso de SHRINKDATABASE y 5203 para SHRINKFILE) en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada cinco minutos durante la primera hora, y cada hora sucesivamente.   Por ejemplo, si el registro de errores contiene el siguiente mensaje de error:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Esto significa que la operación de reducción está bloqueada por transacciones de instantánea que tienen marcas de tiempo anteriores a 109, que es la última transacción que ha completado la operación de reducción. También indica que las columnas **transaction_sequence_num** o **first_snapshot_sequence_num** de la vista de administración dinámica [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) contienen el valor de 15. Si las columnas **transaction_sequence_num** o **first_snapshot_sequence_num** contienen un número inferior al de la última transacción completada mediante una operación de reducción (109), la operación de reducción esperará a que las transacciones finalicen.
  
Para resolver el problema, puede llevar a cabo una de las tareas siguientes:
-   Finalizar la transacción que está bloqueando la operación de reducción.  
-   Finalizar la operación de reducción. Se conservará todo el trabajo completado.  
-   No hacer nada y permitir que la operación de reducción espere a que finalice la transacción que la está bloqueando.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. Reducir una base de datos y especificar un porcentaje de espacio disponible  
 En este ejemplo se reduce el tamaño de los archivos de datos y de registro de la base de datos de usuario `UserDB` para dejar un 10 por ciento de espacio disponible en la base de datos.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Truncar una base de datos  
 En el ejemplo siguiente se reducen los archivos de datos y de registro en la base de datos de ejemplo `AdventureWorks` al último tamaño asignado.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>Vea también  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)
  
  
