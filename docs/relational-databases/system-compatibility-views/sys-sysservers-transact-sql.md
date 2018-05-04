---
title: Sys.sysservers (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysservers
- sysservers_TSQL
- sysservers
- sys.sysservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysservers system table
- sys.sysservers compatibility view
ms.assetid: d02f186f-c00f-44a6-b38d-dc78a3d2145b
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 26847a019cd903c08081221ce2b24ea0ca0071e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada servidor al que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene acceso como origen de datos OLE DB.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|Id. (solo para uso local) del servidor remoto.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SRVNAME**|**sysname**|Nombre del servidor.|  
|**srvproduct**|**sysname**|Nombre de producto del servidor remoto.|  
|**ProviderName**|**nvarchar(128)**|Nombre de proveedor OLE DB para el acceso a este servidor.|  
|**datasource**|**nvarchar(4000)**|Valor de origen de datos OLE DB.|  
|**Ubicación**|**nvarchar(4000)**|Valor de ubicación OLE DB.|  
|**PROVIDERSTRING**|**nvarchar(4000)**|Valor de cadena de proveedor OLE DB.|  
|**schemadate**|**datetime**|Fecha en que se actualizó la fila por última vez.|  
|**topologyx**|**int**|No se usa.|  
|**topologyy**|**int**|No se usa.|  
|**catalog**|**sysname**|Catálogo utilizado al establecer una conexión con un proveedor OLE DB.|  
|**srvcollation**|**sysname**|La intercalación del servidor.|  
|**ConnectTimeout**|**int**|Configuración de tiempo de espera para la conexión del servidor.|  
|**QueryTimeout**|**int**|Configuración del tiempo de espera para consultas sobre un servidor.|  
|**srvnetname**|**Char (30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = El servidor es un servidor remoto.<br /><br /> 0 = El servidor es un servidor vinculado.|  
|**RPC**|**bit**|1 = **sp_serveroption@rpc** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@rpc** establecido en **false** o **desactivar**.|  
|**pub**|**bit**|1 = **sp_serveroption@pub** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@pub** establecido en **false** o **desactivar**.|  
|**Sub**|**bit**|1 = **sp_serveroption@sub** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@sub** establecido en **false** o **desactivar**.|  
|**dist**|**bit**|1 = **sp_serveroption@dist** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@dist** establecido en **false** o **desactivar**.|  
|**dpub**|**bit**|1 = **sp_serveroption@dpub** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@dpub** establecido en **false** o **desactivar**.|  
|**rpcout**|**bit**|1 =  **sp_serveroption@rpc out** establecido en **true** o **en**.<br /><br /> 0 =  **sp_serveroption@rpc out** establecido en **false** o **desactivar**.|  
|**DataAccess**|**bit**|1 =  **sp_serveroption@data acceso** establecido en **true** o **en**.<br /><br /> 0 =  **sp_serveroption@data acceso** establecido en **false** o **desactivar**.|  
|**collationcompatible**|**bit**|1 =  **sp_serveroption@collation compatible** establecido en **true** o **en**.<br /><br /> 0 =  **sp_serveroption@collation compatible** establecido en **false** o **desactivar**.|  
|**Sistema**|**bit**|1 = **sp_serveroption@system** establecido en **true** o **en**.<br /><br /> 0 = **sp_serveroption@system** establecido en **false** o **desactivar**.|  
|**UseRemoteCollation**|**bit**|1 =  **sp_serveroption@remote intercalación** establecido en **true** o **en**.<br /><br /> 0 =  **sp_serveroption@remote intercalación** establecido en **false** o **desactivar**.|  
|**lazyschemavalidation**|**bit**|1 =  **sp_serveroption@lazy la validación del esquema** establecido en **true** o **en**.<br /><br /> 0 =  **sp_serveroption@lazy la validación del esquema** establecido en **false** o **desactivar**.|  
|**Intercalación**|**sysname**|Intercalación del servidor según lo establecido por  **sp_serveroption@collation nombre**.|  
|**nonsqlsub**|bit|0 = el servidor es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = el servidor no es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
