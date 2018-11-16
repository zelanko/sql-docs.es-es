---
title: Sys.database_usage (base de datos de SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f17e34de7c230b111652ea57a3baa072a442a6a5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656744"
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Nota: Esto se aplica solo a Azure SQL Database V11.**  
  
 Muestra el número, tipo y la duración de las bases de datos en el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server.  
  
 El **sys.database_usage** vista contiene las siguientes columnas.  
  
|Nombre de la columna|Descripción|  
|-----------------|-----------------|  
|time|Fecha en que se produjeron los eventos de uso.|  
|sku|El tipo de nivel de servicio para la base de datos: **Web**, **Business**, **básica**, **estándar**, **Premium**|  
|quantity|El número máximo de bases de datos de un tipo SKU que existía durante ese día.|  
  
## <a name="permissions"></a>Permisos  
 Acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la **maestro** base de datos.  
  
## <a name="remarks"></a>Comentarios  
 El **sys.database_usage** vista devuelve una fila por cada día de la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de precios de SQL Database](https://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en Microsoft Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
