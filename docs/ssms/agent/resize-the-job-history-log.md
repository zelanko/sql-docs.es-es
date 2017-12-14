---
title: "Cambiar el tamaño del registro del historial de trabajos | Microsoft Docs"
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
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47f6b26598e5b603a95f9edda06a587b801237db
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo establecer límites de tamaño para registros de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para establecer los límites de tamaño de los registros de historial de trabajos, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>Para cambiar el tamaño del registro de historial de trabajos según un tamaño sin procesar  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Historial** y asegúrese de que la opción **Limitar tamaño del registro de historial de trabajos**esté seleccionada.  
  
4.  En la casilla **Tamaño máximo del registro de historial de trabajos (filas)** , escriba el número máximo de filas que debe permitir el registro de historial de trabajos.  
  
5.  En la casilla **Máximo de filas de historial de trabajos por trabajo** , escriba el número máximo de filas que se va a permitir para un trabajo en el historial de trabajos.  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>Para cambiar el tamaño del registro de historial de trabajos según el tiempo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, a continuación, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Historial** y, a continuación, haga clic en **Quitar automáticamente historial del agente**.  
  
4.  Seleccione el número apropiado de **días**, **semanas**o **meses**.  
  
