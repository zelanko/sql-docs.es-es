---
title: catalog.folders (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14930bfd90b242f30a8b3f265f6ed3b367bd07f9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296536"
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las carpetas del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**bigint**|Identificador único de la carpeta.|  
|NAME|**sysname(nvarchar(128)**|Nombre de la carpeta, que es único dentro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|description|**nvarchar(1024)**|Descripción de la carpeta.|  
|created_by_sid|**varbinary(85)**|Identificador de seguridad único (SID) del usuario que creó la carpeta.|  
|created_by_name|**nvarchar(128)**|Nombre del usuario que creó la carpeta.|  
|created_time|**datetimeoffset(7)**|Fecha y hora en que se creó la carpeta.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra una fila para cada carpeta en el catálogo.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la carpeta  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
