---
title: REVOCAR permisos de objeto de sistema (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 461cde90e42168333f5c2cd700c25cc1a396fabe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-system-object-permissions-transact-sql"></a>REVOKE (permisos de objeto de sistema de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca permisos en objetos de sistema como procedimientos almacenados, procedimientos almacenados extendidos, funciones y vistas de una entidad de seguridad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
## <a name="arguments"></a>Argumentos  
 [**sys.** ] .  
 El **sys** calificador sólo es necesario cuando se hace referencia a vistas de catálogo y vistas de administración dinámica.  
  
 *system_object*  
 Especifica el objeto en el que se va a revocar el permiso.  
  
 *entidad de seguridad*  
 Especifica la entidad de seguridad desde la que se revoca el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar esta instrucción para revocar permisos para determinados procedimientos almacenados, procedimientos almacenados extendidos, funciones con valores de tabla, funciones escalares, vistas, vistas de catálogo, vistas de compatibilidad, vistas INFORMATION_SCHEMA, vistas de administración dinámica y tablas del sistema instalados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada uno de estos objetos del sistema existe como registro único en la base de datos de recursos (**mssqlsystemresource**). La base de datos de recursos es de solo lectura. Se muestra un vínculo al objeto como un registro en el **sys** esquema de cada base de datos.  
  
 La resolución predeterminada de nombres resuelve los nombres no calificados de procedimiento para la base de datos de recursos. Por lo tanto, la **sys.** se requiere el calificador solo cuando se especifica vistas de catálogo y vistas de administración dinámica.  
  
> [!CAUTION]  
>  Si revoca permisos en objetos del sistema, se producirán errores en las aplicaciones que dependen de ellos. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utiliza vistas de catálogo y podría no funcionar correctamente si cambia los permisos predeterminados en las vistas de catálogo.  
  
 No se admite la revocación de permisos en desencadenadores y columnas de objetos del sistema.  
  
 Los permisos de objetos del sistema se mantendrán durante las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede ver los objetos del sistema en la vista de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) .  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se revoca el permiso `EXECUTE` para `sp_addlinkedserver` a `public`.  
  
```  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.system_objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [Sys.database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CONCEDER permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [DENEGAR permisos de objeto de sistema &#40; Transact-SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
