---
title: sp_certify_removable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs:
- TSQL
helpviewer_keywords:
- sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: c39665f54a915282a6c59fe7d57b24d0cde0a5e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045927"
---
# <a name="sp_certify_removable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba que una base de datos se ha configurado correctamente para la distribución en medios extraíbles e informa al usuario si surgen problemas.  
  
> **IMPORTANTE:** [! INCLUYA[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) en su lugar.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'`Especifica la base de datos que se va a comprobar. *dbname* es de **tipo sysname**.  
  
`[ @autofix = ] 'auto'`Proporciona a la propiedad de la base de datos y a todos los objetos de base de datos el administrador del sistema, y quita los usuarios de base de datos creados por el usuario y los permisos no predeterminados. *auto* es de tipo **nvarchar (4)** y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Si la base de datos está configurada correctamente, **sp_certify_removable** realiza lo siguiente:  
  
-   Deja la base de datos sin conexión para que se puedan copiar los archivos.  
  
-   Actualiza las estadísticas de todas las tablas e informa de cualquier problema relacionado con los usuarios o la propiedad.  
  
-   Marca los grupos de archivos de datos como de solo lectura para que los archivos puedan copiarse en medios de solo lectura.  
  
 El administrador del sistema debe ser el propietario de la base de datos y de todos sus objetos. El administrador del sistema es un usuario conocido que existe en todos los servidores que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutan y se espera que existan cuando la base de datos se distribuya y se instale posteriormente.  
  
 Si ejecuta **sp_certify_removable** sin el valor **auto** y devuelve información acerca de cualquiera de las siguientes condiciones:  
  
-   El administrador del sistema no es el propietario de la base de datos.  
  
-   Existe algún usuario creado por el usuario.  
  
-   El administrador del sistema no tiene la propiedad de todos los objetos de la base de datos.  
  
-   Se han concedido permisos que no son los predeterminados.  
  
 Estas condiciones pueden corregirse de la forma siguiente:  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas y procedimientos y, a continuación, ejecute de nuevo **sp_certify_removable** .  
  
-   Simplemente ejecute **sp_certify_removable** con el valor **auto** .  
  
 Tenga presente que este procedimiento almacenado solo comprueba los usuarios y sus permisos. Puede agregar grupos a la base de datos y conceder permisos a esos grupos. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución están restringidos a los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes certifican que la base de datos `inventory` se puede quitar.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Desasociar y adjuntar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
