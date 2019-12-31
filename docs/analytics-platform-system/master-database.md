---
title: Base de datos maestra
description: Obtenga información sobre la base de datos maestra en almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafef8a5b702b6df4475d34e9395bb12bc9461fb
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400987"
---
# <a name="master-database---parallel-data-warehouse"></a>Base de datos maestra: almacenamiento de datos paralelos
La base de datos maestra de PDW de SQL Server almacena la información de inicio de sesión de nivel de dispositivo y el catálogo de base de datos. Se trata de una SQL Server base de datos maestra que se encuentra en el nodo de control. Como tal, proporciona una funcionalidad similar a PDW de SQL Server que proporciona Master a SQL Server.  
  
Para obtener más información acerca de las bases de datos del sistema, vea bases de datos [del sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
En la lista siguiente se describen las operaciones que no se pueden realizar en la base de datos maestra de PDW de SQL Server.  
  
*No se puede:*  
  
-   Realice una copia de seguridad diferencial de Master.  
  
-   Cree objetos de usuario en Master.  
  
-   Cambiar la intercalación de Master.  
  
-   Cambiar el propietario de Master.  
  
-   Quite o cambie el nombre de la maestra.  
  
-   Modificar permisos en maestra.  
  
-   Ejecute **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Descripción|  
|--------|---------------|  
|Cree una copia de seguridad completa de Master.|Ejemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obtener más información, vea [backup Database](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restauración de la base de datos maestra|Para restaurar la base de datos maestra, use la página [restaurar la base de datos maestra](restore-the-master-database.md) en la herramienta Configuration Manager.|  
|Ver información del catálogo de base de datos.|`SELECT * FROM master.sys.databases;`|  
|Ver información de permisos e inicio de sesión en todo el sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
