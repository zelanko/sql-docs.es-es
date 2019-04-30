---
title: Cambiar los detalles de la programación de un trabajo maestro del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: f5414451-4d8e-464b-bd9e-f2b70c6899b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f9e53c4ae42f981b1b579294954a965ef8c376
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140690"
---
# <a name="change-the-scheduling-details-for-a-sql-server-agent-master-job"></a>Cambiar los detalles de programación de un trabajo maestro del Agente SQL Server
  En este tema se describe cómo cambiar los detalles de la programación de una definición de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar los detalles de la programación de una definición de trabajo mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 No se puede destinar un trabajo principal del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a servidores locales y remotos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 A menos que sea miembro del rol fijo de servidor **sysadmin** , solo podrá modificar los trabajos de su propiedad. Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>Para cambiar los detalles de la programación de una definición de trabajo  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor que contiene el trabajo cuya programación desea modificar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Trabajos** .  
  
4.  Haga clic con el botón derecho en la programación que desea modificar y seleccione **Propiedades**.  
  
5.  En el **Job Properties -**_job_name_ cuadro de diálogo **seleccionar una página**, seleccione **programaciones**. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: Nuevo trabajo &#40;programa página&#41;](job-properties-new-job-schedules-page.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>Para cambiar los detalles de la programación de una definición de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- changes the enabled status of the NightlyJobs schedule to 0   
    -- and sets the owner to terrid.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_schedule  
        @name = 'NightlyJobs',  
        @enabled = 0,  
        @owner_login_name = 'terrid' ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_update_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql).  
  
  
