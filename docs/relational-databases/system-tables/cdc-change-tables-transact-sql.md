---
title: CDC.change_tables (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs: TSQL
helpviewer_keywords: cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd28fa79040f39fd62c33b15478d18ed34766a8f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cdcchangetables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada tabla de cambios en la base de datos. Se creará una tabla de cambios si la captura de datos modificados está habilitada en una tabla de origen. Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) procedimiento almacenado.  
  |Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de cambios. Es único en una base de datos.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta columna siempre devuelve 0.|  
|**source_object_id**|**int**|Id. de la tabla de origen habilitada para la captura de datos modificados.|  
|**capture_instance**|**sysname**|Nombre de la instancia de captura usada para nombrar los objetos de seguimiento específicos de la instancia. De forma predeterminada, el nombre se deriva del nombre de esquema de origen más el nombre de la tabla de origen en el formato *schemaname_sourcename*.|  
|**start_lsn**|**binary(10)**|Número de secuencia de registro (LSN) que representa el extremo inferior al consultar los datos de cambio en la tabla de cambios.<br /><br /> NULL = no se ha establecido el extremo bajo.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], esta columna siempre devuelve NULL.|  
|**supports_net_changes**|**bit**|La consulta de los cambios de red está habilitada para la tabla de cambios.|  
|**has_drop_pending**|**bit**|El proceso de captura ha recibido la notificación de que se ha quitado la tabla de origen.|  
|**role_name**|**sysname**|Nombre del rol de base de datos usada para obtener acceso a los datos de cambio.<br /><br /> NULL = no se utiliza un rol.|  
|**index_name**|**sysname**|Nombre del índice utilizado para identificar de forma exclusiva las filas en la tabla de origen. **index_name** es el nombre del índice de clave principal de la tabla de origen, o el nombre de un índice único especificado cuando se habilitó la captura de datos modificados en la tabla de origen.<br /><br /> NULL = al habilitar la captura de datos modificados, la tabla de origen no tenía una clave principal y no se ha especificado un índice único.<br /><br /> Nota: Si está habilitada la captura de datos modificados en una tabla donde existe una clave principal, la característica de captura de datos modificados utiliza el índice independientemente de si los cambios netos está habilitado o no. Una vez habilitada la captura de datos modificados, no se permite ninguna modificación en la clave principal. Si no hay ninguna clave principal en la tabla, todavía se puede habilitar la captura de datos modificados, pero solo si los cambios netos se han establecido en "false". Una vez habilitada la captura de datos modificados, puede crear una clave principal. También puede modificar la clave principal porque la captura de datos modificados no utiliza la clave principal.|  
|**filegroup_name**|**sysname**|Nombre del grupo de archivos en que reside la tabla de cambio.<br /><br /> NULL = la tabla de cambio está en el grupo de archivos predeterminado de la base de datos.|  
|**create_date**|**datetime**|Fecha de habilitación de la tabla de origen.|  
|**partition_switch**|**bit**|Indica si la **SWITCH PARTITION** comando de **ALTER TABLE** se puede ejecutar en una tabla que está habilitada para la captura de datos modificados. = 0 true indica que el cambio de particiones está bloqueado. Las tablas sin particiones siempre devuelven 1.|  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
