---
title: 'Base de datos maestra: almacenamiento de datos paralelos | Documentos de Microsoft'
description: Obtenga información acerca de la base de datos maestra en almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="master-database---parallel-data-warehouse"></a>Base de datos maestra: almacenamiento de datos paralelos
La base de datos maestra de SQL Server PDW almacena información de inicio de sesión de nivel de dispositivo y el catálogo de base de datos. Es una base de datos maestra de SQL Server reside en el nodo de Control. Por lo tanto, proporciona una funcionalidad similar a SQL Server PDW como maestro se proporciona con SQL Server.  
  
Para obtener más información acerca de las bases de datos del sistema, consulte [bases de datos de sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
En la lista siguiente describe las operaciones que no se puede realizar en la base de datos maestra de SQL Server PDW.  
  
Se *no se puede:*  
  
-   Realizar una copia de seguridad diferencial de master.  
  
-   Crear objetos de usuario en master.  
  
-   Cambiar la intercalación de master.  
  
-   Cambiar el propietario del maestro.  
  
-   Quitar o cambiar el nombre de patrón.  
  
-   Modificar los permisos al maestro.  
  
-   Ejecutar **SHRINKLOG DBCC**.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Tarea|Description|  
|--------|---------------|  
|Crear una copia de seguridad de master.|Ejemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obtener más información, consulte [base de datos de copia de seguridad](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restaurar la base de datos maestra|Para restaurar la base de datos maestra, use la [restaurar la base de datos Master](restore-the-master-database.md) página en la herramienta Administrador de configuración.|  
|Ver información de catálogo de base de datos.|`SELECT * FROM master.sys.databases;`|  
|Ver la información de inicio de sesión y permisos de todo el sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
