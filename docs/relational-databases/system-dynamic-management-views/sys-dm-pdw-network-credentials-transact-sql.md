---
title: Sys.dm_pdw_network_credentials (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.reviewer: 
ms.service: 
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21935bde6ebefe2b30743a4961ba05e3092539d6
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>Sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Devuelve una lista de todas las credenciales de red se almacena en la [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo para todos los servidores de destino. Resultados se muestran para el nodo de Control y cada nodo de proceso.  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.|  
|target_server_name|**nvarchar (32)**|Dirección IP del servidor de destino que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] tendrá acceso mediante las credenciales de nombre de usuario y contraseña.|  
|username|**nvarchar (32)**|Nombre de usuario para el que se almacena la contraseña.|  
|LAST_MODIFIED|**datetime**|Fecha y hora de la última operación que se modificó la credencial.|  
  
## <a name="permissions"></a>Permissions  
 Requiere que el estado de vista del servidor.  
  
## <a name="general-remarks"></a>Notas generales  
 La clave para esta vista de administración dinámica es *pdw_node_id* más *target_server_name*.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
