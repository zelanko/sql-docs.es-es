---
title: Sys. sysservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 333be9cb6c86c1db3801ac50159610c6d19d1611
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941099"
---
# <a name="syssysservers-transact-sql"></a>sys.sysservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada servidor al que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene acceso como origen de datos OLE DB.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**srvid**|**smallint**|Id. (solo para uso local) del servidor remoto.|  
|**srvstatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|Nombre del servidor.|  
|**srvproduct**|**sysname**|Nombre de producto del servidor remoto.|  
|**ProviderName**|**nvarchar(128)**|Nombre de proveedor OLE DB para el acceso a este servidor.|  
|**datasource**|**nvarchar(4000)**|Valor de origen de datos OLE DB.|  
|**location**|**nvarchar(4000)**|Valor de ubicación OLE DB.|  
|**providerstring**|**nvarchar(4000)**|Valor de cadena de proveedor OLE DB.|  
|**schemadate**|**datetime**|Fecha en que se actualizó la fila por última vez.|  
|**topologyx**|**int**|No se usa.|  
|**topología**|**int**|No se usa.|  
|**catalog**|**sysname**|Catálogo utilizado al establecer una conexión con un proveedor OLE DB.|  
|**srvcollation**|**sysname**|La intercalación del servidor.|  
|**ConnectTimeout**|**int**|Configuración de tiempo de espera para la conexión del servidor.|  
|**QueryTimeout**|**int**|Configuración del tiempo de espera para consultas sobre un servidor.|  
|**srvnetname**|**Char (30)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**isremote**|**bit**|1 = El servidor es un servidor remoto.<br /><br /> 0 = El servidor es un servidor vinculado.|  
|**rpc**|**bit**|1 = **sp_serveroption\@RPC** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@RPC** establecido en **false** u **OFF**.|  
|**pub**|**bit**|1 = **sp_serveroption\@pub** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@pub** establecido en **false** u **OFF**.|  
|**sub**|**bit**|1 = **sp_serveroption\@sub** se establece en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@sub** se establece en **false** u **OFF**.|  
|**dist**|**bit**|1 = **sp_serveroption\@Dist** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@Dist** establecido en **false** u **OFF**.|  
|**dpub**|**bit**|1 = **sp_serveroption\@DPUB** se establece en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@DPUB** se establece en **false** u **OFF**.|  
|**rpcout**|**bit**|1 = **sp_serveroption\@RPC out** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@RPC out** establecido en **false** u **OFF**.|  
|**DataAccess**|**bit**|1 = **sp_serveroption\@Data Access** se establece en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@Data Access** se establece en **false** u **OFF**.|  
|**collationcompatible**|**bit**|1 = **sp_serveroption\@collation compatible** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@collation compatible** establecido en **false** u **OFF**.|  
|**system**|**bit**|1 = **sp_serveroption\@System** está establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@System** está establecido en **false** u **OFF**.|  
|**useremotecollation**|**bit**|1 = **sp_serveroption\@Remote collation** establecido en **true** u **on**.<br /><br /> 0 = **sp_serveroption\@Remote collation** establecido en **false** u **OFF**.|  
|**lazyschemavalidation**|**bit**|1 = **la\@validación diferida** de esquemas de sp_serveroption está establecida en **true** u **on**.<br /><br /> 0 = **la\@validación diferida** de esquemas de sp_serveroption está establecida en **false** u **OFF**.|  
|**intercalación**|**sysname**|Intercalación de servidor establecida **por\@el nombre**de intercalación de sp_serveroption.|  
|**nonsqlsub**|bit|0 = el servidor es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 1 = el servidor no es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a las &#40;vistas del sistema TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
