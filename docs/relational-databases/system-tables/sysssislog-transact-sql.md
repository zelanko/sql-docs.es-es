---
title: sysssislog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad08260b1db8e361e02963330b2de75d67c02d1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755433"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada entrada de registro generada por los paquetes o sus tareas y contenedores en tiempo de ejecución. Esta tabla se crea en la base de datos msdb al instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si configura el registro para registrar en otra base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se crea una tabla sysssislog con este formato en la base de datos especificada.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]escribe entradas de registro en esta tabla **solo** cuando los paquetes usan el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de registro.  
  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**int**|Identificador único de la entrada de registro.|  
|event|**sysname**|Nombre del evento que genera la entrada de registro.|  
|computer|**nvarchar**|Equipo en el que se estaba ejecutando el paquete cuando se generó la entrada de registro.|  
|operator|**nvarchar**|Nombre de usuario de la persona que ejecutó el paquete que generó la entrada de registro.|  
|source|**nvarchar**|Nombre del ejecutable, en el paquete, que generó la entrada de registro.|  
|sourceid|**uniqueidentifier**|GUID del ejecutable, en el paquete, que generó la entrada de registro.|  
|executionid|**uniqueidentifier**|GUID de la instancia de ejecución del ejecutable que genera la entrada de registro.|  
|starttime|**datetime**|La hora a la que comenzó la ejecución del paquete.|  
|endtime|**datetime**|Hora en que se completó el paquete.<br /><br /> Esta característica no está implementada. El valor de la columna endtime siempre es igual que el de la columna starttime.|  
|datacode|**int**|Valor entero opcional que normalmente indica el resultado de ejecutar el contenedor o la tarea.|  
|databytes|**imagen**|Matriz de bytes opcional que contiene información adicional.|  
|message|**nvarchar**|Descripción del evento e información asociada a dicho evento.|  
  
## <a name="see-also"></a>Consulte también  
 [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
