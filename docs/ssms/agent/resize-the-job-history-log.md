---
title: Cambiar el tamaño del registro del historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5dea3b0a7eb9076bb778a14a4c8ab1834df0b93e
ms.sourcegitcommit: 58f1d5498c87bfe0f6ec4fd9d7bbe723be47896b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995839"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe el modo de establecer límites de tamaño para registros de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para establecer los límites de tamaño de los registros de historial de trabajos, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
*Para cambiar el tamaño del registro de historial de trabajos según un tamaño sin procesar*
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Historial** y, luego, configure que la opción **Limitar tamaño del registro de historial de trabajos** esté seleccionada.  
  
4.  En la casilla **Tamaño máximo del registro de historial de trabajos (filas)** , escriba el número máximo de filas que debe permitir el registro de historial de trabajos.  
  
5.  En la casilla **Máximo de filas de historial de trabajos por trabajo** , escriba el número máximo de filas que se va a permitir para un trabajo en el historial de trabajos.  
  
**Para cambiar el tamaño del registro de historial de trabajos según el tiempo:**
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, a continuación, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Historial** y, a continuación, haga clic en **Quitar automáticamente historial del agente**.  
  
4.  Seleccione el número apropiado de **días**, **semanas** o **meses**.  
  
