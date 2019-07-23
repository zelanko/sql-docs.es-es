---
title: Crear una alerta con nivel de gravedad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a87769e03e9661f9020b61ec4ea9a34b64084668
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267294"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe el modo de crear una alerta del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se active cuando se produzca un evento con un nivel de gravedad específico en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para crear una alerta con nivel de gravedad, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona una forma gráfica y fácil de administrar todo el sistema de alertas, y constituye el método recomendado para configurar una infraestructura de alertas.  
  
-   Los eventos generados durante **xp_logevent** se producen en la base de datos maestra. Por tanto, **xp_logevent** no desencadena una alerta a menos que el valor de **@database_name** de la alerta sea is **'master'** o NULL.  
  
-   Con los niveles de gravedad entre 19 y 25 se envía un mensaje de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al registro de la aplicación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows y se desencadena una alerta. Los eventos con niveles de gravedad inferiores a 19 solo desencadenarán alertas si ha utilizado **sp_altermessage**, RAISERROR WITH LOG o **xp_logevent** para forzar que se escriban en el registro de la aplicación Windows.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
De forma predeterminada, solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_add_alert**.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Para crear una alerta con nivel de gravedad  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor donde desea crear una alerta con nivel de seguridad.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en **Alertas** y seleccione **Nueva alerta**.  
  
4.  En el cuadro de diálogo **Nueva alerta** , en el cuadro **Nombre** , escriba un nombre para esta alerta.  
  
5.  En la lista **Tipo** , seleccione **Alerta de evento de SQL Server**.  
  
6.  En **Definición de evento de alerta**, en la lista **Nombre de la base de datos** , seleccione una base de datos para restringir la alerta a una base de datos específica.  
  
7.  En **Las alertas se mostrarán en función de**, haga clic en **Gravedad** y seleccione la gravedad específica que generará la alerta.  
  
8.  Active la casilla correspondiente a **Mostrar alerta cuando el mensaje contenga** para restringir la alerta a una secuencia de caracteres en particular y, a continuación, escriba una palabra clave o una cadena de caracteres en el **Texto del mensaje**. El número máximo de caracteres es 100.  
  
9. Haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Para crear una alerta con nivel de gravedad  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Adds an alert (Test Alert) that notifies the
    -- Alert Operator via email when an error with a 
    -- severity of 23 is detected.
    
    -- Assumes that the Alert Operator already exists 
    -- and that database mail is configured.
    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert @name=N'Test Alert', 
      @message_id = 0, 
      @severity = 23, 
      @enabled = 1, 
      @include_event_description_in = 1
    ;
    GO
    
    EXEC dbo.sp_add_notification @alert_name=N'Test Alert',
      @operator_name=N'Alert Operator',
      @notification_method=1
    ;
    GO

    ```  
  
Para más información, consulte [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09).  
  
