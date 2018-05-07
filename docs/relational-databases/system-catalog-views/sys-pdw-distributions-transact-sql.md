---
title: Sys.pdw_distributions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0bfc4540ddf3f7778e41043c727d96a7b2074113
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwdistributions-transact-sql"></a>Sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre las distribuciones en el dispositivo. Muestra una fila por cada distribución de dispositivo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Identificador numérico único asociado con la distribución.<br /><br /> Clave para esta vista.|1 hasta el número de nodos de proceso de dispositivo multiplicado por el número de distribuciones por nodo de proceso.|  
|pdw_node_id|**int**|Identificador del nodo que se encuentra en esta distribución.|Vea pdw_node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|name|**nvarchar(32)**|Identificador asociado con la distribución, que se utiliza como un sufijo en tablas distribuidas de cadena.|Cadena compuesta de "A-z", "a-z", "0-9', '_','-'.|  
|position|**int**|Posición de la distribución dentro de un nodo correspondiente a otras distribuciones en ese nodo.|1 hasta el número de distribuciones por nodo.|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
