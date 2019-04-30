---
title: Base de datos master - almacenamiento de datos paralelos | Microsoft Docs
description: Obtenga información sobre la base de datos maestra en el almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213298"
---
# <a name="master-database---parallel-data-warehouse"></a>Base de datos master - almacenamiento de datos paralelos
La base de datos master PDW de SQL Server almacena información de inicio de sesión de nivel de dispositivo y el catálogo de base de datos. Es una base de datos maestra de SQL Server reside en el nodo de Control. Por lo tanto, proporciona una funcionalidad similar a SQL Server PDW como maestros proporciona a SQL Server.  
  
Para obtener más información acerca de las bases de datos del sistema, consulte [las bases de datos del sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
La lista siguiente describe las operaciones que no se puede realizar en la base de datos maestra de SQL Server PDW.  
  
Le *no se puede:*  
  
-   Realizar una copia de seguridad diferencial de patrón.  
  
-   Crear objetos de usuario en la rama maestra.  
  
-   Cambiar la intercalación de patrón.  
  
-   Cambiar el propietario del maestro.  
  
-   Quite o cambie el nombre de patrón.  
  
-   Modificar los permisos de master.  
  
-   Ejecutar **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Descripción|  
|--------|---------------|  
|Crear una copia de seguridad completa de patrón.|Ejemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obtener más información, consulte [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restauración de la base de datos maestra|Para restaurar la base de datos maestra, use el [restaurar la base de datos Master](restore-the-master-database.md) página en la herramienta Administrador de configuración.|  
|Ver información del catálogo de base de datos.|`SELECT * FROM master.sys.databases;`|  
|Ver información de inicio de sesión y el permiso de todo el sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
