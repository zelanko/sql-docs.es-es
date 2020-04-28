---
title: Sys. Configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9eb9ced4e010001f42e106ce8b1903e029f2f1c4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68109560"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada valor de opción de configuración de todo el servidor en el sistema.  

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Id. exclusivo del valor de configuración.|  
|**name**|**nvarchar(35)**|Nombre de la opción de configuración.|  
|**value**|**sql_variant**|Valor configurado para esta opción.|  
|**cantidad**|**sql_variant**|Valor mínimo de la opción de configuración.|  
|**máximo**|**sql_variant**|Valor máximo de la opción de configuración.|  
|**value_in_use**|**sql_variant**|Valor actual de esta opción.|  
|**denominación**|**nvarchar(255)**|Descripción de la opción de configuración.|  
|**is_dynamic**|**bit**|1 = La variable que surte surte efecto cuando se ejecuta la instrucción RECONFIGURE.|  
|**is_advanced**|**bit**|1 = la variable solo se muestra cuando se establece **Show advancedoption** .|  
  
 Para obtener una lista de todas las opciones de configuración del servidor, consulte [Opciones de configuración del servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Para las opciones de configuración de nivel de base de datos, vea [ALTER DATABASE scoped configuration &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar la configuración de Soft-NUMA, consulte [&#40;de Soft-numa SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de configuración de todo el servidor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
