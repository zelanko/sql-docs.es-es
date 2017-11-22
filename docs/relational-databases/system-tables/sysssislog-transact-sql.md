---
title: sysssislog (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs: TSQL
helpviewer_keywords: sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: "40"
author: spelluru
ms.author: spelluru
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2073eac1ce40cd735b4fde72744e5bc56f24686f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada entrada de registro generada por los paquetes o sus tareas y contenedores en tiempo de ejecución. Esta tabla se crea en la base de datos msdb al instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si configura el registro para registrar en otra base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se crea una tabla sysssislog con este formato en la base de datos especificada.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]Escribe entradas de registro en esta tabla **sólo** cuando utilizan la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de registro.  
  
  
|Nombre de columna|Tipo de datos|Descripción|  
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
|databytes|**image**|Matriz de bytes opcional que contiene información adicional.|  
|message|**nvarchar**|Descripción del evento e información asociada a dicho evento.|  
  
## <a name="see-also"></a>Vea también  
 [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
