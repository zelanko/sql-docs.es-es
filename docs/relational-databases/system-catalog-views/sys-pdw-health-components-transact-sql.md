---
title: Sys. pdw_health_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83bea79a009e25d54f9d0ae589936de7fed7d94a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396049"
---
# <a name="syspdw_health_components-transact-sql"></a>Sys. pdw_health_components (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Almacena información sobre todos los componentes y dispositivos que existen en el sistema. Entre ellos se incluyen el hardware, los dispositivos de almacenamiento y los dispositivos de red.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificador único de un componente o dispositivo.<br /><br /> Clave para esta vista.|NOT NULL|  
|group_id|**Int**|Grupo de componentes lógico al que pertenece este componente. Vea [Sys. pdw_health_components (almacenamiento de datos paralelos)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nombre del componente.|NOT NULL|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
