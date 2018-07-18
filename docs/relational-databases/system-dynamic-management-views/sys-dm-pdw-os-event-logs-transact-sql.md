---
title: Sys.dm_pdw_os_event_logs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 27ec56462721ad3f8282366a11c274062aba7a91
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38978927"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre los eventos de Windows diferentes registros en distintos nodos.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Este registro es de un nodo de dispositivo.<br /><br /> pdw_node_id y nombreDelRegistro forman la clave para esta vista.||  
|nombreDelRegistro|**nvarchar(255)**|Nombre del registro de eventos de Windows.<br /><br /> pdw_node_id y nombreDelRegistro forman la clave para esta vista.||  
|log_source|**nvarchar(255)**|Nombre del origen de registro de eventos de Windows.||  
|event_id|**int**|Id. del evento. No es único.||  
|event_type|**nvarchar(255)**|Tipo del evento, que identifica la gravedad.|'Information', 'Advertencia', 'Error'|  
|event_message|**nvarchar(4000)**|Detalles del evento.||  
|generate_time|**datetime**|Tiempo que se creó el evento.||  
|write_time|**datetime**|El evento se ha escrito realmente en el registro de tiempo.||  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, consulte la sección de valores máximos de la vista del sistema en el [valores mínimos y máximos (SQL Server PDW)](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
