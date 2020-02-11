---
title: Sys. pdw_health_component_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79d459fdff2e26726168f5200b53c82f3bb6a79c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127505"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>Sys. pdw_health_component_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena información sobre las agrupaciones lógicas de componentes y dispositivos.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|Identificador único para componentes y dispositivos.<br /><br /> Clave para esta vista.|NOT NULL|  
|group_name|**nvarchar(255)**|Nombre del grupo lógico para los componentes y dispositivos.|NOT NULL|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Data Warehouse y vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
