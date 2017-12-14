---
title: Asignar alertas a un operador | Microsoft Docs
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
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b1d997f822ecf563c7550499e4e379e71cd6d15
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="assign-alerts-to-an-operator"></a>Assign Alerts to an Operator
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo asignar alertas del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a los operadores para que puedan recibir notificaciones sobre trabajos en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para asignar alertas a un operador, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] proporciona una sencilla forma gráfica de administrar todo el sistema de alertas. Se recomienda utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] para configurar la infraestructura de alertas.  
  
-   Para enviar una notificación como respuesta a una alerta, primero debe configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para el envío de correo. Para más información, consulte [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce).  
  
-   Si se produce algún error al enviar un mensaje de correo electrónico o una notificación por buscapersonas, el error se comunica en el registro de errores de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Solo los miembros del rol fijo de servidor **sysadmin** pueden asignar alertas a operadores.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-assign-alerts-to-an-operator"></a>Para asignar alertas a un operador  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el operador al que desea asignar una alerta.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Operadores** .  
  
4.  Haga clic con el botón derecho en el operador al que desea asignar una alerta y seleccione **Propiedades** y, luego, la página **Notificaciones**.  
  
5.  En el cuadro de diálogo**Propiedades** de *nombre_operador*, en **Seleccionar una página**,seleccione **Notificaciones**.  
  
6.  En **Ver las notificaciones enviadas a este usuario por**, seleccione **Alertas** para ver una lista de las alertas enviadas a este operador o seleccione **Trabajos** para ver una lista de los trabajos que envían notificaciones a este operador. Active una o varias de las siguientes casillas para definir el método de notificación de cada notificación según corresponda: **Correo electrónico**, **Buscapersonas**o **Net send**.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-assign-alerts-to-an-operator"></a>Para asignar alertas a un operador  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_notification (Transact-SQL)](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
