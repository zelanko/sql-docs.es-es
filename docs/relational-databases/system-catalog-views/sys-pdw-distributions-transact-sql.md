---
title: Sys.pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0af52bacdd709c067a62192f3a114453692cbedb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987347"
---
# <a name="syspdwdistributions-transact-sql"></a>Sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre las distribuciones en el dispositivo. Muestra una fila por cada distribución de dispositivo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Identificador numérico único asociado con la distribución.<br /><br /> Clave para esta vista.|1 al número de nodos de proceso en el dispositivo multiplicado por el número de distribuciones por nodo de proceso.|  
|pdw_node_id|**int**|Identificador del nodo en que esta distribución se encuentra.|Vea pdw_node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|NAME|**nvarchar(32)**|Identificador asociado con la distribución, utilizada como sufijo en las tablas distribuidas de cadena.|Cadena compuesta de "A-z", "a-z", "0-9', '_','-'.|  
|position|**int**|Posición de la distribución dentro de un nodo correspondiente para otras distribuciones en ese nodo.|1 para el número de distribuciones por nodo.|  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
