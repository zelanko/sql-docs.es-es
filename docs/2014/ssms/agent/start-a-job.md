---
title: Iniciar un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d255a32058588d943ea88d596a4c0bfdb1badfed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325495"
---
# <a name="start-a-job"></a>Start a Job
  En este tema se describe cómo iniciar la ejecución de un trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
 Un trabajo es una serie especificada de acciones que realiza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden ejecutar en un servidor local o en varios servidores remotos.  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para iniciar un trabajo,utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-start-a-job"></a>Para iniciar un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server** y **Trabajos**. En función de cómo desea que se inicie el trabajo, realice uno de los siguientes procedimientos:  
  
    -   Si está trabajando en un solo servidor o en un servidor de destino, o está ejecutando un trabajo de servidor local en un servidor maestro, haga clic con el botón derecho en el trabajo que quiere iniciar y, después, haga clic en **Iniciar trabajo**.  
  
    -   Si desea iniciar varios trabajos, haga clic con el botón derecho en **Monitor de actividad de trabajo**y, a continuación, haga clic en **Ver actividad de trabajo**. En el Monitor de actividad de trabajo puede seleccionar varios trabajos, hacer clic con el botón derecho en su selección y hacer clic en **Iniciar trabajos**.  
  
    -   Si está trabajando en un servidor maestro y quiere que todos los servidores de destino ejecuten el trabajo simultáneamente, haga clic con el botón derecho en el trabajo que quiere iniciar, haga clic en **Iniciar trabajo**y, después, haga clic en **Iniciar en todos los servidores de destino**.  
  
    -   Si está trabajando en un servidor maestro y quiere especificar los servidores de destino para el trabajo, haga clic con el botón derecho en el trabajo que quiere iniciar, haga clic en **Iniciar trabajo**y, después, haga clic en **Iniciar en servidores de destino específicos**. En el cuadro de diálogo **Exponer instrucciones de descarga** , active la casilla **Estos servidores de destino** y, a continuación, seleccione cada servidor de destino en el que debe ejecutarse este trabajo.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-start-a-job"></a>Para iniciar un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 Para más información, vea [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para iniciar un trabajo**  
  
 Llame al método `Start` de la clase `Job` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
  
