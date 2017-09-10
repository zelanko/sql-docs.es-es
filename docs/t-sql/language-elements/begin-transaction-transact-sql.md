---
title: "COMENZAR la transacción (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN_TRANSACTION_TSQL
- TRANSACTION_TSQL
- TRANSACTION
- BEGIN TRANSACTION
- BEGIN TRAN
- BEGIN_TRAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction logs [SQL Server], BEGIN TRANSACTION statement
- marked transactions [SQL Server], BEGIN TRANSACTION statement
- BEGIN TRANSACTION statement
- local transactions [SQL Server]
- marking transactions [SQL Server]
- transactions [SQL Server], starting
- transaction names [SQL Server]
- starting point marked for transactions
- starting transactions
ms.assetid: c6258df4-11f1-416a-816b-54f98c11145e
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f52f237795de00f4ad78403bed986ac571005c31
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="begin-transaction-transact-sql"></a>BEGIN TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Marca el punto de inicio de una transacción local explícita. Las transacciones explícitas comenzar con la instrucción BEGIN TRANSACTION y terminan con la instrucción COMMIT o ROLLBACK.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
--Applies to SQL Server and Azure SQL Database
 
BEGIN { TRAN | TRANSACTION }   
    [ { transaction_name | @tran_name_variable }  
      [ WITH MARK [ 'description' ] ]  
    ]  
[ ; ]  
```  
 
```  
--Applies to Azure SQL Data Warehouse and Parallel Data Warehouse
 
