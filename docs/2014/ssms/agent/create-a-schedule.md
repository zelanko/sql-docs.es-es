---
title: Crear una programación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a00b07bb54d30d4e1db49cf2db70dec8286b27e0
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798291"
---
# <a name="create-a-schedule"></a>Create a Schedule
  Puede crear una programación para los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para crear una programación, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-create-a-schedule"></a>Para crear una programación  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**, haga clic con el botón derecho en **Trabajos**y seleccione **Administrar programaciones**.  
  
3.  En el cuadro de diálogo **Administrar programaciones** , haga clic en **Nueva**.  
  
4.  En el cuadro **Nombre** , escriba el nombre de la nueva programación.  
  
5.  Si no desea que la programación tenga efecto inmediatamente después de su creación, desactive la casilla **Habilitada** .  
  
6.  En **Tipo de programación**, seleccione una de las siguientes operaciones:  
  
    -   Para iniciar el trabajo cuando las CPU alcancen la condición de inactivas, haga clic en **Iniciar al quedar inactivas las CPU**.  
  
    -   Si desea que una programación se ejecute varias veces, haga clic en **Periódica**. Para establecer la programación periódica, rellene los grupos **Frecuencia**, **Frecuencia diaria**y **Duración** en el cuadro de diálogo.  
  
    -   Si desea que la programación se ejecute solo una vez, haga clic en **Una vez**. Para establecer la programación en **Una vez** , rellene el grupo **Única repetición** del cuadro de diálogo.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-schedule"></a>Para crear una programación  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
 Para obtener más información, [vea &#40;SP_ADD_SCHEDULE Transact-&#41;SQL](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql).  
  
##  <a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para crear una programación**  
  
 Utilice la clase `JobSchedule` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
