---
title: Reciclar registros de errores del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0654dcc83e757751ac055192775c0ee958f26e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753072"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar registros de errores del Agente SQL Server
  Utilice esta página para reciclar los registros de errores del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El reciclaje del registro cierra el registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inicia un nuevo registro de errores sin reiniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tenga en cuenta que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene los nueve registros de errores más recientes. Si ya hay nueve registros de errores presentes, el reciclaje del registro de errores hará que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimine el registro de errores más antiguo.  
  
## <a name="see-also"></a>Vea también  
 [Registro de errores del Agente SQL Server](sql-server-agent-error-log.md)  
  
  
