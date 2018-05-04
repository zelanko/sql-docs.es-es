---
title: Sys.database_usage (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7754ed63cc6325b9b6cf1650e7b71daad03393ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: Esto se aplica solo a V11 de base de datos de SQL Azure.**  
  
 Muestra el número, el tipo y la duración de las bases de datos en el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server.  
  
 El **sys.database_usage** vista contiene las columnas siguientes.  
  
|Nombre de la columna|Description|  
|-----------------|-----------------|  
|time|Fecha en que se produjeron los eventos de uso.|  
|sku|El tipo de nivel de servicio de la base de datos: **Web**, **Business**, **básica**, **estándar**, **Premium**|  
|quantity|El número máximo de bases de datos de un tipo SKU que existía durante ese día.|  
  
## <a name="permissions"></a>Permissions  
 Acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la **maestro** base de datos.  
  
## <a name="remarks"></a>Comentarios  
 El **sys.database_usage** vista devuelve una fila para cada día de la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de precios de base de datos SQL](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en base de datos SQL Azure de Windows](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
