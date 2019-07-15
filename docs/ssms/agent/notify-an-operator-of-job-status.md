---
title: Notificar a un operador el estado de un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e45be45ce29e7e63d6831b841824fc2069680e6d
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685652"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo establecer opciones de notificación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server de modo que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda enviar a los operadores notificaciones acerca de los trabajos.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para notificar a un operador el estado de un trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
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
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar a un operador el estado de un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para notificar a un operador el estado de un trabajo**  
  
Use la clase **Job** mediante el lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
