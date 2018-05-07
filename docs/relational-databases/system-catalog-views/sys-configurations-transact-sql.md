---
title: Sys.Configurations (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 25de8a6eb70c79551caca8188c4f67a786e62172
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada valor de opción de configuración de todo el servidor en el sistema.  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Id. exclusivo del valor de configuración.|  
|**Nombre**|**nvarchar(35)**|Nombre de la opción de configuración.|  
|**value**|**sql_variant**|Valor configurado para esta opción.|  
|**Mínimo**|**sql_variant**|Valor mínimo para la opción de configuración.|  
|**Máximo**|**sql_variant**|Valor máximo para la opción de configuración.|  
|**value_in_use**|**sql_variant**|Valor actual de esta opción.|  
|**Descripción**|**nvarchar(255)**|Descripción de la opción de configuración.|  
|**is_dynamic**|**bit**|1 = La variable que surte surte efecto cuando se ejecuta la instrucción RECONFIGURE.|  
|**is_advanced**|**bit**|1 = la variable se muestra solo cuando la **mostrar advancedoption** se establece.|  
  
 Para obtener una lista de todas las opciones de configuración de servidor, consulte [opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Para opciones de configuración de nivel de base de datos, vea [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar NUMA de software, consulte [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de la configuración del servidor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
