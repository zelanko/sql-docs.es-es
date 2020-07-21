---
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
ms.openlocfilehash: 4b68fbc20fb220af49036890edc2b67d1a4f7b65
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724680"
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
  
## <a name="remarks"></a>Comentarios  
 La vista **Sys. database_usage** devuelve una fila por cada día de la suscripción.  
  
## <a name="see-also"></a>Consulte también  
 [Detalles de precios de SQL Database](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en Base de datos SQL de Azure](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
