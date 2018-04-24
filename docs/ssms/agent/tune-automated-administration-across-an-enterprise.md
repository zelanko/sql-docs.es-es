---
title: Optimizar la administración automatizada en una empresa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 24ae20b48409b95dadf758722e6694d55cf9945f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Optimizar la administración automatizada en una empresa
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

La administración multiservidor con el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] de Microsoft aprovecha las características de optimización automática de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Por tanto, en condiciones normales no es necesaria la optimización adicional de trabajos. Sin embargo, la carga de red aumenta al ejecutar trabajos, generar alertas y notificar operadores. Puede optimizar la administración automatizada en una empresa para minimizar el tráfico de red que causan estas actividades.  
  
## <a name="see-also"></a>Ver también  
[Supervisar el rendimiento del motor de flujo de datos](http://msdn.microsoft.com/en-us/11e17f4e-72ed-44d7-a71d-a68937a78e4c)  
  
