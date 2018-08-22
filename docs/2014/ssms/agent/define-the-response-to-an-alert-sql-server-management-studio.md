---
title: Definir la respuesta a una alerta (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ea3859dd3bc94d8d42c0ed1748091678b5b70f4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394957"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>Definir la respuesta a una alerta (SQL Server Management Studio)
  En este tema se describe cómo definir el modo en que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] responde a las alertas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para definir la respuesta a una alerta, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las opciones Buscapersonas y **net send** se quitarán del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar estas características en los nuevos trabajos de programación y planee modificar las aplicaciones que actualmente las utilizan.  
  
-   Tenga en cuenta que deberá configurar el Agente SQL Server para que utilice el Correo electrónico de base de datos para enviar a los operadores notificaciones por correo electrónico o buscapersonas. Para obtener más información, vea el tema sobre [asignación de alertas a un operador](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden definir la respuesta a una alerta.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir la respuesta a una alerta  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la alerta en la que desea definir una respuesta.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Alertas** .  
  
4.  Haga clic con el botón derecho en la alerta en la que desea definir una respuesta y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo *Propiedades de la alerta***nombre_de_alerta*, en **Seleccionar una página**, seleccione **Respuesta**.  
  
6.  Active la casilla **Ejecutar trabajo** y, en la lista situada debajo de la casilla **Ejecutar trabajo** , seleccione el trabajo que se ejecutará cuando se produzca la alerta. Puede crear un nuevo trabajo haciendo clic en **Nuevo trabajo**. Puede ver más información acerca del trabajo haciendo clic en **View Job**. Para obtener más información sobre las opciones disponibles en los cuadros de diálogo **Nuevo trabajo** y **Propiedades del trabajo***nombre_de_trabajo*, consulte [Crear un trabajo](create-a-job.md) y [Ver un trabajo](view-a-job.md).  
  
7.  Active la casilla **Notificar a los operadores** si desea notificar a los operadores cuándo se activará la alerta. En **Lista de operadores**, seleccione uno o más de los métodos siguientes para notificar al operador o a los operadores: **Correo electrónico**, **Buscapersonas**o **Net Send**. Puede crear un nuevo operador haciendo clic en **Nuevo operador**. Puede ver más información acerca de un operador haciendo clic en **Ver operador**. Para obtener más información acerca de las opciones disponibles en los cuadros de diálogo **Nuevo operador** y **Ver las propiedades del operador** , vea [Create an Operator](create-an-operator.md) y [View Information About an Operator](view-information-about-an-operator.md).  
  
8.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir la respuesta a una alerta  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that François Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_add_notification &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
  
