---
title: Transacciones (almacenamiento de datos SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ea7244857dcd25b1e36f3420811ef035d4ee3b2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-sql-data-warehouse"></a>Transacciones (almacenamiento de datos SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Una transacción es un grupo de una o varias instrucciones de base de datos totalmente confirmado o revertido completamente. Cada transacción es atómicas, coherentes, aisladas y duraderas (ACID). Si la transacción se realiza correctamente, se confirman todas las instrucciones dentro de él. Si se produce un error en la transacción, que es al menos una de las instrucciones en el grupo se produce un error, a continuación, se revierte todo el grupo.  
  
 Principio y al final de transacciones depende de la configuración de confirmación automática y las instrucciones BEGIN TRANSACTION, COMMIT y ROLLBACK. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]admite los siguientes tipos de transacciones:  
  
-   *Las transacciones explícitas* inicio con la instrucción BEGIN TRANSACTION y terminan con la instrucción COMMIT o ROLLBACK.  
  
-   *Transacciones de confirmación automática* iniciar automáticamente dentro de una sesión y no se inician con la instrucción BEGIN TRANSACTION. Cuando el valor de confirmación automática es ON, cada instrucción se ejecuta en una transacción y no es necesario realizar ninguna confirmación explícita o reversión. Cuando el valor de confirmación automática es OFF, se requiere una instrucción COMMIT o ROLLBACK para determinar el resultado de la transacción. En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], transacciones de confirmación automática comiencen inmediatamente después de una instrucción COMMIT o ROLLBACK, o después de una instrucción SET AUTOCOMMIT OFF.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Marca el punto inicial de una transacción explícita.  
  
 CONFIRMACIÓN [TRABAJO]  
 Marca el final de una transacción explícita o de confirmación automática. Esta instrucción hace que los cambios en la transacción para confirmarse permanentemente a la base de datos. La instrucción COMMIT será idéntica a la instrucción COMMIT TRANSACTION, COMMIT WORK y COMMIT TRAN.  
  
 REVERSIÓN [TRABAJO]  
 Revierte una transacción al principio de la transacción. Ningún cambio para la transacción se confirman en la base de datos. La instrucción ROLLBACK es idéntica a ROLLBACK WORK, ROLLBACK TRAN y ROLLBACK TRANSACTION.  
  
 CONFIRMACIÓN AUTOMÁTICA DE CONJUNTO { **ON** | {OFF}  
 Determina cómo pueden iniciar y finalizar las transacciones.  
  
 ON  
 Cada instrucción se ejecuta en su propia transacción y ninguna instrucción COMMIT o ROLLBACK explícita es necesaria. Las transacciones explícitas se permiten al AUTOCOMMIT es ON.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]inicia automáticamente una transacción cuando una transacción no está en curso. Las siguientes instrucciones se ejecutan como parte de la transacción y una confirmación o reversión es necesaria para determinar el resultado de la transacción. Tan pronto como una transacción se confirma o revierte en este modo de funcionamiento, el modo permanece en OFF, y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia una nueva transacción. No se permiten transacciones explícitas cuando AUTOCOMMIT es OFF.  
  
 Si cambia la configuración de confirmación automática dentro de una transacción activa, la configuración afecta a la transacción actual y no tiene efecto hasta que se complete la transacción.  
  
 Si AUTOCOMMIT es ON, ejecuta otra instrucción SET AUTOCOMMIT ON tiene ningún efecto. Del mismo modo, si AUTOCOMMIT es OFF, ejecuta otra SET AUTOCOMMIT OFF tiene ningún efecto.  
  
 SET IMPLICIT_TRANSACTIONS {ON | **OFF** }  
 Esto cambia los mismos modos de confirmación automática establecido. Cuando ON, SET IMPLICIT_TRANSACTIONS establece la conexión en el modo de transacción implícita. Cuando OFF, restablece la conexión al modo de confirmación automática.  Para obtener más información, vea [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 No hay permisos específicos deben ejecutar las instrucciones relacionadas con la transacción. Se requieren permisos para ejecutar las instrucciones dentro de la transacción.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si se ejecutan COMMIT o ROLLBACK y no hay ninguna transacción activa, se produce un error.  
  
 Si se ejecuta una instrucción BEGIN TRANSACTION mientras una transacción ya está en curso, se produce un error. Esto puede ocurrir si una instrucción BEGIN TRANSACTION se produce después de una instrucción BEGIN TRANSACTION correcta o cuando la sesión está en AUTOCOMMIT SET OFF.  
  
 Si un error que no sea un error de tiempo de ejecución instrucción impide la finalización correcta de una transacción explícita, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] automáticamente revierte la transacción y libera todos los recursos mantenidos por la transacción. Por ejemplo, si conexión de red del cliente a una instancia de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se interrumpe o el cliente cierra la aplicación, se deshacen las transacciones no confirmadas para la conexión cuando la red notifica a la instancia de la interrupción.  
  
 Si se produce un error de tiempo de ejecución instrucción en un lote, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se comporta coherente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT** establecido en **ON** y se revierte la transacción entera. Para obtener más información sobre la **XACT_ABORT** configuración, vea [SET XACT_ABORT (Transact-SQL)](http://msdn.microsoft.com/library/ms188792.aspx).  
  
## <a name="general-remarks"></a>Notas generales  
 Una sesión puede ejecutar solo una transacción en un momento dado; puntos de retorno y transacciones anidadas no son compatibles.  
  
 Es responsabilidad de la [!INCLUDE[DWsql](../../includes/dwsql-md.md)] programador confirmación solo en un momento cuando todos los datos al que hace referencia la transacción sea lógicamente correcto.  
  
 Cuando se termina una sesión antes de que finalice una transacción, se revierte la transacción.  
  
 Modos de transacción se administran en el nivel de sesión. Por ejemplo, si una sesión inicia una transacción explícita o confirmación automática establece en OFF o IMPLICIT_TRANSACTIONS establece en ON, no tiene ningún efecto en los modos de transacción de cualquier otra sesión.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede revertir una transacción después de que se emita una instrucción COMMIT porque las modificaciones de datos no se ha realizado una parte permanente de la base de datos.  
  
 La [crear base de datos &#40; Almacenamiento de datos SQL de Azure &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) y [Eliminar base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md) comandos no se puede usar dentro de una transacción explícita.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]no tiene una transacción mecanismo de uso compartido. Esto implica que en cualquier momento dado, solo una sesión puede esté realizando un trabajo en cualquier transacción en el sistema.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]utiliza el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios tienen acceso a datos al mismo tiempo. El bloqueo se utiliza por las transacciones implícitas y explícitas. Cada transacción solicita bloqueos de diferentes tipos en los recursos, como tablas o bases de datos de los que depende la transacción. Todos los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bloqueos son tabla nivel o superior. Estos bloqueos impiden que otras transacciones puedan modificar los recursos de forma que esto provoque problemas para la transacción que solicita el bloqueo. Cada transacción libera sus bloqueos cuando ya no tiene una dependencia en los recursos bloqueados; las transacciones explícitas mantener bloqueos hasta que la transacción finaliza cuando se confirma o revierte.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. Uso de una transacción explícita  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Revertir una transacción  
 En el ejemplo siguiente se muestra el efecto de revertir una transacción.  En este ejemplo, la instrucción ROLLBACK deshará la instrucción INSERT, pero sigue existiendo la tabla creada.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. Configuración de confirmación automática  
 En el ejemplo siguiente se establece el valor de confirmación automática en `ON`.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 En el ejemplo siguiente se establece el valor de confirmación automática en `OFF`.  
  
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
  
## <a name="see-also"></a>Vea también  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
