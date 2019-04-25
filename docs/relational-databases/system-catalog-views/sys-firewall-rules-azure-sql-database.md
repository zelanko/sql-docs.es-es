---
title: Sys.firewall_rules (base de datos de SQL Azure) | Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5127dacf628231199c5ce5ac49fdb2377c82f270
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631641"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la configuración de firewall de nivel de servidor asociada con su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 La vista `sys.firewall_rules` contiene las columnas siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**INT**|El identificador de la configuración del firewall de nivel de servidor.|  
|NAME|**NVARCHAR(128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de servidor.|  
|start_ip_address|**VARCHAR(45)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR(45)**|La dirección IP más alta en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: Se permiten los intentos de conexión de Windows Azure cuando este campo y el **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**FECHA Y HORA**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de servidor.<br /><br /> Nota: UTC es el acrónimo de hora Universal coordinada.|  
|modify_date|**FECHA Y HORA**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de servidor.|  
  
## <a name="remarks"></a>Comentarios

 Que devuelve información sobre la configuración de firewall de nivel de base de datos asociados con Microsoft Azure SQL Database, use [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permisos

 Acceso de solo lectura a esta vista está disponible para todos los usuarios con permiso para conectarse a la **maestro** base de datos.  
  
## <a name="see-also"></a>Vea también

[sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[Sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurar un Firewall de Windows para acceder al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar un Firewall para el acceso de FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
