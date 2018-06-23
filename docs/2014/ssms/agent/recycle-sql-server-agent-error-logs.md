---
title: Reciclar registros de errores del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e966fcf544ace7a719d4760c366c69fe91b892f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104164"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar registros de errores del Agente SQL Server
  Utilice esta página para reciclar los registros de errores del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El reciclaje del registro cierra el registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inicia un nuevo registro de errores sin reiniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tenga en cuenta que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene los nueve registros de errores más recientes. Si ya hay nueve registros de errores presentes, el reciclaje del registro de errores hará que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimine el registro de errores más antiguo.  
  
## <a name="see-also"></a>Vea también  
 [Registro de errores del Agente SQL Server](sql-server-agent-error-log.md)  
  
  