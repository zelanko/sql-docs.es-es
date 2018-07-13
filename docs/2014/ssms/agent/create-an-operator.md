---
title: Crear un operador | Microsoft Docs
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
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 155bd9cf304e258b51bbb577c9c8be336f5b9bec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148366"
---
# <a name="create-an-operator"></a>Crear un operador
  En este tema se describe cómo configurar un usuario para que reciba notificaciones acerca de los trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un operador, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las opciones Buscapersonas y **net send** se quitarán del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar estas características en los nuevos trabajos de programación y planee modificar las aplicaciones que actualmente las utilizan.  
  
-   Tenga en cuenta que deberá configurar el Agente SQL Server para que utilice el Correo electrónico de base de datos para enviar a los operadores notificaciones por correo electrónico o buscapersonas. Para obtener más información, vea el tema sobre [asignación de alertas a un operador](http://msdn.microsoft.com/library/ms190038.aspx).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece un método gráfico sencillo para administrar trabajos y es el método recomendado para crear y administrar la infraestructura de trabajo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden crear operadores.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>Para crear un operador  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea crear un operador del Agente SQL Server.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Operadores** y, luego, seleccione **Nuevo operador**.  
  
     Las siguientes opciones están disponibles en la página **General** del cuadro de diálogo **Nuevo operador** :  
  
     **Nombre**  
     Cambie el nombre del operador.  
  
     **Enabled**  
     Habilite el operador. Si no se hablita, no se le envía ninguna notificación.  
  
     **Nombre de correo electrónico**  
     Especifica la dirección de correo electrónico del operador.  
  
     **Dirección de NET SEND**  
     Especifique la dirección que se va a usar para **net send**.  
  
     **Correo electrónico del buscapersonas**  
     Especifica la dirección de correo electrónico que debe utilizarse para el buscapersonas del operador.  
  
     **Programación de buscapersonas en servicio**  
     Establece las horas a las que el buscapersonas está activo.  
  
     **Lunes - Viernes**  
     Seleccione los días en los que el buscapersonas está activo.  
  
     **Inicio del día laborable**  
     Seleccione la hora del día a partir de la cual el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía mensajes al buscapersonas.  
  
     **Fin del día laborable**  
     Seleccione la hora del día a partir de la cual el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deja de enviar mensajes al buscapersonas.  
  
     Las siguientes opciones están disponibles en la página **Notificaciones** del cuadro de diálogo **Nuevo operador** :  
  
     **Alertas**  
     Muestra las alertas de la instancia.  
  
     **Jobs**  
     Muestra los trabajos de la instancia.  
  
     **Lista de alertas**  
     Enumera las alertas de la instancia.  
  
     **Lista de trabajos**  
     Enumera los trabajos de la instancia.  
  
     **Correo electrónico**  
     Envía la notificación al operador por correo electrónico.  
  
     **Buscapersonas**  
     Envía la notificación al operador mediante un mensaje de correo electrónico a la dirección del buscapersonas.  
  
     **Net send**  
     Notifique a este operador con **net send**.  
  
4.  Cuando termine de crear el nuevo operador, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-an-operator"></a>Para crear un operador  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- sets up the operator information for user 'danwi.' The operator is enabled.   
    -- SQL Server Agent sends notifications by pager from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_add_operator &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-operator-transact-sql).  
  
  
