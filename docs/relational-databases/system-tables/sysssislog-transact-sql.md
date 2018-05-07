---
title: sysssislog (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: 40
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f60ec3735bc89c7e729ac6ec01e6f62f126c51f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada entrada de registro generada por los paquetes o sus tareas y contenedores en tiempo de ejecución. Esta tabla se crea en la base de datos msdb al instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si configura el registro para registrar en otra base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se crea una tabla sysssislog con este formato en la base de datos especificada.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Escribe entradas de registro en esta tabla **sólo** cuando utilizan la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de registro.  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|Identificador único de la entrada de registro.|  
|event|**sysname**|Nombre del evento que genera la entrada de registro.|  
|computer|**nvarchar**|Equipo en el que se estaba ejecutando el paquete cuando se generó la entrada de registro.|  
|operador|**nvarchar**|Nombre de usuario de la persona que ejecutó el paquete que generó la entrada de registro.|  
|origen|**nvarchar**|Nombre del ejecutable, en el paquete, que generó la entrada de registro.|  
|sourceid|**uniqueidentifier**|GUID del ejecutable, en el paquete, que generó la entrada de registro.|  
|executionid|**uniqueidentifier**|GUID de la instancia de ejecución del ejecutable que genera la entrada de registro.|  
|starttime|**datetime**|El tiempo que el paquete empezó a ejecutarse.|  
|endtime|**datetime**|Hora en que se completó el paquete.<br /><br /> Esta característica no está implementada. El valor de la columna endtime siempre es igual que el de la columna starttime.|  
|datacode|**int**|Valor entero opcional que normalmente indica el resultado de ejecutar el contenedor o la tarea.|  
|databytes|**imagen**|Matriz de bytes opcional que contiene información adicional.|  
|message|**nvarchar**|Descripción del evento e información asociada a dicho evento.|  
  
## <a name="see-also"></a>Vea también  
 [Integration Services & #40; SSIS & #41; Registro](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
