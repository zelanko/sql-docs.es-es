---
description: log_shipping_primary_secondaries (Transact-SQL)
title: log_shipping_primary_secondaries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_secondaries_TSQL
- log_shipping_primary_secondaries
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_secondaries system table
ms.assetid: 4b315c70-7265-4acd-b35b-a4dbb7881d98
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6749e16a5678b580d3d78036c551f3c3295a0a48
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545751"
---
# <a name="log_shipping_primary_secondaries-transact-sql"></a>log_shipping_primary_secondaries (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Asigna cada base de datos principal a sus bases de datos secundarias. Esta tabla se almacena en la base de datos **msdb** .  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|Id. de la base de datos principal para la configuración del trasvase de registros.|  
|**secondary_server**|**sysname**|Nombre de la instancia secundaria de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración del trasvase de registros.|  
|**secondary_database**|**sysname**|Nombre de la base de datos secundaria en la configuración del trasvase de registros.|  
  
## <a name="see-also"></a>Consulte también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_secondary &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md)   
 [sp_delete_log_shipping_primary_secondary &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md)   
 [sp_help_log_shipping_primary_secondary &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
