---
title: Creación de una alerta de base de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 971f9519208f9af67d8d1d1af63737ed876bfff1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787486"
---
# <a name="create-a-sql-server-database-alert"></a>Crear una alerta de base de datos de SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El Monitor del sistema permite crear una alerta que se activará al alcanzar un valor de umbral de un contador del Monitor del sistema. Como respuesta a la alerta, el Monitor del sistema puede iniciar una aplicación, como por ejemplo una aplicación personalizada creada para tratar la condición de alerta. Por ejemplo, puede crear una alerta que se active cuando el número de interbloqueos sea superior a un valor específico.  
  
 También se pueden definir alertas mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información, consulte [Alertas](../../ssms/agent/alerts.md).  
  
 Para obtener más información sobre cómo usar el Monitor del sistema para configurar una alerta de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Configurar una alerta de base de datos de SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
