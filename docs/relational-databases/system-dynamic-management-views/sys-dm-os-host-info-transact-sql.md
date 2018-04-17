---
title: sys.dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e8e36375f534a187c749bbd4217fddd0a98f8fb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve una fila que muestra información de versión de sistema operativo.  
  
|Nombre de columna |Tipo de datos |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |El tipo de sistema operativo: Windows o Linux |
|**host_distribution** |**nvarchar(256)** |Descripción del sistema operativo. |
|**host_release**|**nvarchar(256)**|Versión del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (número de versión). Para obtener una lista de valores y descripciones, consulte [versión del sistema operativo (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx). <br> Para Linux, devuelve una cadena vacía. |  
|**host_service_pack_level**|**nvarchar(256)**|Nivel de Service Pack del sistema operativo Windows. <br> Para Linux, devuelve una cadena vacía. |  
|**host_sku**|**int**|Identificador de referencia de almacén (SKU) de Windows. Para obtener una lista de identificadores de SKU y descripciones, consulte [función GetProductInfo](http://msdn.microsoft.com/library/ms724358.aspx). Acepta valores NULL. <br> Para Linux, devuelve NULL. |  
|**os_language_version**|**int**|Identificador de configuración regional (LCID) del sistema operativo Windows. Para obtener una lista de descripciones y valores LCID, consulte [Locale IDs Assigned by Microsoft](http://go.microsoft.com/fwlink/?LinkId=208080). No puede ser null.|  

## <a name="remarks"></a>Comentarios  
Esta vista es similar a [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), adición de columnas para diferenciar Windows y Linux.
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
El `SELECT` permiso en `sys.dm_os_host_info` se concede a los `public` rol de forma predeterminada. Si revoca, requiere `VIEW SERVER STATE` permiso en el servidor.   
 
>  [!CAUTION]
>  A partir de la versión [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.3 de CTP, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] versión 17 requiere `SELECT` permiso en `sys.dm_os_host_info` para conectarse a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Si `SELECT` se revoca el permiso de `public`, solo los inicios de sesión con `VIEW SERVER STATE` permiso puede conectarse con la versión más reciente de SSMS. (Otras herramientas, como `sqlcmd.exe` puede conectarse sin `SELECT` permiso en `sys.dm_os_host_info`.)

  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las columnas de la **sys.dm_os_host_info** vista.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Este es un conjunto en Windows de resultados de ejemplo:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |3082 |  

Este es un conjunto en Linux de resultados de ejemplo:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |3082 |  

  
## <a name="see-also"></a>Vea también  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

