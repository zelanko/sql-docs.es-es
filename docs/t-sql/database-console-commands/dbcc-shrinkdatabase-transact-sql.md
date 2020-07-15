---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: e36315d58721fc6c50393b0bff10c7e8a2e3dee0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757208"
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Reduce el tamaño de los archivos de datos y de registro de la base de datos especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
_nombre\_base de datos_ | _id\_base de datos_ | 0  
Es el nombre o id. de la base de datos que se va a reducir. 0 especifica que se usa la base de datos actual.  
  
_porcentaje\_destino_  
Es el porcentaje de espacio disponible que se desea dejar en el archivo de la base de datos después de reducir la base de datos.  
  
NOTRUNCATE  
Desplaza las páginas asignadas desde el final del archivo a páginas no asignadas en el principio del archivo. Esta acción compacta los datos dentro del archivo. _porcentaje\_destino_ es opcional. Azure SQL Data Warehouse no admite esta opción. 
  
El espacio disponible al final del archivo no se devuelve al sistema operativo, y el tamaño físico del archivo no cambia. Por tanto, parece que la base de datos no se reduce cuando se especifica NOTRUNCATE.  
  
NOTRUNCATE solo es aplicable a archivos de datos. NOTRUNCATE no afecta al archivo de registro.  
  
TRUNCATEONLY  
Libera todo el espacio libre al final del archivo en el sistema operativo. Dentro del archivo no se mueve ninguna página. El archivo de datos se reduce solo a la última extensión asignada. Omite _porcentaje\_destino_ si se especifica con TRUNCATEONLY. Azure SQL Data Warehouse no admite esta opción.
  
TRUNCATEONLY afecta al archivo de registro. Para truncar solo el archivo de datos, use DBCC SHRINKFILE.  
  
WITH NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describen las columnas del conjunto de resultados.
  
|Nombre de la columna|Descripción|  
|-----------------|-----------------|  
|**DbId**|Número de identificación de la base de datos del archivo que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**FileId**|Número de identificación del archivo que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] intentó reducir.|  
|**CurrentSize**|El número de páginas de 8 KB que el archivo ocupa actualmente.|  
|**MinimumSize**|El número de páginas de 8 KB que el archivo podría ocupar, como mínimo. Este valor se corresponde al tamaño mínimo o tamaño de creación original de un archivo.|  
|**UsedPages**|El número de páginas de 8 KB que utiliza actualmente el archivo.|  
|**EstimatedPages**|El número de páginas de 8 KB al que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima que se puede reducir el archivo.|  
  
>[!NOTE]
> El [!INCLUDE[ssDE](../../includes/ssde-md.md)] no presenta filas para los archivos que no se reducen.  
  
## <a name="remarks"></a>Observaciones  

>[!NOTE]
> Actualmente, Azure SQL Data Warehouse no admite DBCC SHRINKDATABASE. No se recomienda ejecutar este comando, ya que se trata de una operación de uso intensivo de E/S y puede dejar el almacén de datos sin conexión. Además, después de ejecutar este comando habrá implicaciones económicas para sus instantáneas del almacén de datos. 

Para reducir todos los archivos de datos y de registro de una base de datos específica, ejecute el comando DBCC SHRINKDATABASE. Para reducir un archivo de datos o de registro de cada vez para una base de datos específica, ejecute el comando [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).
  
Para ver la cantidad actual de espacio disponible (sin asignar) en la base de datos, ejecute [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
Las operaciones DBCC SHRINKDATABASE se pueden detener en cualquier momento del proceso y se conserva el trabajo completado hasta ese momento.
  
El tamaño de la base de datos no puede ser menor que el tamaño mínimo configurado de la base de datos. El tamaño mínimo se especifica cuando se crea originalmente la base de datos. O bien, el tamaño mínimo puede ser el último tamaño establecido de forma explícita mediante un operación de cambio de tamaño de archivo. DBCC SHRINKFILE o ALTER DATABASE son ejemplos de operaciones de cambio de tamaño de archivo. 

Supongamos que una base de datos se ha creado originalmente con un tamaño de 10 MB. Después, aumenta a 100 MB. El tamaño mínimo al que se puede reducir la base de datos es de 10 MB, incluso si se han eliminado todos los datos de la base de datos.
  
Al ejecutar DBCC SHRINKDATABASE, especifique las opciones NOTRUNCATE o TRUNCATEONLY. Si no lo hace, el resultado es el mismo que si ejecuta una operación DBCC SHRINKDATABASE con la opción NOTRUNCATE seguida de una operación DBCC SHRINKDATABASE con TRUNCATEONLY.
  
No es necesario que la base de datos reducida esté en modo de usuario único. Otros usuarios pueden estar trabajando en la base de datos cuando se reduce, incluidas las bases de datos del sistema.
  
No se puede reducir una base de datos mientras se está realizando una copia de seguridad de la misma. Por el contrario, no se puede realizar una copia de seguridad de una base de datos mientras se está realizando una operación de reducción en ella.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Cómo funciona DBCC SHRINKDATABASE  
DBCC SHRINKDATABASE reduce los archivos de datos de uno en uno, pero reduce los archivos de registro como si todos estuvieran en una agrupación de registros contiguos. Los archivos se reducen siempre desde el final.
  
Suponga que tiene un par de archivos de registro, un archivo de datos y una base de datos denominada **mydb**. Los archivos de datos y de registro tienen 10 MB cada uno, y el archivo de datos contiene 6 MB de datos. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula un tamaño de destino para cada archivo. Este valor es el tamaño al que se va a reducir el archivo. Cuando DBCC SHRINKDATABASE se especifica con _porcentaje\_destino_, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula el tamaño final para que quede _porcentaje\_destino_ de espacio disponible en el archivo tras la reducción. 

Por ejemplo, si establece el valor de _porcentaje\_destino_ en 25 para reducir **mydb**, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que el tamaño de destino del archivo de datos será de 8 MB (6 MB de datos más 2 MB de espacio disponible). Por tanto, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] pasa los datos de los últimos 2 MB del archivo de datos al espacio disponible de los primeros 8 MB del archivo de datos y, después, reduce el archivo.
  
