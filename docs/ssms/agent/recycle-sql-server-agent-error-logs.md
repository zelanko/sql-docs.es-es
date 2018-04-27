---
title: Reciclar registros de errores del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 74d7baf3f1cdbfc52253b683e4fe93c5316504f1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar registros de errores del Agente SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para reciclar los registros de errores del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . El reciclaje del registro cierra el registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e inicia un nuevo registro de errores sin reiniciar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Tenga en cuenta que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mantiene los nueve registros de errores más recientes. Si ya hay nueve registros de errores presentes, el reciclaje del registro de errores hará que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] elimine el registro de errores más antiguo.  
  
## <a name="see-also"></a>Ver también  
[Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
