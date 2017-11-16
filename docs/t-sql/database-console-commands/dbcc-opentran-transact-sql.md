---
title: DBCC OPENTRAN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3d3b47d9bc553edd49f6f401d1a1c7a857d0a7d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

DBCC OPENTRAN ayuda a identificar las transacciones activas que pueden evitar el truncamiento del registro. DBCC OPENTRAN muestra información acerca de la transacción activa más antigua y las transacciones distribuidas y no distribuidas replicadas más antiguas, si las hubiera, dentro del registro de transacciones de la base de datos especificada. Solo se presentan resultados si hay una transacción activa que existe en el registro o si la base de datos contiene información de replicación. Si no hay transacciones activas en el registro, se muestra un mensaje informativo.
  
> [!NOTE]  
>  DBCC OPENTRAN no se admite para publicadores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] ) ]  
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id*| 0  
 Es el nombre o el identificador de la base de datos de la que se va a presentar la información de la transacción más antigua. Si no se especifica o se especifica 0, se utiliza la base de datos actual. Nombres de base de datos deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 TABLERESULTS  
 Especifica los resultados en un formato tabular que se puede cargar en una tabla. Utilice esta opción para crear una tabla de resultados que se pueda insertar en una tabla y hacer comparaciones. Cuando no se especifica esta opción, se da formato a los resultados de modo que sean legibles.  
  
 NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Comentarios  
Utilice DBCC OPENTRAN para determinar si hay alguna transacción abierta dentro del registro de transacciones. Cuando utiliza la instrucción BACKUP LOG, solo puede truncar la parte inactiva del registro; una transacción abierta puede evitar que el registro se trunque completamente. Para identificar una transacción abierta, utilice sp_who para obtener el Id. del proceso del sistema.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC OPENTRAN devuelve el siguiente conjunto de resultados cuando no hay transacciones abiertas:
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="examples"></a>Ejemplos  
### <a name="a-returning-the-oldest-active-transaction"></a>A. Devolver la transacción activa más antigua  
En el ejemplo siguiente se obtiene información de transacción para la base de datos actual. Los resultados pueden variar.
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Transaction information for database 'master'.
Oldest active transaction:
SPID (server process ID) : 52
UID (user ID) : -1
Name          : user_transaction
LSN           : (518:1576:1)
Start time    : Jun  1 2004  3:30:07:197PM
SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
  
> [!NOTE]  
>  El resultado "UID (user ID)" no tiene ningún sentido y se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. Especificar la opción WITH TABLERESULTS  
El siguiente ejemplo carga los resultados del comando DBCC OPENTRAN en una tabla temporal.
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[Confirmar transacción &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Db_id &#40; Transact-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  

