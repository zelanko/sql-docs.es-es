---
title: Sys.tcp_endpoints (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1c04be5f76337422601486d08ff41316c7c98192
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="systcpendpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada extremo TCP que haya en el sistema. Los puntos de conexión que se describen en **sys.tcp_endpoints** proporcionar un objeto conceda y revoque el privilegio de conexión. La información que se muestra sobre puertos y direcciones IP no se utiliza para configurar los protocolos y es posible que no coincida con la configuración real del protocolo. Para ver y configurar protocolos, utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas >**||Hereda columnas de [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**port**|int|Número de puerto en el que escucha el extremo. No admite valores NULL.|  
|**is_dynamic_port**|bit|1 = El número de puerto se asignó dinámicamente.<br /><br /> No admite valores NULL.|  
|**ip_address**|**nvarchar(45)**|Dirección IP de escucha según se especifica en la cláusula LISTENER_IP. Acepta valores NULL.|  
  
## <a name="remarks"></a>Comentarios  
 Ejecute la siguiente consulta para reunir información sobre los extremos y las conexiones. Los extremos sin conexiones actuales o sin conexiones TCP aparecerán con valores NULL. Agregar el **donde** cláusula `WHERE des.session_id = @@SPID` para devolver información acerca de la conexión actual.  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de extremos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
