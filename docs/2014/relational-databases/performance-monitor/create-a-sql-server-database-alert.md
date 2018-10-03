---
title: Creación de una alerta de base de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f58ae046ce906472a8c4b979832e278c4e2b7ad8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114996"
---
# <a name="create-a-sql-server-database-alert"></a>Crear una alerta de base de datos de SQL Server
  El Monitor del sistema permite crear una alerta que se activará al alcanzar un valor de umbral de un contador del Monitor del sistema. Como respuesta a la alerta, el Monitor del sistema puede iniciar una aplicación, como por ejemplo una aplicación personalizada creada para tratar la condición de alerta. Por ejemplo, puede crear una alerta que se active cuando el número de interbloqueos sea superior a un valor específico.  
  
 También se pueden definir alertas mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [Alertas](../../ssms/agent/alerts.md).  
  
 Para obtener más información sobre cómo usar el Monitor del sistema para configurar una alerta de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Configurar una alerta de base de datos de SQL Server &#40;Windows&#41;](../performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Vea también  
 [sp_add_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql)  
  
  
