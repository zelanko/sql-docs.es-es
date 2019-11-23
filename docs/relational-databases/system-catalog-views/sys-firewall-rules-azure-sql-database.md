---
title: Sys. firewall_rules (Azure SQL Database) | Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 91c3a4101f19afe4a986514fea8dab207c6d9b48
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155549"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la configuración de Firewall de nivel de servidor asociada a la [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 La vista `sys.firewall_rules` contiene las columnas siguientes:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**INT**|El identificador de la configuración del firewall de nivel de servidor.|  
|name|**NVARCHAR (128)**|El nombre que eligió para describir y distinguir la configuración del firewall de nivel de servidor.|  
|start_ip_address|**VARCHAR (45)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|end_ip_address|**VARCHAR (45)**|La dirección IP más alta en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: los intentos de conexión de Azure se permiten cuando este campo y el campo **start_ip_address** es igual a `0.0.0.0`.|  
|create_date|**DATETIME**|Fecha y hora UTC en la que se creó la configuración del firewall de nivel de servidor.<br /><br /> Nota: UTC es un acrónimo de hora universal coordinada.|  
|modify_date|**DATETIME**|Fecha y hora UTC en la que se modificó por última vez la configuración del firewall de nivel de servidor.|  
  
## <a name="remarks"></a>Remarks

 Para devolver información sobre la configuración de Firewall de nivel de base de datos asociada a la Microsoft Azure SQL Database, use [Sys. database_firewall_rules &#40;&#41;Azure SQL Database](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permisos

 El acceso de solo lectura a esta vista está disponible para todos los usuarios con permiso para conectarse a la base de datos **maestra** .  
  
## <a name="see-also"></a>Vea también

[sp_set_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Base de datos SQL de Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[Sys. database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurar un firewall de Windows para el acceso a Motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar un Firewall para el acceso de FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
