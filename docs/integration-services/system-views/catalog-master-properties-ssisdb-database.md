---
title: Catalog.master_properties (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>Catalog.master_properties (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Muestra las propiedades de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out Master.

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|El nombre de la propiedad maestro escalada.|  
|property_value|**nvarchar(max)**|El valor de la propiedad maestro escalada.|

## <a name="remarks"></a>Comentarios
Esta vista muestra una fila para cada propiedad principal de escalado. Las propiedades mostradas en esta vista incluyen lo siguiente:

|Nombre de propiedad|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Busca el servidor SQL Server que base de datos de registro en.|
|**LAST_ONLINE_TIME**|La última vez cuando escala Out maestro está conectado.|
|**MACHINE_IP**|La dirección IP de la máquina.|
|**NOMBREDEEQUIPO**|Nombre del equipo.|
|**MASTER_ADDRESS**|El extremo de escala Out Master.|
|**MASTER_SERVICE_PORT**|El puerto en el extremo de escala Out Master.|
|**SSLCERT_THUMBPRINT**|La huella digital del certificado de escala Out Master.|

## <a name="permissions"></a>Permissions
Todos los miembros del rol de base de datos public de tener permiso para esta vista de lectura. 

