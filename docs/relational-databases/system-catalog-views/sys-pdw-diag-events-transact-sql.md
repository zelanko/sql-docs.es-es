---
description: Sys. pdw_diag_events (Transact-SQL)
title: Sys. pdw_diag_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 59bb3e9c-2829-49a0-b382-652ed1f54f88
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c38eb1e89f3e06bee1f3ec2841efc72845a96386
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490294"
---
# <a name="syspdw_diag_events-transact-sql"></a>Sys. pdw_diag_events (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene información sobre los eventos que se pueden incluir en las sesiones de diagnóstico del sistema.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|Nombre del evento de diagnóstico específico.||  
|**source**|**nvarchar(255)**|Origen del evento (motor, general, DMS, etc.)||  
|**is_enabled**|**bit**|Indica si el evento se está publicando.||  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
