---
title: Sys. pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5d10a3bcbf02e88e054c12060299e9462af3004d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127451"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>Sys. pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre las operaciones de carga en curso [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]y completadas en. La información se conserva entre reinicios del sistema.  
  
|||||  
|-|-|-|-|  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|run_id|**int**|Identificador único de una ejecución del cargador.||  
|fase|**nvarchar(30**|La fase actual de la ejecución.|' CREATE_STAGING ', ' DMS_LOAD ', ' LOAD_INSERT ', ' LOAD_CLEANUP '|  
|request_id|**nvarchar (32)**|IDENTIFICADOR de la solicitud que se está ejecutando en esta fase.||  
|status|**nvarchar (16)**|Estado de esta fase.||  
|start_time|**datetime**|Hora a la que se inició la fase.||  
|end_time|**datetime**|Hora a la que finalizó la fase, si existe.|NULL si no se ha iniciado o está en curso.|  
|total_elapsed_time|**int**|Tiempo total que esta fase tardó en ejecutarse (o hasta ahora).|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), se producirá un error de materialización debido al desbordamiento.<br /><br /> El valor máximo en milisegundos es equivalente a 24,8 días.|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Data Warehouse y vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
