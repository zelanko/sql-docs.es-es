---
title: Permisos de objeto de sistema GRANT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 68fc428edb12c5b62d5e6eadb6d92bc090e66fde
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="grant-system-object-permissions-transact-sql"></a>GRANT (permisos de objeto de sistema de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permisos para objetos de sistema, como procedimientos almacenados del sistema, procedimientos almacenados extendidos, funciones y vistas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>Argumentos  
 [sys]. .  
 Solo se requiere el calificador sys para hacer referencia a vistas de catálogo y vistas de administración dinámica.  
  
 *system_object*  
 Especifica el objeto en el que se va a conceder el permiso.  
  
 *entidad de seguridad*  
 Especifica la entidad de seguridad para la que se concede el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar esta instrucción para conceder permisos para determinados procedimientos almacenados, procedimientos almacenados extendidos, funciones con valores de tabla, funciones escalares, vistas, vistas de catálogo, vistas de compatibilidad, vistas INFORMATION_SCHEMA, vistas de administración dinámica y tablas del sistema instalados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada objeto del sistema existe como registro único en la base de datos de recursos del servidor (mssqlsystemresource). La base de datos de recursos es de solo lectura. Se muestra un vínculo al objeto como registro en el esquema sys de todas las bases de datos. Es posible conceder, denegar y revocar el permiso para ejecutar o seleccionar un objeto del sistema.  
  
 Para conceder un permiso para ejecutar o seleccionar un objeto no es necesario cumplir todos los permisos requeridos para utilizar el objeto. La mayoría de los objetos realiza operaciones para las que se necesitan permisos adicionales. Por ejemplo, un usuario para el que se concede el permiso EXECUTE para sp_addlinkedserver no puede crear un servidor vinculado a menos que el usuario sea también miembro del rol fijo de servidor sysadmin.  
  
 La resolución predeterminada de nombres resuelve los nombres no calificados de procedimiento para la base de datos de recursos. Por tanto, solo se requiere el calificador sys para especificar vistas de catálogo y vistas de administración dinámica.  
  
 No se admite la concesión de permisos en desencadenadores y columnas de objetos del sistema.  
  
 Los permisos de objetos del sistema se mantendrán durante las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede ver los objetos del sistema en la vista de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) . Los permisos en objetos del sistema están visibles en el [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) vista en la base de datos maestra de catálogo.  
  
 La siguiente consulta muestra información acerca de los permisos de objetos del sistema:  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-granting-select-permission-on-a-view"></a>A. Conceder el permiso SELECT para una vista  
 El siguiente ejemplo se concede el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión `Sylvester1` permiso para seleccionar una vista que muestra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión. A continuación, el ejemplo concede el permiso adicional necesario para ver los metadatos para los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no son propiedad del usuario.  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. Conceder el permiso EXECUTE para un procedimiento almacenado extendido  
 En el siguiente ejemplo se concede el permiso `EXECUTE` para `xp_readmail` a `Sylvester1`.  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.system_objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [Sys.database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [REVOCAR permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [DENEGAR permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
