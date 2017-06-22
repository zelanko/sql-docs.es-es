---
title: Elementos protegibles | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 10/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 51db5d7a36569601e7d21d5fc50d16230b85ea5d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="securables"></a>Elementos protegibles
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Los elementos protegibles son los recursos cuyo acceso es regulado por el sistema de autorización del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por ejemplo, una tabla es un elemento protegible. Algunos elementos protegibles pueden estar incluidos en otros, con lo que se crean jerarquías anidadas denominadas "ámbitos" que a su vez se pueden proteger. Los ámbitos protegibles son **servidor**, **base de datos**y **esquema**.  
  
## <a name="securable-scope-server"></a>Ámbito protegible: servidor  
 El ámbito protegible **servidor** contiene los siguientes valores que puede proteger:  
  
-   Grupo de disponibilidad  
  
-   Extremo  
  
-   Inicio de sesión  
  
-   Rol de servidor  
  
-   base de datos  
  
## <a name="securable-scope-database"></a>Ámbito protegible: base de datos  
 El ámbito protegible **base de datos** contiene los siguientes valores que puede proteger:  
  
-   Rol de aplicación  
  
-   Ensamblado  
  
-   Clave asimétrica  
  
-   Certificado  
  
-   Contrato  
  
-   Catálogo de texto completo  
  
-   Lista de palabras irrelevantes de texto completo  
  
-   Tipo de mensaje  
  
-   Enlace de servicio remoto  
  
-   (Base de datos) Rol  
  
-   Ruta  
  
-   esquema  
  
-   Lista de propiedades de búsqueda  
  
-   ssNoVersion  
  
-   Clave simétrica  
  
-   Usuario  
  
## <a name="securable-scope-schema"></a>Ámbito protegible: esquema  
 El ámbito protegible **esquema** contiene los siguientes valores que se pueden proteger:  
  
-   Tipo  
  
-   Colección de esquemas XML  
  
-   Objeto: la clase de objeto tiene los miembros siguientes:  
  
    -   Agregado  
  
    -   Función  
  
    -   Procedimiento  
  
    -   Cola  
  
    -   Synonym (Sinónimo)  
  
    -   Tabla  
  
    -   Ver 
    
    -   Tabla externa 
  
## <a name="controlling-access-to-a-securable"></a>Controlar el acceso a un elemento protegible  
 La entidad que recibe el permiso para un elemento protegible se denomina "entidad de seguridad". Las entidades de seguridad más comunes son inicios de sesión y usuarios de la base de datos. El acceso a elementos protegibles se controla mediante la concesión o denegación de permisos o con la incorporación de inicios de sesión y usuarios a roles con acceso. Para obtener más información sobre cómo controlar los permisos, vea [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md), [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md), [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md), [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) y [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
> [!CAUTION]  
>  Los permisos predeterminados que se conceden a objetos del sistema en el momento de la instalación se evalúan detenidamente frente a posibles amenazas y no necesitan modificarse como parte de la protección de la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los cambios a los permisos de los objetos del sistema podrían limitar o interrumpir la funcionalidad y dejar potencialmente a su instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un estado no admitido.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
 [Proteger SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)  
  
  

