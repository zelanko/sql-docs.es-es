---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23dc13b8dac23914cc4f337e4b39fbf84ee4b782
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860466"
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
  
## <a name="see-also"></a>Consulte también  
[Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
