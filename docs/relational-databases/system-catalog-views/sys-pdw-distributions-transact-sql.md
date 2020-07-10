---
title: Sys. pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 12a3318f88a719ab70043e2685a475e14cf24fdc
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197402"
---
# <a name="syspdw_distributions-transact-sql"></a>Sys. pdw_distributions (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información acerca de las distribuciones del dispositivo. Muestra una fila por distribución de dispositivo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Identificador numérico único asociado a la distribución.<br /><br /> Clave para esta vista.|1 al número de nodos de proceso en el dispositivo multiplicado por el número de distribuciones por nodo de proceso.|  
|pdw_node_id|**int**|IDENTIFICADOR del nodo en el que se encuentra esta distribución.|Vea pdw_node_id en [Sys. dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|name|**nvarchar(32)**|Identificador de cadena asociado a la distribución, que se utiliza como sufijo en las tablas distribuidas.|Cadena formada por "A-Z", "a-z", "0-9", "_", "-".|  
|position|**int**|Posición de la distribución dentro de un nodo respectiva a otras distribuciones en ese nodo.|1 al número de distribuciones por nodo.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
