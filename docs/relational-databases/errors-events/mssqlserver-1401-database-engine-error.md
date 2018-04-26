---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d30bfa0a55fcf15c5027f4fd7dcdceaf9c22d55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1401|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_MASTERSTARTUP|  
|Texto del mensaje|Error en el inicio de la rutina del subproceso maestro de creación de reflejo de la base de datos por el siguiente motivo: %ls. Corrija la causa de este error y reinicie el servicio SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Error al iniciar el subproceso de control de creación de reflejo de la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
En el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], busque el error asociado que precedía a este mensaje. Corrija la causa de este error y reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER).  
  
## <a name="see-also"></a>Ver también  
[Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
