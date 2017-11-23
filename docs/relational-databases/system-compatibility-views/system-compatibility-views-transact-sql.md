---
title: Vistas de compatibilidad de sistema (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1337914bca53cde4aa374d838b22a08ace940a79
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="system-compatibility-views-transact-sql"></a>Vistas de compatibilidad de sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muchas de las tablas del sistema de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se implementan ahora como un conjunto de vistas. Se conocen como vistas de compatibilidad y solo se proporcionan por compatibilidad con versiones anteriores. Las vistas de compatibilidad exponen los mismos metadatos que estaban disponibles en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. No obstante, las vistas de compatibilidad no exponen ninguno de los metadatos relacionados con las características incluidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Por tanto, cuando utilice estas nuevas características, como [!INCLUDE[ssSB](../../includes/sssb-md.md)] o las particiones, deberá cambiar a la utilización de las vistas de catálogo.  
  
 Otro motivo para actualizar a las vistas de catálogo es que es posible que las columnas de vista de compatibilidad que almacenan los Id. de usuario y de tipo devuelvan valores NULL o activen desbordamientos aritméticos. Esto se debe a que se pueden crear más de 32.767 usuarios, grupos y roles, y 32.767 tipos de datos. Por ejemplo, si fuera a crear 32.768 usuarios y después ejecutara la siguiente consulta: `SELECT * FROM sys.sysusers` Si ARITHABORT está establecido en ON, la consulta provocará un error de desbordamiento aritmético. Si ARITHABORT se establece en OFF, la **uid** columna devuelve NULL.  
  
 Para evitar estos problemas, se recomienda utilizar las nuevas vistas de catálogo, que pueden procesar ese mayor número de identificadores de usuario y de tipo. La tabla siguiente indica las columnas que pueden presentar este desbordamiento.  
  
|Nombre de columna|Vista de compatibilidad|Vista de SQL Server 2005|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**UID**|**sysobjects**|**sys.objects**|  
|**UID**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**otorgante de permisos**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**UID**|**systypes**|**sys.types**|  
|**UID**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**GID**|**sysusers**|**sys.database_principals**|  
|**UID**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**UID**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 Cuando se hace referencia en una base de datos de usuario, tablas del sistema que se han especificado como desusadas en SQL Server 2000 (como **syslanguages** o **syscacheobjects**), ahora se enlazan a la vista de compatibilidad de la parte posterior de la **sys** esquema. Dado que las tablas del sistema de SQL Server 2000 están en desuso en múltiples versiones, no se considera que este cambio sea una novedad.  
  
 Ejemplo: Si un usuario crea una tabla de usuario denominada **syslanguages** en un usuario de base de datos en SQL Server 2008, la instrucción `SELECT * from dbo.syslanguages;` en esa base de datos devuelve los valores de la tabla de usuario. A partir de SQL Server 2012, esta práctica devolverá datos desde la vista del sistema **sys.syslanguages**.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
