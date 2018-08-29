---
title: sp_grantdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
manager: craigg
ms.openlocfilehash: 819276576c9cc266c78b4075fbd0e75cf5ad06e8
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030837"
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un usuario de base de datos a la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ]  **' *** inicio de sesión* **'** es el nombre del grupo de Windows, el inicio de sesión de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión que debe asignarse a la nueva base de datos usuario. Los nombres de grupos de Windows e inicios de sesión de Windows deben calificarse con un nombre de dominio de Windows en el formulario *dominio*\\*inicio de sesión *; por ejemplo, **LONDON\Joeb**. El inicio de sesión ya no se puede asignar a un usuario de la base de datos. *inicio de sesión* es un **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@name_in_db=**] **'***name_in_db***'** [ **salida**]  
 Es el nombre del nuevo usuario de la base de datos. *name_in_db* es una variable OUTPUT con un tipo de datos de **sysname**y su valor predeterminado es null. Si no se especifica, *inicio de sesión* se utiliza. Si se especifica como variable OUTPUT con un valor NULL, **@name_in_db** está establecido en *inicio de sesión*. *name_in_db* no debe existir en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Notas  
 **sp_grantdbaccess** llama CREATE USER, que admite opciones adicionales. Para obtener información sobre cómo crear usuarios de base de datos, vea [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md). Para quitar un usuario de base de datos de una base de datos, utilice [DROP USER](../../t-sql/statements/drop-user-transact-sql.md).  
  
 **sp_grantdbaccess** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **db_owner** rol fijo de base de datos o el **db_accessadmin** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `CREATE USER` para agregar un usuario de base de datos para el inicio de sesión de Windows `Edmonds\LolanSo` a la base de datos actual. El nuevo usuario se llama `Lolan`. Es el método preferido para crear un usuario de base de datos.  
  
```  
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
