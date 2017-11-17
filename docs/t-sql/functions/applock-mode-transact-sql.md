---
title: APPLOCK_MODE (Transact-SQL) | Documentos de Microsoft
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
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ceec0a5465187e1b470bd9eb8b1039a5b3d60aae
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el modo de bloqueo mantenido por el propietario del bloqueo en un recurso de aplicación específico. APPLOCK_MODE es una función de bloqueo de aplicación y funciona en la base de datos actual. El ámbito de los bloqueos de aplicación es la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>Argumentos  
'*database_principal*'  
Es el usuario, el rol o el rol de aplicación al que se pueden conceder permisos para los objetos de la base de datos. El llamador de la función debe ser un miembro de *database_principal*, dbo o db_owner rol fijo de base de datos para poder llamar a la función correctamente.
  
'*resource_name*'  
Es un nombre de recurso de bloqueo especificado por la aplicación cliente. La aplicación debe asegurar que el nombre del recurso sea exclusivo. El nombre especificado se convierte internamente mediante un algoritmo hash en un valor que puede almacenarse en el administrador de bloqueos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name*es **nvarchar (255)** no tiene ningún valor predeterminado. *resource_name* es binario compara y distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación de la base de datos actual.
  
'*lock_owner*'  
Es el propietario del bloqueo, que es el *lock_owner* valor cuando se solicitó el bloqueo. *lock_owner* es **nvarchar (32)**, y el valor puede ser **transacciones** (valor predeterminado) o **sesión**.
  
## <a name="return-types"></a>Tipos de valor devuelto
**nvarchar (32)**
  
## <a name="return-value"></a>Valor devuelto
Devuelve el modo de bloqueo mantenido por el propietario del bloqueo en un recurso de aplicación específico. El modo de bloqueo puede tener uno de estos valores:
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Compartido**|**Exclusivo**||  
  
*Este modo de bloqueo es una combinación de otros modos de bloqueo y no se puede adquirir explícitamente mediante el uso de sp_getapplock.
  
## <a name="function-properties"></a>Propiedades de la función
**No determinista**
  
**No indizable**
  
**No Paralelizable**
  
## <a name="examples"></a>Ejemplos  
Dos usuarios (usuario A y usuario B) con sesiones independientes ejecutan la siguiente secuencia de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
El usuario A ejecuta:
  
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
  
Después, el usuario B ejecuta:
  
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
  
Después, el usuario A ejecuta:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
Después, el usuario B ejecuta:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
A continuación, el usuario A y el usuario B ejecutan:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[APPLOCK_TEST &#40; Transact-SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

