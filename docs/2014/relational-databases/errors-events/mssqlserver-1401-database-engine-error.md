---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0ea81464154aff79cd31a73871702d5110b1ce1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968025"
---
# <a name="mssqlserver_1401"></a>MSSQLSERVER_1401
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1401|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_MASTERSTARTUP|  
|Texto del mensaje|Error en el inicio de la rutina del subproceso maestro de creación de reflejo de la base de datos por el siguiente motivo: %ls. Corrija la causa de este error y reinicie el servicio SQL Server.|  
  
## <a name="explanation"></a>Explicación  
 Error al iniciar el subproceso de control de creación de reflejo de la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
 En el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], busque el error asociado que precedía a este mensaje. Corrija la causa de este error y reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER).  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
