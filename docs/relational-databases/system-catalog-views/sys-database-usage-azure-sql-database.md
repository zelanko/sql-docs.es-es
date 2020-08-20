---
description: sys.database_usage (Azure SQL Database)
title: Sys. database_usage (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c72973c21b2e660667b2bed31d771f3ce19c43b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455274"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  **Nota: esto solo se aplica a Azure SQL Database v11.**  
  
 Muestra el número, el tipo y la duración de las bases de datos en el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor.  
  
 La vista **Sys. database_usage** contiene las columnas siguientes.  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|time|Fecha en que se produjeron los eventos de uso.|  
|sku|El tipo de nivel de servicio para la base de datos: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantity|El número máximo de bases de datos de un tipo SKU que existía durante ese día.|  
  
## <a name="permissions"></a>Permisos  
 El acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la base de datos **maestra** .  
  
## <a name="remarks"></a>Observaciones  
 La vista **Sys. database_usage** devuelve una fila por cada día de la suscripción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de precios de SQL Database](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en Base de datos SQL de Azure](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
