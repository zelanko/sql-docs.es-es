---
description: sys.firewall_rules (Azure SQL Database)
title: sys.firewall_rules (Azure SQL Database) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current
ms.openlocfilehash: b7e08498a9f3867c03c2198957af0ac35f9a0a01
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477436"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Devuelve información sobre la configuración de Firewall de nivel de servidor asociada a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .  
  
 La vista `sys.firewall_rules` contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**INT**|El identificador de la configuración del firewall de nivel de servidor.|  
|name|**NVARCHAR (128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de servidor.|  
|start_ip_address|**VARCHAR (45)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR (45)**|La dirección IP más alta en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: los intentos de conexión de Azure se permiten cuando este campo y el campo **start_ip_address** es igual a `0.0.0.0` .|  
|create_date|**DATETIME**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de servidor.<br /><br /> Nota: UTC es un acrónimo de hora universal coordinada.|  
|modify_date|**DATETIME**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de servidor.|  
  
## <a name="remarks"></a>Comentarios

 Para devolver información acerca de la configuración de Firewall de nivel de base de datos asociada a la Microsoft Azure SQL Database, use [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permisos

 El acceso de solo lectura a esta vista está disponible para todos los usuarios con permiso para conectarse a la base de datos **maestra** .  
  
## <a name="see-also"></a>Consulte también

[sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurar un firewall de Windows para el acceso a Motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar un Firewall para el acceso de FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar un firewall para el acceso del Servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
