---
title: Configurar el registro de historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 206f25645a0b00829f76d45c497938d29a9775cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107335"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
  En este tema se describe cómo configurar el registro de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Configuración del registro de historial de trabajos utilizando lo siguiente:**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
 **Para configurar el registro de historial de trabajos**  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server** , seleccione la página **Historial** .  
  
4.  Elija una de las opciones siguientes:  
  
    1.  Seleccione **Limitar tamaño del registro de historial de trabajos**y, a continuación, escriba el número máximo de filas del registro y el número máximo de filas por trabajo.  
  
    2.  Seleccione **Quitar automáticamente historial del agente**y especifique un período de tiempo para que se elimine del registro la información anterior al mismo.  
  
## <a name="see-also"></a>Vea también  
 [Implementar trabajos](implement-jobs.md)   
 [Supervisar la actividad de trabajo](monitor-job-activity.md)   
 [Crear trabajos](create-jobs.md)  
  
  