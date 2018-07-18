---
title: Sys.database_firewall_rules (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea5b9d5cb50740e349aa6d3cf58bd20f620a8ab6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038333"
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la configuración de firewall de nivel de base de datos asociada con su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La configuración de firewall de nivel de base de datos es especialmente útil cuando se usan usuarios de base de datos independientes. Para obtener más información, vea [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 La vista `sys.database_firewall_rules` contiene las columnas siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|El identificador de la configuración del firewall de nivel de base de datos.|  
|NAME|**NVARCHAR (128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de base de datos.|  
|start_ip_address|**VARCHAR (50)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de base de datos. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR (50)**|La dirección IP más alta en el intervalo de la configuración del firewall. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: Windows Azure de intentos de conexión se permiten cuando este campo y el **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**FECHA Y HORA**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de base de datos.|  
|modify_date|**FECHA Y HORA**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de base de datos.|  
  
## <a name="remarks"></a>Notas  
 Para quitar una regla de firewall de base de datos, use [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). Para establecer una regla de firewall para todos [!INCLUDE[ssSDS](../../includes/sssds-md.md)], consulte [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). Para devolver información acerca de la base de datos existente en las reglas de firewall, consulte [sys.database_firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permisos  
 Esta vista está disponible en el **maestro** base de datos y en cada base de datos de usuario. El acceso de solo lectura a esta vista está disponible para todos los usuarios que dispongan de permiso para conectarse a la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys.database_firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Configurar un Firewall de Windows para acceder al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar un Firewall para el acceso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
