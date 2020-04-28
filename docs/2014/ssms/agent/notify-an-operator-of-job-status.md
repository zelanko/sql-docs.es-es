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
ms.openlocfilehash: ff9340d7c9fb768f9e057d00868a9e238421a5f4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798203"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
  En este tema se describe cómo establecer opciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] notificación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], o objetos de administración de SQL Server, por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo que el agente puede enviar notificaciones a los operadores acerca de los trabajos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para notificar a un operador el estado de un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
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
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
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
  
 Para obtener más información, vea [sp_add_notification &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para notificar a un operador el estado de un trabajo**  
  
 Utilice la clase `Job` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
