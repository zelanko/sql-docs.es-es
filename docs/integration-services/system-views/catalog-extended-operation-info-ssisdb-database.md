---
title: catalog.extended_operation_info (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca82bdc8a04ffee4426ffb934a9e9a4ddaf4654f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296609"
---
# <a name="catalogextended_operation_info-ssisdb-database"></a>catalog.extended_operation_info (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra la información extendida sobre todas las operaciones del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|El identificador único (id.) de la información extendida.|  
|operation_id|**bigint**|El Identificador único de la operación que corresponde a la información extendida.|  
|object_name|**nvarchar(260)**|Nombre del objeto.|  
|object_type|**smallint**|Tipo de objeto afectado por la operación. El objeto puede ser una carpeta (`10`), proyecto (`20`), paquete (`30`), entorno (`40`) o instancia de ejecución (`50`).|  
|reference_id|**bigint**|El Identificador único de la referencia que se utiliza en la operación.|  
|status|**int**|Estado de la operación. Los valores posibles son creado (`1`), en ejecución (`2`), cancelado (`3`), con errores (`4`), pendiente (`5`), finalizado inesperadamente (`6`), correcto (`7`), deteniendo (`8`) y completado (`9`).|  
|start_time|**datetimeoffset(7)**|Fecha y hora en que empezó la operación.|  
|end_time|**datetimeoffset(7)**|La fecha y hora en la que finalizó la operación.|  
  
## <a name="remarks"></a>Notas  
 Una operación única puede tener varias filas de información extendida.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
