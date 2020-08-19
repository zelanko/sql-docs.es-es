---
description: catalog.master_properties (base de datos SSISDB)
title: catalog.master_properties (base de datos SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09e13f54b3e7ee92ed72b055246ea1235845448f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422059"
---
# <a name="catalogmaster_properties-ssisdb-database"></a>catalog.master_properties (base de datos SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Muestra las propiedades del patrón de escalabilidad horizontal de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Nombre de la propiedad del patrón de escalabilidad horizontal.|  
|property_value|**nvarchar(max)**|Valor de la propiedad del patrón de escalabilidad horizontal.|

## <a name="remarks"></a>Observaciones
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
