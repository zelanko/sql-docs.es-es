---
title: sys.pdw_health_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 69e5d36db3d5ed69b0a0ecc062a0692955b84398
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011557"
---
# <a name="syspdwhealthcomponents-transact-sql"></a>sys.pdw_health_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena información sobre todos los componentes y dispositivos que existen en el sistema. Estos incluyen el hardware, dispositivos de almacenamiento y dispositivos de red.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificador único de un componente o el dispositivo.<br /><br /> Clave para esta vista.|NOT NULL|  
|group_id|**Int**|El grupo de componentes lógicos a la que pertenece este componente. Consulte [sys.pdw_health_components (almacenamiento de datos paralelos)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nombre del componente.|NOT NULL|  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
