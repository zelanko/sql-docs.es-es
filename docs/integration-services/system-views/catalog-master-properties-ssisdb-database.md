---
title: catalog.master_properties (base de datos SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85b3388be32ac33382ad34f12ec135e84313cb33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687451"
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (base de datos SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Muestra las propiedades del patrón de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Nombre de la propiedad del patrón de escalabilidad horizontal.|  
|property_value|**nvarchar(max)**|Valor de la propiedad del patrón de escalabilidad horizontal.|

## <a name="remarks"></a>Notas
Esta vista muestra una fila para cada propiedad del patrón de escalabilidad horizontal. Las propiedades mostradas en esta vista incluyen lo siguiente:

|Nombre de propiedad|Descripción|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Instancia de SQL Server donde se ubica la base de datos de registro.|
|**LAST_ONLINE_TIME**|Última vez que el patrón de escalabilidad horizontal estuvo conectado.|
|**MACHINE_IP**|Dirección IP de la máquina.|
|**MACHINE_NAME**|Nombre del equipo.|
|**MASTER_ADDRESS**|Punto de conexión del patrón de escalabilidad horizontal.|
|**MASTER_SERVICE_PORT**|Puerto del punto de conexión del patrón de escalabilidad horizontal.|
|**SSLCERT_THUMBPRINT**|Huella digital del certificado del patrón de escalabilidad horizontal.|

## <a name="permissions"></a>Permisos
Todos los miembros del rol de base de datos público tienen permiso de lectura para esta vista. 
