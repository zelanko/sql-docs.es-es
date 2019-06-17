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
manager: craigg
ms.openlocfilehash: 97964286b3281eee4e5b6850065c85034628bfdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62994402"
---
# <a name="spcertifyremovable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba que una base de datos se ha configurado correctamente para la distribución en medios extraíbles e informa al usuario si surgen problemas.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) instead.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` Especifica la base de datos que debe comprobarse. *dbname* es **sysname**.  
  
`[ @autofix = ] 'auto'` Asigna la propiedad de la base de datos y todos los objetos de base de datos para el administrador del sistema y quita los usuarios de base de datos creada por el usuario y permisos no predeterminados. *Auto* es **nvarchar (4)** , su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Si la base de datos está configurado correctamente, **sp_certify_removable** realiza lo siguiente:  
  
-   Deja la base de datos sin conexión para que se puedan copiar los archivos.  
  
-   Actualiza las estadísticas de todas las tablas e informa de cualquier problema relacionado con los usuarios o la propiedad.  
  
-   Marca los grupos de archivos de datos como de solo lectura para que los archivos puedan copiarse en medios de solo lectura.  
  
 El administrador del sistema debe ser el propietario de la base de datos y de todos sus objetos. El administrador del sistema es un usuario conocido que existe en todos los servidores que ejecutan [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y puede esperarse que exista cuando la base de datos se distribuye y se instala más adelante.  
  
 Si ejecuta **sp_certify_removable** sin el **automática** valor y devuelve información acerca de cualquiera de las condiciones siguientes:  
  
-   El administrador del sistema no es el propietario de la base de datos.  
  
-   Existe algún usuario creado por el usuario.  
  
-   El administrador del sistema no tiene la propiedad de todos los objetos de la base de datos.  
  
-   Se han concedido permisos que no son los predeterminados.  
  
 Estas condiciones pueden corregirse de la forma siguiente:  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas y procedimientos y, luego, ejecute **sp_certify_removable** nuevo.  
  
-   Simplemente ejecute **sp_certify_removable** con el **automática** valor.  
  
 Tenga presente que este procedimiento almacenado solo comprueba los usuarios y sus permisos. Puede agregar grupos a la base de datos y conceder permisos a esos grupos. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Ejecutar permisos están restringidos a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes certifican que la base de datos `inventory` se puede quitar.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>Vea también  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_create_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
