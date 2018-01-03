---
title: base de datos maestra (PDW de SQL Server)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c71617c0-6689-4f52-81c6-58f4cf7c7377
caps.latest.revision: "8"
ms.workload: not set
ms.openlocfilehash: 1fde1a329703ed833a9fdeb6686b1a63c04aea79
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="master-database"></a>Base de datos maestra
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
  
## <a name="related-tasks"></a>Related Tasks  
  
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
  
