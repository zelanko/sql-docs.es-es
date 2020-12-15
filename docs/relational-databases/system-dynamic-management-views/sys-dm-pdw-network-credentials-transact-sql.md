---
description: sys.dm_pdw_network_credentials (Transact-SQL)
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 7d94853e62c1e9e97ddd65ad973e9e481d90bcb0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472746"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Devuelve una lista de todas las credenciales de red almacenadas en el [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo para todos los servidores de destino. Los resultados se muestran para el nodo de control y para cada nodo de proceso.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.|  
|target_server_name|**nvarchar(32)**|Dirección IP del servidor de destino al que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] se va a tener acceso mediante las credenciales de nombre de usuario y contraseña.|  
|username|**nvarchar(32)**|Nombre de usuario para el que se almacena la contraseña.|  
|last_modified|**datetime**|Fecha y hora de la última operación que modificó la credencial.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el estado de vista del servidor.  
  
## <a name="general-remarks"></a>Notas generales  
 La clave de esta vista de administración dinámica es *pdw_node_id* más *target_server_name*.  
  
## <a name="see-also"></a>Consulte también  
 [Azure Synapse Analytics y vistas de administración dinámica de almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
