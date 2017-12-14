---
title: Reciclar registros de errores del Agente SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7516288036cd22deb58a85b076c543f4bc9fb7de
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar registros de errores del Agente SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para reciclar los registros de errores del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. El reciclaje del registro cierra el registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e inicia un nuevo registro de errores sin reiniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Tenga en cuenta que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mantiene los nueve registros de errores más recientes. Si ya hay nueve registros de errores presentes, el reciclaje del registro de errores hará que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] elimine el registro de errores más antiguo.  
  
## <a name="see-also"></a>Vea también  
[Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