BEGIN { TRAN | TRANSACTION }   
[ ; ]  
```  

  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 **Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure
 
 Es el nombre asignado a la transacción. *transaction_name* debe cumplir las reglas para identificadores, pero los identificadores de más de 32 caracteres no se permiten. Utilice nombres de transacciones solamente en la pareja más externa de instrucciones BEGIN…COMMIT o BEGIN…ROLLBACK anidadas. *transaction_name* es siempre mayúsculas de minúsculas, incluso cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no distingue mayúsculas de minúsculas.  
  
 @*tran_name_variable*  
 **Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure
 
 Se trata del nombre de una variable definida por el usuario que contiene un nombre de transacción válido. La variable debe declararse con una **char**, **varchar**, **nchar**, o **nvarchar** tipo de datos. Si se pasan más de 32 caracteres a la variable, solo se utilizarán los primeros 32; el resto de caracteres se truncará.  
  
 CON marca ['*descripción*']  
**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure

Especifica que la transacción está marcada en el registro. *descripción* es una cadena que describe la marca. A *descripción* más de 128 caracteres se truncan a 128 caracteres antes de almacenarse en la tabla msdb.dbo.logmarkhistory.  
  
 Si utiliza WITH MARK, debe especificar un nombre de transacción. WITH MARK permite restaurar un registro de transacciones hasta una marca con nombre.  
  
## <a name="general-remarks"></a>Notas generales
BEGIN TRANSACTION incrementa@TRANCOUNT en 1.
  
BEGIN TRANSACTION representa un punto en el que los datos a los que hace referencia una conexión son lógica y físicamente coherentes. Si se producen errores, se pueden revertir todas las modificaciones realizadas en los datos después de BEGIN TRANSACTION para devolver los datos al estado conocido de coherencia. Cada transacción dura hasta que se completa sin errores y se emite COMMIT TRANSACTION para hacer que las modificaciones sean una parte permanente de la base de datos, o hasta que se produzcan errores y se borren todas las modificaciones con la instrucción ROLLBACK TRANSACTION.  
  
BEGIN TRANSACTION inicia una transacción local para la conexión que emite la instrucción. Según la configuración del nivel de aislamiento de la transacción actual, la transacción bloquea muchos recursos adquiridos para aceptar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] emitidas por la conexión hasta que la misma finaliza con una instrucción COMMIT TRANSACTION o ROLLBACK TRANSACTION. Las transacciones que quedan pendientes durante mucho tiempo pueden impedir que otros usuarios tengan acceso a estos recursos bloqueados y pueden impedir también el truncamiento del registro.  
  
 Aunque BEGIN TRANSACTION inicia una transacción local, ésta no se guardará en el registro de transacciones hasta que la aplicación realice posteriormente una acción que se deba almacenar en el registro, como la ejecución de una instrucción INSERT, UPDATE o DELETE. Una aplicación puede realizar acciones tales como adquirir bloqueos para proteger el nivel de aislamiento de transacción de instrucciones SELECT, pero no se guarda ningún dato en el registro hasta que la aplicación realiza una acción de modificación.  
  
 Asignar un nombre a varias transacciones en un conjunto de transacciones anidadas afecta mínimamente a la transacción. Solamente el nombre de la primera transacción (la más externa) se registra en el sistema. Revertir a otro nombre (que no sea un nombre de punto de retorno válido) genera un error. De hecho, no se revierte ninguna de las instrucciones ejecutadas antes de la operación de revertir en el momento en que se produce este error. Solo se revierten las instrucciones cuando se revierte la transacción externa.  
  
 La transacción local iniciada por la instrucción BEGIN TRANSACTION aumenta al nivel de transacción distribuida si se realizan las siguientes acciones antes de confirmarla o revertirla:  
  
-   Se ejecuta una instrucción INSERT, DELETE o UPDATE que hace referencia a una tabla remota de un servidor vinculado. La instrucción INSERT, UPDATE o DELETE se produce un error si el proveedor de OLE DB utilizado para tener acceso al servidor vinculado no es compatible con la interfaz ITransactionJoin.  
  
-   Se realiza una llamada a un procedimiento almacenado remoto cuando la opción REMOTE_PROC_TRANSACTIONS es ON.  
  
 La copia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se convierte en el controlador de la transacción y utiliza el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) para administrar la transacción distribuida.  
  
 Una transacción se puede ejecutar explícitamente como una transacción distribuida utilizando BEGIN DISTRIBUTED TRANSACTION. Para obtener más información, vea [BEGIN DISTRIBUTED TRANSACTION &#40; Transact-SQL &#41; ](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Cuando SET IMPLICIT_TRANSACTIONS está configurado en ON, una instrucción BEGIN TRANSACTION abrirá dos transacciones anidadas. Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)  
  
## <a name="marked-transactions"></a>Transacciones marcadas  
 La opción WITH MARK coloca el nombre de la transacción en el registro de transacciones. Al restaurar una base de datos a su estado anterior, se puede utilizar la transacción marcada en lugar de la fecha y la hora. Para obtener más información, vea [usar transacciones marcadas para recuperar las bases de datos relacionadas sistemáticamente &#40; Modelo de recuperación completa &#41; ](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) y [restauración &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Además, se necesitan las marcas del registro de transacciones si tiene la intención de recuperar un conjunto de bases de datos relacionadas a un estado coherente lógicamente. Una transacción distribuida puede colocar marcas en los registros de transacción de las bases de datos relacionadas. Recuperar el conjunto de bases de datos relacionadas hasta estas marcas da como resultado un conjunto de bases de datos coherente en cuanto a las transacciones. La colocación de las marcas en las bases de datos relacionadas requiere procedimientos especiales.  
  
 La marca se coloca en el registro de transacciones solamente si la transacción marcada actualiza la base de datos. No se marcan las transacciones que no modifican los datos.  
  
 BEGIN TRAN *new_name* WITH MARK puede anidarse dentro de una transacción existente que no esté marcada. De ese modo, *new_name* se convierte en el nombre de marca de la transacción, a pesar de que el nombre que la transacción ya se han asignado. En el siguiente ejemplo, `M2` es el nombre de la marca.  
  
```  
BEGIN TRAN T1;  
UPDATE table1 ...;  
BEGIN TRAN M2 WITH MARK;  
UPDATE table2 ...;  
SELECT * from table1;  
COMMIT TRAN M2;  
UPDATE table3 ...;  
COMMIT TRAN T1;  
```  
  
 Al anidar transacciones, intentar marcar una transacción ya marcada da lugar a un mensaje de advertencia (no de error):  
  
 "BEGIN TRAN T1 WITH MARK ...;"  
  
 "UPDATE tabla1 ...;"  
  
 "BEGIN TRAN M2 WITH MARK ...;"  
  
 "Servidor: mensaje 3920, nivel 16, estado 1, línea 3"  
  
 "La opción WITH MARK solo se aplica a la primera instrucción BEGIN TRAN WITH MARK."  
  
 "Se omitirá la opción."  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-an-explicit-transaction"></a>A. Uso de una transacción explícita
**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure, almacenamiento de datos de SQL Azure, almacenamiento de datos paralelos

Este ejemplo utiliza AdventureWorks. 

```
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```

### <a name="b-rolling-back-a-transaction"></a>B. Revertir una transacción
**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure, almacenamiento de datos de SQL Azure, almacenamiento de datos paralelos

En el ejemplo siguiente se muestra el efecto de revertir una transacción. En este ejemplo, la instrucción ROLLBACK deshará la instrucción INSERT, pero sigue existiendo la tabla creada.

```
 
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  

```

### <a name="c-naming-a-transaction"></a>C. Asignar un nombre a una transacción 
**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure

En el siguiente ejemplo se muestra cómo asignar un nombre a una transacción.  
  
```  
DECLARE @TranName VARCHAR(20);  
SELECT @TranName = 'MyTransaction';  
  
BEGIN TRANSACTION @TranName;  
USE AdventureWorks2012;  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
  
COMMIT TRANSACTION @TranName;  
GO  
```  
  
### <a name="d-marking-a-transaction"></a>D. Marcar una transacción  
**Se aplica a:** (a partir de 2008) de SQL Server, base de datos de SQL Azure

En el siguiente ejemplo se muestra cómo marcar una transacción. Se marca la transacción `CandidateDelete`.  
  
```  
BEGIN TRANSACTION CandidateDelete  
    WITH MARK N'Deleting a Job Candidate';  
GO  
USE AdventureWorks2012;  
GO  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
GO  
COMMIT TRANSACTION CandidateDelete;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [TRABAJO de confirmación &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

