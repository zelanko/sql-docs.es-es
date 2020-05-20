---
title: Sys. dm_os_enumerate_fixed_drives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c45db91b29c85d6ffced4e31e01fb8f24f338c16
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830545"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>Sys. dm_os_enumerate_fixed_drives (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Introducido en SQL Server 2019.

Enumera los volúmenes montados en Letras de unidad como `C:\` .

|Nombre de la columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|Ruta de acceso al volumen, como `C:\` .|  
|`drive_type`|`int`|Código para el tipo de unidad. Vea [ `GetDriveTypeW` función](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`drive_type_desc`|`nvarchar(512)`|Descripción del tipo de unidad. Vea [ `GetDriveTypeW` función](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`free_space_in_bytes`|`bigint`|Espacio libre en disco en bytes.|

## <a name="permissions"></a>Permisos

El usuario debe tener el `VIEW SERVER STATE` permiso en el servidor.

## <a name="see-also"></a>Consulte también  

 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con e/s &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
