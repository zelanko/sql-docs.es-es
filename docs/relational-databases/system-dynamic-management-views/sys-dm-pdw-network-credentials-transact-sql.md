---
title: Sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
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
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e7b4534410eabf1186b115c07fef8a8d79960938
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005787"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>Sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Devuelve una lista de todas las credenciales de red se almacena en el [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo para todos los servidores de destino. Los resultados se muestran para el nodo de Control y cada nodo de proceso.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.|  
|target_server_name|**nvarchar(32)**|Dirección IP del servidor de destino que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] tendrá acceso mediante las credenciales de usuario y la contraseña.|  
|username|**nvarchar(32)**|Nombre de usuario para el que se almacena la contraseña.|  
|LAST_MODIFIED|**datetime**|Fecha y hora de la última operación que puede modificar la credencial.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el estado de vista del servidor.  
  
## <a name="general-remarks"></a>Notas generales  
 La clave para esta vista de administración dinámica es *pdw_node_id* plus *target_server_name*.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