Suponga que el archivo de datos de **mydb** contiene 7 MB de datos. Si se especifica un _porcentaje\_destino_ de 30, este archivo de datos se puede reducir al porcentaje libre de 30. Pero si se especifica un _porcentaje\_destino_ de 40, no se reduce el archivo de datos porque el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no reducirá ningún archivo a un tamaño menor que el que los datos ocupan actualmente. 

Este problema también se puede considerar de otra manera: 40 % de espacio disponible deseado + 70 % de datos en el archivo (7 MB de 10 MB) es mayor que 100 %. Cualquier valor de _tamaño\_destino_ mayor que 30 no reducirá el archivo de datos. No se reducirá porque el porcentaje de espacio disponible que quiere y el porcentaje actual que ocupa el archivo de datos es más del 100 %.
  
En los archivos de registro, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa _porcentaje\_destino_ para calcular el tamaño de destino completo del registro. Por ese motivo _porcentaje\_destino_ es la cantidad de espacio libre en el registro después de la operación de reducción. El tamaño final del registro entero se traduce al tamaño final de cada archivo de registro.
  
DBCC SHRINKDATABASE intenta reducir cualquier archivo de registro físico a su tamaño final de forma inmediata. Supongamos que ningún elemento del registro lógico permanece en los registros virtuales más allá del tamaño de destino del archivo de registro. Después, el archivo se trunca correctamente y DBCC SHRINKDATABASE finaliza sin mensajes. Pero si parte del registro lógico permanece en los registros virtuales más allá del tamaño final, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] libera tanto espacio como sea posible y después emite un mensaje informativo. El mensaje indica las acciones que se deben llevar a cabo para mover el registro lógico de los registros virtuales al final del archivo. Después de que se ejecuten las acciones, se puede usar DBCC SHRINKDATABASE para liberar el espacio restante.
  
Un archivo de registro solo se puede reducir a un límite de archivo de registro virtual. Por ese motivo, puede que no sea posible reducir un archivo de registro a un tamaño menor que el de un archivo de registro virtual. Puede que no sea posible incluso si no se está usando. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige dinámicamente el tamaño del archivo de registro virtual cuando se crean o se extienden archivos de registro.
  
## <a name="best-practices"></a>Prácticas recomendadas  
Tenga en cuenta la siguiente información cuando vaya a reducir una base de datos:
-   Una reducción es más efectiva después de una operación que cree espacio sin usar, como por ejemplo una operación para truncar o eliminar tablas.
-   La mayoría de las bases de datos requieren que haya espacio disponible para realizar las operaciones diarias normales. Es posible que reduzca una base de datos varias veces y observe que vuelve a aumentar de tamaño. Este crecimiento indica que el espacio reducido es necesario para las operaciones normales. En estos casos, no sirve reducir la base de datos reiteradamente.  
-   La reducción no mantiene el estado de fragmentación de los índices de la base de datos y generalmente aumenta la fragmentación hasta cierto punto. Este resultado es otra razón para no reducir la base de datos de forma repetida.  
-   A menos que tenga un requisito específico, no establezca la opción de base de datos AUTO_SHRINK en ON.  
  
## <a name="troubleshooting"></a>Solución de problemas  
Es posible bloquear las operaciones de reducción mediante una transacción que se ejecuta con un [nivel de aislamiento basado en versiones de fila](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por ejemplo, una operación de eliminación grande que se ejecuta con un nivel de aislamiento basado en versiones de fila está en curso cuando se ejecuta una operación DBCC SHRINK DATABASE. Cuando se produce esta situación, la operación de reducción esperará a que finalice la operación de eliminación antes de continuar. Cuando la operación de reducción espera, las operaciones DBCC SHRINKFILE y DBCC SHRINKDATABASE imprimen un mensaje informativo (5202 en el caso de SHRINKDATABASE y 5203 para SHRINKFILE). Este mensaje se imprime en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada cinco minutos durante la primera hora y, después, cada hora posterior. Por ejemplo, si el registro de errores contiene el siguiente mensaje de error:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Este error significa que las transacciones de instantánea que tienen marcas de tiempo anteriores a 109 bloquearán la operación de reducción. Esa transacción es la última que ha completado la operación de reducción. También indica que las columnas **transaction_sequence_num** o **first_snapshot_sequence_num** de la vista de administración dinámica [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) contienen un valor de 15. Es posible que las columnas **transaction_sequence_num** o **first_snapshot_sequence_num** de la vista contengan un número inferior al de la última transacción completada mediante una operación de reducción (109). En ese caso, la operación de reducción esperará a que esas transacciones finalicen.
  
Para resolver el problema, puede llevar a cabo una de las tareas siguientes:
-   Finalizar la transacción que bloquea la operación de reducción  
-   Finalizar la operación de reducción Se conserva todo el trabajo completado.  
-   No hacer nada y permitir que la operación de reducción espere a que finalice la transacción que la está bloqueando.  
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. Reducir una base de datos y especificar un porcentaje de espacio disponible  
En el ejemplo siguiente se reduce el tamaño de los archivos de datos y de registro de la base de datos de usuario `UserDB` para dejar un 10 % de espacio disponible en la base de datos.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Truncar una base de datos  
En el ejemplo siguiente se reducen los archivos de datos y de registro de la base de datos de ejemplo `AdventureWorks` al último tamaño asignado.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>Consulte también  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)
  
  
