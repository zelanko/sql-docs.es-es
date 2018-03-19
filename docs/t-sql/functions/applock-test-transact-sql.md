---
title: APPLOCK_TEST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f4009a151873bf989a39bc4fb91ec3a9963af9f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve información acerca de si se puede conceder o no un bloqueo para un recurso de aplicación determinado para el propietario de un bloqueo específico, sin adquirir el bloqueo. APPLOCK_TEST es una función de bloqueo de aplicación que opera en la base de datos actual. El ámbito de los bloqueos de aplicación es la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumentos  
**'** *database_principal* **'**  
Es el usuario, el rol o el rol de aplicación al que se pueden conceder permisos para los objetos de la base de datos. El autor de la llamada de la función debe ser miembro de *database_principal*, **dbo** o del rol fijo de base de datos **db_owner** para poder llamar a la función correctamente.
  
**'** *resource_name* **'**  
Es un nombre de recurso de bloqueo especificado por la aplicación cliente. La aplicación debe garantizar que el recurso es único. El nombre especificado se convierte internamente mediante un algoritmo hash en un valor que puede almacenarse en el administrador de bloqueos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name* es **nvarchar(255)** y no tiene ningún valor predeterminado. *resource_name* se compara con un binario y distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación de la base de datos actual.
  
**'** *lock_mode* **'**  
Es el modo de bloqueo que se va a obtener para un recurso determinado. *lock_mode* es **nvarchar(32)** y carece de valor predeterminado. El valor puede ser: **Shared**, **Update**, **IntentShared**, **IntentExclusive**, **Exclusive**.
  
**'** *lock_owner* **'**  
Es el propietario del bloqueo, que es el valor de *lock_owner* cuando se solicitó el bloqueo. *lock_owner* es **nvarchar(32)**. El valor puede ser **Transaction** (predeterminado) o **Session**. Si se especifica el valor predeterminado o **Transaction** explícitamente, debe ejecutarse APPLOCK_TEST desde una transacción.
  
## <a name="return-types"></a>Tipos de valores devueltos
**smallint**
  
## <a name="return-value"></a>Valor devuelto
Devuelve 0 cuando no se puede conceder el bloqueo al propietario especificado y devuelve 1 si se puede conceder el bloqueo.
  
## <a name="function-properties"></a>Propiedades de las funciones
**Nondeterministic**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente, dos usuarios (**Usuario A** y **Usuario B**) con sesiones independientes ejecutan la siguiente secuencia de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
El **Usuario A** ejecuta:
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
Después, el **Usuario B** ejecuta:
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
Después, el **Usuario A** ejecuta:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
Después, el **Usuario B** ejecuta:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
Después, el **Usuario A** y el **Usuario B** ejecutan:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
