---
title: catalog.worker_agents (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2678853d13436811b53b40473a04191625535db
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295142"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Muestra la información del trabajo de escalabilidad horizontal [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Id. de agente de trabajo del trabajo de escalabilidad horizontal.|
|IsEnabled|**bit**|Si está habilitado el trabajo de escalabilidad horizontal.|
|DisplayName|**nvarchar(256)**|Nombre para mostrar del trabajo de escalabilidad horizontal.|
|Descripción|**nvarchar(256)**|Descripción del trabajo de escalabilidad horizontal.|
|MachineName|**nvarchar(256)**|Nombre de máquina del trabajo de escalabilidad horizontal.|
|Etiquetas|**nvarchar(max)**|Etiquetas del trabajo de escalabilidad horizontal.|
|UserAccount|**nvarchar(256)**|Cuenta de usuario que ejecuta el servicio de trabajo de escalabilidad horizontal.|
|LastOnlineTime|**datetimeoffset(7)**|Última vez que el trabajo de escalabilidad horizontal estuvo en línea.|

## <a name="remarks"></a>Notas
Esta vista muestra una fila para cada trabajo de escalabilidad horizontal que esté conectado al patrón de escalabilidad horizontal que funciona con el catálogo de SSISDB.

## <a name="permissions"></a>Permisos
Esta vista exige uno de los siguientes permisos:

- Pertenencia al rol de base de datos de **ssis_admin**

- Pertenencia al rol de base de datos **ssis_cluster_executor**

- Pertenencia al rol de servidor de **sysadmin**
