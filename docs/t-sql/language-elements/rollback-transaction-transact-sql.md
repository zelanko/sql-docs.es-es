---
title: ROLLBACK TRANSACTION (Transact-SQL) | Documentos de Microsoft
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
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e31f62560b4061610c0d3c0ec3147110a3e84644
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Revierte una transacción explícita o implícita hasta el inicio de la transacción o hasta un punto de retorno dentro de la transacción. Puede usar ROLLBACK TRANSACTION para borrar todas las modificaciones de datos realizadas desde el inicio de la transacción o hasta un punto de retorno. También libera los recursos que mantiene la transacción.  
  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 Es el nombre asignado a la transacción en BEGIN TRANSACTION. *transaction_name* debe ajustarse a las reglas para identificadores, pero se utilizan solo los 32 primeros caracteres del nombre de transacción. Cuando se anidan transacciones, *transaction_name* debe ser el nombre de la instrucción BEGIN TRANSACTION más externa. *transaction_name* es siempre mayúsculas de minúsculas, incluso cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no distingue mayúsculas de minúsculas.  
  
 **@***tran_name_variable*  
 Se trata del nombre de una variable definida por el usuario que contiene un nombre de transacción válido. La variable debe declararse con una **char**, **varchar**, **nchar**, o **nvarchar** tipo de datos.  
  
 *savepoint_name*  
 Es *savepoint_name* de una instrucción SAVE TRANSACTION. *savepoint_name* debe ajustarse a las reglas para identificadores. Use *savepoint_name* cuando una operación de reversión condicional debería afectar a solo una parte de la transacción.  
  
 **@***savepoint_variable*  
 Es el nombre de una variable definida por el usuario que contiene un nombre de punto de retorno válido. La variable debe declararse con una **char**, **varchar**, **nchar**, o **nvarchar** tipo de datos.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Una instrucción ROLLBACK TRANSACTION no produce ningún mensaje para el usuario. Si necesita indicar advertencias en procedimientos almacenados o en desencadenadores, utilice las instrucciones RAISERROR o PRINT. RAISERROR es la instrucción más adecuada para indicar errores.  
  
## <a name="general-remarks"></a>Notas generales  
 ROLLBACK TRANSACTION sin un *savepoint_name* o *transaction_name* acumula hasta el principio de la transacción. Cuando se trata de transacciones anidadas, esta misma instrucción revierte todas las transacciones internas hasta la instrucción BEGIN TRANSACTION más externa. En ambos casos, ROLLBACK TRANSACTION disminuye la @@TRANCOUNT función del sistema en 0. ROLLBACK TRANSACTION *savepoint_name* no disminuye@TRANCOUNT.  
  
 ROLLBACK TRANSACTION no puede hacer referencia un *savepoint_name* en transacciones distribuidas iniciadas explícitamente con BEGIN DISTRIBUTED TRANSACTION u originadas a partir de una transacción local.  
  
 Una transacción no se puede revertir después de ejecutar una instrucción COMMIT TRANSACTION, excepto cuando COMMIT TRANSACTION está asociada a una transacción anidada incluida en la transacción que se revierte. En tal caso, la transacción anidada también se revertirá, incluso si ha emitido una instrucción COMMIT TRANSACTION para ella.  
  
 En una transacción se permiten nombres de puntos de retorno duplicados pero una instrucción ROLLBACK TRANSACTION que use este nombre solo revierte las transacciones realizadas hasta la instrucción SAVE TRANSACTION más reciente que también emplee este nombre.  
  
## <a name="interoperability"></a>Interoperabilidad  
 En los procedimientos almacenados, las instrucciones ROLLBACK TRANSACTION sin un *savepoint_name* o *transaction_name* revertir todas las instrucciones a la instrucción BEGIN TRANSACTION. Una instrucción ROLLBACK TRANSACTION en un procedimiento almacenado que hace que @@TRANCOUNT tenga un valor diferente cuando se completa el procedimiento almacenado que el @@TRANCOUNT valor cuando se llamó al procedimiento almacenado genera un mensaje informativo. Este mensaje no afecta a los siguientes procesos.  
  
 Si se emite la instrucción ROLLBACK TRANSACTION en un desencadenador:  
  
-   Se revierten todas las modificaciones de datos realizadas hasta ese punto de la transacción actual, incluidas las que realizó el desencadenador.  
  
-   El desencadenador continúa la ejecución del resto de las instrucciones después de la instrucción ROLLBACK. Si alguna de estas instrucciones modifica datos, no se revierten las modificaciones. La ejecución de las instrucciones restantes no activa ningún desencadenador anidado.  
  
-   Tampoco se ejecutan las instrucciones del lote después de la instrucción que activó el desencadenador.  
  
 @@TRANCOUNT se incrementa en uno al entrar en un desencadenador, incluso cuando está en modo de confirmación automática. (El sistema trata a un desencadenador como a una transacción anidada implícita.)  
  
 Las instrucciones ROLLBACK TRANSACTION de los procedimientos almacenados no afectan a las siguientes instrucciones del lote que llamó al procedimiento; se ejecutan las siguientes instrucciones del lote. Las instrucciones ROLLBACK TRANSACTION de los desencadenadores finalizan el lote que contiene la instrucción que activó el desencadenador; no se ejecutan las siguientes instrucciones del lote.  
  
 El efecto de ROLLBACK en los cursores se define mediante estas reglas:  
  
1.  Con CURSOR_CLOSE_ON_COMMIT establecido en ON, ROLLBACK cierra todos los cursores abiertos pero sin desasignarlos.  
  
2.  Con CURSOR_CLOSE_ON_COMMIT establecido en OFF, ROLLBACK no afecta a los cursores STATIC o INSENSITIVE sincrónicos abiertos o a los cursores STATIC asincrónicos que se hayan llenado completamente. Se cierran los cursores de otros tipos que estén abiertos, pero sin cancelar su asignación.  
  
3.  Un error que finaliza un lote y genera una operación de reversión interna cancela la asignación de todos los cursores declarados en el lote que contiene la instrucción errónea. Se cancela la asignación de todos los cursores independientemente de su tipo o de la configuración de CURSOR_CLOSE_ON_COMMIT. Esto incluye los cursores declarados en procedimientos almacenados a los que llama el lote con errores. Los cursores declarados en un lote  antes del lote con el error están sujetos a las reglas 1 y 2. Un error de interbloqueo es un ejemplo de este tipo de error. Una instrucción ROLLBACK emitida en un desencadenador también genera automáticamente este tipo de error.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Una instrucción ROLLBACK TRANSACTION que especifica un *savepoint_name* libera los bloqueos adquiridos más allá del punto de retorno, a excepción de las extensiones y conversiones. Estos bloqueos no se liberan y no vuelven a convertirse a su modo de bloqueo previo.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra el efecto de revertir una transacción con nombre.  
  
```  
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int;)  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
--The following statements start a named transaction,  
--insert two rows, and then roll back  
--the transaction named in the variable @TransactionName.  
--Another statement outside of the named transaction inserts two rows.  
--The query returns the results of the previous statements.  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
  
--Results  
--value  
-------------  
--3  
--4  
```  
  
## <a name="see-also"></a>Vea también  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [TRABAJO de confirmación &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

