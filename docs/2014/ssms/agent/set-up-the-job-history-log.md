---
title: Configurar el registro de historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 48b0c0b72b7b27ca944e78603d2c574a8f4d27dc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85001771"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
  En este tema se describe cómo configurar el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro de historial de trabajos del agente.  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Configuración del registro de historial de trabajos usando lo siguiente:**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
 **Para configurar el registro de historial de trabajos**  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server** , seleccione la página **Historial** .  
  
4.  Elija entre las siguientes opciones:  
  
    1.  Seleccione **Limitar tamaño del registro de historial de trabajos**y, a continuación, escriba el número máximo de filas del registro y el número máximo de filas por trabajo.  
  
    2.  Seleccione **Quitar automáticamente historial del agente**y especifique un período de tiempo para que se elimine del registro la información anterior al mismo.  
  
## <a name="see-also"></a>Consulte también  
 [Implementar trabajos](implement-jobs.md)   
 [Actividad supervisar trabajo](monitor-job-activity.md)   
 [Crear trabajos](create-jobs.md)  
  
  
