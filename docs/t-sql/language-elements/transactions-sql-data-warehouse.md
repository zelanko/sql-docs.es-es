---
title: Transacciones (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 21e6d25305bd6abf4a3dc4555f2148a2fe385187
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68121585"
---
# <a name="transactions-sql-data-warehouse"></a>Transacciones (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Una transacción es un grupo de una o varias instrucciones de base de datos totalmente confirmadas o totalmente revertidas. Cada transacción es atómica, coherente, aislada y durable (ACID). Si la transacción se realiza correctamente, se confirman todas las instrucciones que contiene. Si se produce un error en la transacción, es decir, se produce un error en al menos una de las instrucciones del grupo, se revierte todo el grupo.  
  
 El principio y el final de las transacciones depende de la configuración de AUTOCOMMIT y de las instrucciones BEGIN TRANSACTION, COMMIT y ROLLBACK. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] admite los siguientes tipos de transacciones:  
  
-   Las *transacciones explícitas* empiezan con la instrucción BEGIN TRANSACTION y acaban con la instrucción COMMIT o ROLLBACK.  
  
-   Las *transacciones de confirmación automática* se inician automáticamente dentro de una sesión y no se inician con la instrucción BEGIN TRANSACTION. Cuando el valor de AUTOCOMMIT es ON, cada instrucción se ejecuta en una transacción y no se necesita COMMIT o ROLLBACK de forma explícita. Cuando el valor de AUTOCOMMIT es OFF, se requiere una instrucción COMMIT o ROLLBACK para determinar el resultado de la transacción. En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], las transacciones de confirmación automática comienzan inmediatamente después de una instrucción COMMIT o ROLLBACK, o bien después de una instrucción SET AUTOCOMMIT OFF.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 BEGIN TRANSACTION  
 Marca el punto de inicio de una transacción explícita.  
  
 COMMIT [ WORK ]  
 Marca el final de una transacción explícita o de confirmación automática. Esta instrucción hace que los cambios en la transacción se confirmen permanentemente en la base de datos. La instrucción COMMIT es idéntica a COMMIT WORK, COMMIT TRAN y COMMIT TRANSACTION.  
  
 ROLLBACK [ WORK ]  
 Revierte una transacción al principio de la misma. No se confirman cambios para la transacción en la base de datos. La instrucción ROLLBACK es idéntica a ROLLBACK WORK, ROLLBACK TRAN y ROLLBACK TRANSACTION.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 Determina cómo se pueden iniciar y finalizar las transacciones.  
  
 ACTIVAR  
 Cada instrucción se ejecuta en su propia transacción y no se necesita ninguna instrucción COMMIT o ROLLBACK explícita. Las transacciones explícitas se permiten cuando AUTOCOMMIT es ON.  
  
 Apagado  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia automáticamente una transacción cuando no hay en curso una transacción. Todas las instrucciones siguientes se ejecutan como parte de la transacción y se necesita COMMIT o ROLLBACK para determinar el resultado de la transacción. Cuando una transacción se confirma o revierte en este modo de funcionamiento, el modo permanece en OFF, y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia una nueva transacción. Cuando AUTOCOMMIT es OFF las transacciones explícitas no se permiten.  
  
 Si se cambia la configuración de AUTOCOMMIT dentro de una transacción activa, la configuración afecta a la transacción actual y no tiene efecto hasta que se complete la transacción.  
  
 Si AUTOCOMMIT es ON, no tiene ningún efecto ejecutar otra instrucción SET AUTOCOMMIT ON. Del mismo modo, si AUTOCOMMIT es OFF, no tiene ningún efecto ejecutar otra instrucción SET AUTOCOMMIT OFF.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 Esto alterna los mismos modos que SET AUTOCOMMIT. Cuando es ON, SET IMPLICIT_TRANSACTIONS establece la conexión en el modo de transacción implícita. Cuando es OFF, restablece la conexión al modo de confirmación automática.  Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 No se necesitan permisos específicos para ejecutar las instrucciones relacionadas con la transacción. Se requieren permisos para ejecutar las instrucciones dentro de la transacción.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si se ejecutan COMMIT o ROLLBACK, y no hay ninguna transacción activa, se produce un error.  
  
 Si se ejecuta BEGIN TRANSACTION mientras ya hay una transacción en curso, se produce un error. Esto puede ocurrir si una instrucción BEGIN TRANSACTION se produce después de una instrucción BEGIN TRANSACTION correcta, o bien cuando la sesión está bajo SET AUTOCOMMIT OFF.  
  
 Si un error que no sea de una instrucción de tiempo de ejecución impide la terminación correcta de una transacción, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] revierte automáticamente la transacción y libera todos los recursos que mantiene. Por ejemplo, si se interrumpe la conexión de red del cliente con una instancia de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o si el cliente se desconecta de la aplicación, las transacciones pendientes de la conexión se revierten al estado anterior cuando la red notifica la interrupción a la instancia.  
  
 Si se produce un error de instrucción de tiempo de ejecución en un lote, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se comporta de forma coherente a **XACT_ABORT** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecido en **ON** y se revierte la transacción completa. Para obtener más información sobre la configuración de **XACT_ABORT**, vea [SET XACT_ABORT (Transact-SQL)](https://msdn.microsoft.com/library/ms188792.aspx).  
  
## <a name="general-remarks"></a>Notas generales  
 Una sesión solo puede ejecutar una transacción en un momento dado; no se admiten los puntos de retorno y las transacciones anidadas.  
  
 Es responsabilidad del programador de [!INCLUDE[DWsql](../../includes/dwsql-md.md)] usar COMMIT solo en el punto donde todos los datos a los que hace referencia la transacción sean lógicamente correctos.  
  
 Cuando se termina una sesión antes de que finalice una transacción, se revierte la transacción.  
  
 Los modos de transacción se administran en el ámbito de sesión. Por ejemplo, si una sesión inicia una transacción explícita o establece AUTOCOMMIT en OFF, o bien IMPLICIT_TRANSACTIONS en ON, no tiene ningún efecto en los modos de transacción de otras sesiones.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede revertir una transacción después de ejecutar una instrucción COMMIT, porque las modificaciones sobre los datos ya son parte permanente de la base de datos.  
  
 Los comandos [CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) y [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) no se pueden usar dentro de una transacción explícita.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] no tiene un mecanismo de uso compartido de transacciones. Esto implica que en cualquier momento dado, solo una sesión puede estar realizando un trabajo en otras transacciones en el sistema.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se usa el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios obtienen acceso a los datos al mismo tiempo. El bloqueo se usa tanto en transacciones implícitas como explícitas. Cada transacción solicita diferentes tipos de bloqueo en los recursos, como por ejemplo, las tablas o bases de datos de las que depende la transacción. Todos los bloqueos de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] son en el nivel de tabla o superior. Estos bloqueos impiden que otras transacciones puedan modificar los recursos de forma que esto provoque problemas para la transacción que solicita el bloqueo. Cada transacción libera sus bloqueos cuando ya no tiene una dependencia en los recursos bloqueados; las transacciones explícitas mantienen los bloqueos hasta que la transacción finaliza cuando se confirma o revierte.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. Usar una transacción explícita  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Revertir una transacción  
 En el ejemplo siguiente se muestra el efecto de revertir una transacción.  En este ejemplo, la instrucción ROLLBACK revertirá la instrucción INSERT, pero la tabla creada seguirá existiendo.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. Configuración de AUTOCOMMIT  
 En el ejemplo siguiente se establece el valor de AUTOCOMMIT en `ON`.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 En el ejemplo siguiente se establece el valor de AUTOCOMMIT en `OFF`.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Uso de una transacción implícita de múltiples instrucciones  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Consulte también  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
