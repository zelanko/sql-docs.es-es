---
title: Sys.Foreign_Keys (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2051dc726a4622f5340dc0972cf6fc38798d3f9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada objeto que sea una restricción FOREIGN KEY, con **sys.object.type** = f el.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<Las columnas que se heredan de sys.objects >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**referenced_object_id**|**int**|Id. del objeto al que se hace referencia.|  
|**key_index_id**|**int**|Id. del índice de clave dentro del objeto al que se hace referencia.|  
|**is_disabled**|**bit**|La restricción FOREIGN KEY está deshabilitada.|  
|**is_not_for_replication**|**bit**|La restricción FOREIGN KEY se creó con la opción NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|El sistema no ha comprobado la restricción FOREIGN KEY.|  
|**delete_referential_action**|**tinyint**|Acción referencial que se declaró para FOREIGN KEY cuando se produce una eliminación.<br /><br /> 0 = Sin acción<br /><br /> 1 = Cascada<br /><br /> 2 = Establecer como NULL<br /><br /> 3 = Establecer valor predeterminado|  
|**delete_referential_action_desc**|**nvarchar (60)**|Descripción de la acción referencial que se declaró para FOREIGN KEY cuando se produce una eliminación:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|Acción referencial que se declaró para FOREIGN KEY cuando se produce una actualización.<br /><br /> 0 = Sin acción<br /><br /> 1 = Cascada<br /><br /> 2 = Establecer como NULL<br /><br /> 3 = Establecer valor predeterminado|  
|**update_referential_action_desc**|**nvarchar (60)**|Descripción de la acción referencial que se declaró para FOREIGN KEY cuando se produce una actualización:<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = El sistema generó el nombre.<br /><br /> 0 = El usuario proporcionó el nombre.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
