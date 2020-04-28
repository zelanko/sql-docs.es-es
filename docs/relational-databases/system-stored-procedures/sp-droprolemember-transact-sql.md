---
title: sp_droprolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7123c1bd3fee61a3d0671a0d8fbe27c2943ba7ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124850"
---
# <a name="sp_droprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una cuenta de seguridad de un rol de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, utilice [ALTER role](../../t-sql/statements/alter-role-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>Sintaxis para SQL Server y Azure SQL Database

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Sintaxis para Azure SQL Data Warehouse y almacenamiento de datos paralelos

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`Es el nombre del rol del que se va a quitar el miembro. *role* es de **tipo sysname**y no tiene ningún valor predeterminado. el *rol* debe existir en la base de datos actual.  
  
`[ @membername = ] 'security_account'`Es el nombre de la cuenta de seguridad que se va a quitar del rol. *security_account* es de **tipo sysname**y no tiene ningún valor predeterminado. *security_account* puede ser un usuario de base de datos, otro rol de base de datos, un inicio de sesión de Windows o un grupo de Windows. *security_account* debe existir en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 sp_droprolemember quita un miembro de un rol de base de datos mediante la eliminación de una fila de la tabla sysmembers. Cuando un miembro se quita de un rol, pierde los permisos que tenía por pertenecer a tal rol.  
  
 Para quitar un usuario de un rol fijo de servidor, utilice sp_dropsrvrolemember. No es posible quitar usuarios del rol public ni quitar dbo de ningún rol.  
  
 Use sp_helpuser para ver los miembros de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol y use Alter role para agregar un miembro a un rol.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER para el rol.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se quita al usuario `JonB` del rol `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En este ejemplo se quita al usuario `JonB` del rol `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

