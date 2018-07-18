---
title: Sys.database_usage (base de datos de SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
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
ms.openlocfilehash: affdc08bb7ae507ca30edfa986cd68a81ba564f2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038823"
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
  
## <a name="remarks"></a>Notas  
 El **sys.database_usage** vista devuelve una fila por cada día de la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de precios de SQL Database](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Cuentas y facturación en Microsoft Azure SQL Database](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
