---
title: sys.dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 052402d3a394e8da3e08828992127d3cd89b95ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900164"
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve una fila que muestra información de versión del sistema operativo.  
  
|Nombre de columna |Tipo de datos |Descripción |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |El tipo de sistema operativo: Windows o Linux |
|**host_distribution** |**nvarchar(256)** |Descripción del sistema operativo. |
|**host_release**|**nvarchar(256)**|Versión del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (número de versión). Para obtener una lista de valores y descripciones, consulte [versión del sistema operativo (Windows)](/windows/desktop/SysInfo/operating-system-version). <br> Para Linux, devuelve una cadena vacía. |  
|**host_service_pack_level**|**nvarchar(256)**|Nivel de Service Pack del sistema operativo Windows. <br> Para Linux, devuelve una cadena vacía. |  
|**host_sku**|**int**|Identificador de referencia de almacén (SKU) de Windows. Para obtener una lista de los identificadores de SKU y descripciones, consulte [función GetProductInfo](https://msdn.microsoft.com/library/ms724358.aspx). Acepta valores NULL. <br> Para Linux, devuelve NULL. |  
|**os_language_version**|**int**|Identificador de configuración regional (LCID) del sistema operativo Windows. Para obtener una lista de valores LCID y las descripciones, consulte [Locale IDs Assigned by Microsoft](https://go.microsoft.com/fwlink/?LinkId=208080). No puede ser null.|  

## <a name="remarks"></a>Comentarios  
Esta vista es similar a [sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), agregar columnas para diferenciar Windows y Linux.
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
El `SELECT` permiso en `sys.dm_os_host_info` se concede a los `public` rol de forma predeterminada. Si revoca, requiere `VIEW SERVER STATE` permiso en el servidor.   
 
> [!CAUTION]
>  Desde la versión [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] requiere la versión 17 `SELECT` permiso en `sys.dm_os_host_info` con el fin de conectarse a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Si `SELECT` se revoca el permiso de `public`, solo los inicios de sesión con `VIEW SERVER STATE` permiso puede conectarse con la versión más reciente de SSMS. (Existen otras herramientas, como `sqlcmd.exe` puede conectarse sin `SELECT` permiso en `sys.dm_os_host_info`.)

  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las columnas de la **sys.dm_os_host_info** vista.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Este es un ejemplo conjunto de resultados en Windows:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |3082 |  

Este es un resultado de ejemplo que se establezca en Linux:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |3082 |  

  
## <a name="see-also"></a>Vea también  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

