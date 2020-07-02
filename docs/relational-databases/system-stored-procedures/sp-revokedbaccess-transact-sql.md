---
title: sp_revokedbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 41d2c1aa64bc3d7913cadbb5e54e9895af55e554
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750483"
---
# <a name="sp_revokedbaccess-transact-sql"></a>sp_revokedbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Quita un usuario de base de datos de la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilice [Drop User](../../t-sql/statements/drop-user-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name_in_db = ] 'name'`Es el nombre del usuario de la base de datos que se va a quitar. *Name* es un **tipo sysname** sin ningún valor predeterminado. *nombre* puede ser el nombre de un inicio de sesión de servidor, un inicio de sesión de Windows o un grupo de Windows y debe existir en la base de datos actual. Si especifica un inicio de sesión de Windows o un grupo de Windows, debe especificar el nombre con el que se conoce en la base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Al quitar el usuario de base de datos, también se quitan los permisos y alias que dependen del usuario.  
  
 **sp_revokedbaccess** solo puede quitar usuarios de la base de datos actual. Antes de quitar un usuario de base de datos propietario de objetos en la base de datos actual, debe transferir la propiedad de los objetos o quitarlos de la base de datos. Para obtener más información, vea [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 **sp_revokedbaccess** no se puede ejecutar en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY USER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita el usuario de base de datos asignado a `Edmonds\LolanSo` de la base de datos actual.  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
