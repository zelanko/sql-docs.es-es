---
description: Set Up the Job History Log
title: Set Up the Job History Log
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: d00c7cb8ee961dca15a7fcdfe0950963e7dec7b2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402494"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

En este tema se describe cómo configurar el registro de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Configuración del registro de historial de trabajos usando lo siguiente:** [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usar SQL Server Management Studio  
**Para configurar el registro de historial de trabajos**  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y, luego, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server** , seleccione la página **Historial** .  
  
4.  Elija entre las siguientes opciones:  
  
    1.  Seleccione **Limitar tamaño del registro de historial de trabajos** y, a continuación, escriba el número máximo de filas del registro y el número máximo de filas por trabajo.  
  
    2.  Seleccione **Quitar automáticamente historial del agente** y especifique un período de tiempo para que se elimine del registro la información anterior al mismo.  
  
## <a name="see-also"></a>Consulte también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
[Actividad de trabajos de monitor](../../ssms/agent/monitor-job-activity.md)  
[Crear trabajos](../../ssms/agent/create-jobs.md)  
