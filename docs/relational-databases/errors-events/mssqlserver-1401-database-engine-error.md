---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: fdae41b3011a31be94777a9ffc05dd9304d0f315
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
  
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
  
## <a name="see-also"></a>Vea también  
[Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
