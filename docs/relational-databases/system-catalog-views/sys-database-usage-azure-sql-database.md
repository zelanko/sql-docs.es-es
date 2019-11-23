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
ms.openlocfilehash: 0a0789ebd9a5aa4bd10605d69afa59a586ce75b2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155543"
---
# <a name="sysdatabase_usage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: esto solo se aplica a Azure SQL Database v11.**  
  
 Muestra el número, el tipo y la duración de las bases de datos en el servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 La vista **Sys. database_usage** contiene las columnas siguientes.  
  
|Column Name|Descripción|  
|-----------------|-----------------|  
|time|Fecha en que se produjeron los eventos de uso.|  
|sku|El tipo de nivel de servicio para la base de datos: **Web**, **Business**, **Basic**, **Standard**, **Premium**|  
|quantity|El número máximo de bases de datos de un tipo SKU que existía durante ese día.|  
  
## <a name="permissions"></a>Permisos  
 El acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la base de datos **maestra** .  
  
## <a name="remarks"></a>Remarks  
 La vista **Sys. database_usage** devuelve una fila por cada día de la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [SQL Database detalles de precios](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
