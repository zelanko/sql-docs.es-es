---
title: Sys.firewall_rules (base de datos de SQL Azure) | Documentos de Microsoft
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
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 090ec967e25fff1fac3761298214e0366c0f2478
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de la configuración de firewall de nivel de servidor asociada con su [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 La vista `sys.firewall_rules` contiene las columnas siguientes:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|El identificador de la configuración del firewall de nivel de servidor.|  
|name|**NVARCHAR (128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de servidor.|  
|start_ip_address|**VARCHAR (50)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR (50)**|La dirección IP más alta en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: Los intentos de conexión de Azure de Windows se permiten cuando este campo y el **start_ip_address** campo es igual a `0.0.0.0`.|  
|create_date|**FECHA Y HORA**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de servidor.<br /><br /> Nota: UTC es un acrónimo de hora Universal coordinada.|  
|modify_date|**FECHA Y HORA**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de servidor.|  
  
## <a name="remarks"></a>Comentarios  
 Para quitar una regla de firewall de base de datos, use [sp_delete_firewall_rule &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md). Para configurar una regla de firewall para una sola base de datos, vea [sys.database_firewall_rules &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md). Para obtener información acerca de las reglas de firewall existente, consultas sys.firewall_rules (base de datos de SQL Azure).  
  
## <a name="permissions"></a>Permissions  
 Acceso de solo lectura a esta vista está disponible para todos los usuarios con permiso para conectarse a la **maestro** base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Sys.database_firewall_rules &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_set_firewall_rule &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar un Firewall para el acceso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Configurar los valores de firewall (Base de datos SQL de Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
