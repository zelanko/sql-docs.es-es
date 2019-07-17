---
title: Notificar a un operador el estado de un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 268f75902f752551e33467e422b6f33ea6c4dcb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211354"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
  En este tema se describe cómo establecer opciones de notificación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server de modo que el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda enviar a los operadores notificaciones acerca de los trabajos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para notificar a un operador el estado de un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**, **Trabajos**, haga clic con el botón derecho en el trabajo que desea editar y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , seleccione la página **Notificaciones** .  
  
4.  Si desea enviar una notificación a un operador por **correo electrónico**, seleccione un operador en la lista y elija alguna de las siguientes opciones:  
  
    -   **Si el trabajo tiene éxito** para notificar al operador cuando el trabajo concluye correctamente.  
  
    -   **Si el trabajo no tiene éxito** para notificar al operador cuando el trabajo se completa de manera incorrecta.  
  
    -   **Si el trabajo termina** para notificar al operador independientemente del estado de la finalización.  
  
5.  Si desea enviar una notificación a un operador por buscapersonas, active la opción **Buscapersonas**, seleccione un operador en la lista y elija alguna de las siguientes opciones:  
  
    -   **Si el trabajo tiene éxito** para notificar al operador cuando el trabajo concluye correctamente.  
  
    -   **Si el trabajo no tiene éxito** para notificar al operador cuando el trabajo se completa de manera incorrecta.  
  
    -   **Si el trabajo termina** para notificar al operador independientemente del estado de la finalización.  
  
6.  Si desea enviar una notificación a un operador por envío de red, active la opción **Envío de red**, seleccione un operador en la lista y elija alguna de las siguientes opciones:  
  
    -   **Si el trabajo tiene éxito** para notificar al operador cuando el trabajo concluye correctamente.  
  
    -   **Si el trabajo no tiene éxito** para notificar al operador cuando el trabajo se completa de manera incorrecta.  
  
    -   **Si el trabajo termina** para notificar al operador independientemente del estado de la finalización.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'Fran??ois Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_add_notification &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para notificar a un operador el estado de un trabajo**  
  
 Utilice la clase `Job` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
