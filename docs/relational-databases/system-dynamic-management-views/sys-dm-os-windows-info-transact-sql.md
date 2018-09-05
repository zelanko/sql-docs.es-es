---
title: sys.dm_os_windows_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27896207321b39ef37d4317a6ca8c4e332ccee55
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348143"
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila con información sobre la versión del sistema operativo Windows.  
  
  Solo se aplica a SQL Server que se ejecutan en Windows. Para ver información similar para SQL Server que se ejecutan en un host que no sean Windows, como Linux, use [sys.dm_os_host_info &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Para Windows, devuelve el número de versión. Para obtener una lista de valores y descripciones, consulte [versión del sistema operativo (Windows)](/windows/desktop/SysInfo/operating-system-version). No puede ser NULL.|  
|**windows_service_pack_level**|**nvarchar(256)**| Para Windows, devuelve el número de service pack. No puede ser NULL. |  
|**windows_sku**|**int**|Para Windows, devuelve el identificador de unidad mantener existencias (SKU) de Windows. Para obtener una lista de los identificadores de SKU y descripciones, consulte [función GetProductInfo](http://msdn.microsoft.com/library/ms724358.aspx). Es que acepta valores NULL. |  
|**os_language_version**|**int**| Para Windows, devuelve el identificador de configuración regional (LCID) de Windows del sistema operativo. Para obtener una lista de valores LCID y las descripciones, consulte [Locale IDs Assigned by Microsoft](http://go.microsoft.com/fwlink/?LinkId=208080). No puede ser NULL.|  
  
  
## <a name="permissions"></a>Permisos  
Se concede el permiso SELECT en sys.dm_os_windows_info al rol public de forma predeterminada. Si revoca, requiere el permiso VIEW SERVER STATE en el servidor.  

## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones
Para ver información de SQL que se ejecuta en un host que no sean Windows, como Linux, use [sys.dm_os_host_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todas las columnas de la **sys.dm_os_windows_info** vista.  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo.  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

