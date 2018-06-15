---
title: sp_detach_db (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
caps.latest.revision: 86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0f17581782cea310bcfad9ec6d7ce4823d1d38c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260771"
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Separa una base de datos que actualmente no se está utilizando de una instancia del servidor y, opcionalmente, ejecuta UPDATE STATISTICS en todas las tablas antes de la separación.  
  
> [!IMPORTANT]  
>  Para separar una base de datos replicada, se debe anular su publicación. Para obtener más información, vea la sección “Comentarios” más adelante en este tema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname =** ] **'***database_name***'**  
 Es el nombre de la base de datos que se va a separar. *database_name* es un **sysname** valor, su valor predeterminado es null.  
  
 [  **@skipchecks =** ] **'***skipchecks***'**  
 Especifica si se debe omitir o ejecutar UPDATE STATISTIC. *valor de skipchecks* es un **nvarchar (10)** valor, su valor predeterminado es null. Para omitir UPDATE STATISTICS, especifique **true**. Para ejecutar explícitamente UPDATE STATISTICS, especifique **false**.  
  
 De forma predeterminada, UPDATE STATISTICS se ejecuta para actualizar información acerca de los datos de las tablas e índices. Ejecutar UPATE STATISTICS es útil para las bases de datos que se trasladan a medios de solo lectura.  
  
 [  **@keepfulltextindexfile=** ] **'***KeepFulltextIndexFile***'**  
 Especifica que el archivo de índice de texto completo asociado a la base de datos que se va a separar no se quitará durante la operación de separación de la base de datos. *KeepFulltextIndexFile* es un **nvarchar (10)** y su valor predeterminado de **true**. Si *KeepFulltextIndexFile* es **false**, todos los archivos de índice de texto completo asociado a la base de datos y se quitan los metadatos del índice de texto completo, a menos que la base de datos es de solo lectura. Si es NULL o **true**, relacionada con el texto completo se mantienen metadatos.  
  
> [!IMPORTANT]  
>  El**@keepfulltextindexfile** parámetro se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No use este parámetro en nuevos trabajos de desarrollo, y modifique lo antes posible las aplicaciones que lo usen actualmente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Cuando se desasocia una base de datos, todos sus metadatos se eliminan. Si la base de datos es la base de datos predeterminada de las cuentas de inicio de sesión, **maestro** se convierte en su base de datos predeterminada.  
  
> [!NOTE]  
>  Para obtener información sobre cómo ver la base de datos predeterminada de todas las cuentas de inicio de sesión, vea [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md). Si tiene los permisos necesarios, puede usar [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para asignar una nueva base de datos predeterminada para un inicio de sesión.  
  
## <a name="restrictions"></a>Restricciones  
 No se puede separar una base de datos si se da alguna de estas circunstancias:  
  
-   Se está utilizando la base de datos actualmente. Para obtener más información, vea "Obtener acceso exclusivo" más adelante en este tema.  
  
-   Si está replicada, la base de datos está publicada.  
  
     Para poder separar la base de datos, debe deshabilitar la publicación ejecutando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    >  Si no puede usar **sp_replicationdboption**, puede quitar la replicación ejecutando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Existe una instantánea de base de datos en la base de datos.  
  
     Para poder separar la base de datos, debe quitar todas sus instantáneas. Para obtener más información, vea [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  No puede separar ni adjuntar una instantánea de base de datos.  
  
-   Se está creando un reflejo de la base de datos.  
  
     La base de datos no se puede separar hasta que finalice la sesión de creación de reflejo de la base de datos. Para obtener más información, vea [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   La base de datos es sospechosa.  
  
     Las bases de datos sospechosas se deben poner en el modo de emergencia para poder desasociar la base de datos. Para obtener más información sobre cómo poner una base de datos en modo de emergencia, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   La base de datos es una base de datos del sistema.  
  
## <a name="obtaining-exclusive-access"></a>Obtener acceso exclusivo  
 Separar una base de datos requiere acceso exclusivo a la misma. Si la base de datos que desea separar está en uso, para poder separarla debe establecer la base de datos en modo SINGLE_USER para obtener acceso exclusivo.  
  
 Por ejemplo, la siguiente `ALTER DATABASE` instrucción obtiene acceso exclusivo a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] después de desconectan de todos los usuarios actuales de la base de datos de la base de datos.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  Para forzar la actual usuarios fuera de la base de datos inmediatamente o tras un número especificado de segundos, también debe utilizar la opción ROLLBACK: ALTER DATABASE *database_name* SET SINGLE_USER WITH ROLLBACK *rollback_option*. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="reattaching-a-database"></a>Volver a adjuntar una base de datos  
 Los archivos separados permanecen y se pueden volver a adjuntar utilizando CREATE DATABASE (con la opción FOR ATTACH o FOR ATTACH_REBUILD_LOG). Los archivos se pueden mover a otro servidor y adjuntarse allí.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** rol fijo de servidor o pertenecer el **db_owner** rol de la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se separa la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] con la base de datos *skipchecks* establecido en true.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 En el ejemplo siguiente se separa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y se conservan los archivos y los metadatos del índice de texto completo. Este comando ejecuta UPDATE STATISTICS, que es el comportamiento predeterminado.  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
  
