---
title: Elementos protegibles | Microsoft Docs
ms.custom: ''
ms.date: 10/14/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7c4a82cfa4d8a82db1e01c49899c3c49c2e01ee9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62745724"
---
# <a name="securables"></a>Elementos protegibles
  Los elementos protegibles son los recursos cuyo acceso es regulado por el sistema de autorización del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por ejemplo, una tabla es un elemento protegible. Algunos elementos protegibles pueden estar incluidos en otros, con lo que se crean jerarquías anidadas denominadas "ámbitos" que a su vez se pueden proteger. Los ámbitos protegibles son **servidor**, **base de datos**y **esquema**.  
  
## <a name="securable-scope-server"></a>Ámbito protegible: servidor  
 El ámbito protegible **servidor** contiene los siguientes valores que puede proteger:  
  
-   grupo de disponibilidad  
  
-   Punto de conexión  
  
-   Inicio de sesión  
  
-   Rol de servidor  
  
-   Base de datos  
  
## <a name="securable-scope-database"></a>Ámbito protegible: base de datos  
 El ámbito protegible **base de datos** contiene los siguientes valores que puede proteger:  
  
-   Rol de aplicación  
  
-   Assembly  
  
-   Clave asimétrica  
  
-   Certificado  
  
-   Contrato  
  
-   Catálogo de texto completo  
  
-   Lista de palabras irrelevantes de texto completo  
  
-   Tipo de mensaje  
  
-   Enlace de servicio remoto  
  
-   (Base de datos) Rol  
  
-   Enrutar  
  
-   Schema  
  
-   Lista de propiedades de búsqueda  
  
-   Servicio  
  
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
  
## <a name="controlling-access-to-a-securable"></a>Controlar el acceso a un elemento protegible  
 La entidad que recibe el permiso para un elemento protegible se denomina "entidad de seguridad". Las entidades de seguridad más comunes son inicios de sesión y usuarios de la base de datos. El acceso a elementos protegibles se controla mediante la concesión o denegación de permisos o añadiendo los inicios de sesión y el usuario a roles con acceso. Para obtener más información sobre cómo controlar los permisos, vea [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql), [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql), [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql), [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) y [sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql).  
  
> [!CAUTION]  
>  Los permisos predeterminados que se conceden a objetos del sistema en el momento de la instalación se evalúan detenidamente frente a posibles amenazas y no necesitan modificarse como parte de la protección de la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Los cambios a los permisos de los objetos del sistema podrían limitar o interrumpir la funcionalidad y dejar potencialmente a su instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en un estado no admitido.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Proteger SQL Server](securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)  
  
  
