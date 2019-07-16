---
title: Sys.database_firewall_rules (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1681c3b245da5d1abded678d54b2b7694598077b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915024"
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la configuración de firewall de nivel de base de datos asociada con su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. La configuración de firewall de nivel de base de datos es especialmente útil cuando se usan usuarios de base de datos independientes. Para obtener más información, vea [Usuarios de base de datos independiente - Conversión de la base de datos en portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 La vista `sys.database_firewall_rules` contiene las columnas siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|El identificador de la configuración del firewall de nivel de base de datos.|  
|name|**NVARCHAR (128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de base de datos.|  
|start_ip_address|**VARCHAR(45)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de base de datos. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR(45)**|La dirección IP más alta en el intervalo de la configuración del firewall. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: Se permiten los intentos de conexión de Windows Azure cuando este campo y el **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**FECHA Y HORA**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de base de datos.|  
|modify_date|**FECHA Y HORA**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de base de datos.|  
  
## <a name="remarks"></a>Comentarios  
 Para devolver información sobre la configuración de firewall de nivel de servidor asociado con Microsoft Azure SQL Database, use [sys.firewall_rules (base de datos de SQL Azure)](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permisos  
 Esta vista está disponible en el **maestro** base de datos y en cada base de datos de usuario. El acceso de solo lectura a esta vista está disponible para todos los usuarios que dispongan de permiso para conectarse a la base de datos.  
  
## <a name="see-also"></a>Vea también
[sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[Sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
[Configurar un Firewall de Windows para acceder al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar un Firewall para el acceso de FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar un firewall para el acceso del Servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
