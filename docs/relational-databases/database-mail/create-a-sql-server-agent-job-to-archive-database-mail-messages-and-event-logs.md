---
title: Creación de un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8396b30122a393ea3532113e261a908d8079432a
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228484"
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>Crear un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Las tablas **msdb** mantienen copias de los mensajes del Correo electrónico de base de datos y sus datos adjuntos, además del registro de eventos del Correo electrónico de base de datos. Puede reducir el tamaño de las tablas y eliminar los mensajes y eventos que ya no sean necesarios periódicamente. Los procedimientos siguientes permiten crear un trabajo del Agente SQL Server para automatizar el proceso.  
  
-   **Antes de empezar:**  , [Requisitos previos](#Prerequisites), [Recomendaciones](#Recommendations), [Permisos](#Permissions)  
  
-   **Para almacenar mensajes y los registros de Correo electrónico de base de datos mediante:**  [Agente SQL Server](#Process_Overview)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Las nuevas tablas para almacenar los datos del archivo se pueden ubicar en una base de datos de archivo especial. De forma alternativa, las filas se pudieron exportar a un archivo de texto.  
   
###  <a name="Recommendations"></a> Recomendaciones  
 En su entorno de producción, puede agregar otros procedimientos de comprobación de errores y enviar un mensaje de correo electrónico a los operadores si el trabajo provoca un error.  
  
  
###  <a name="Permissions"></a> Permisos  
 Debe ser miembro del rol fijo de servidor **sysadmin** para ejecutar los procedimientos almacenados que se describen en este tema.  
  
  
###  <a name="Process_Overview"></a> Información general acerca del proceso de inicialización  
  
-   En el primer procedimiento se crea con cuatro pasos un trabajo denominado Archivar mensajes del Correo electrónico de base de datos.  
  
    1.  Copiar todos los mensajes de las tablas del Correo electrónico de base de datos en una nueva tabla con el nombre del mes anterior en el formato **DBMailArchive_** _<año_mes>_ .  
  
    2.  Copiar todos los datos adjuntos relacionados con los mensajes copiados en el primer paso, de las tablas del Correo electrónico de base de datos en una nueva tabla con el nombre del mes anterior en el formato **DBMailArchive_Attachments_** _<año_mes>_ .  
  
    3.  Copiar todos los eventos del registro de eventos del Correo electrónico de base de datos relacionados con los mensajes copiados en el primer paso, de las tablas del Correo electrónico de base de datos en una nueva tabla con el nombre del mes anterior en el formato **DBMailArchive_Log_** _<año_mes>_ .  
  
    4.  Eliminar los registros de los elementos de correo transferidos de las tablas del Correo electrónico de base de datos.  
  
    5.  Eliminar los eventos relacionados con los elementos de correo transferidos del registro de eventos del Correo electrónico de base de datos.  
  
-   Programar el trabajo para ejecutar periódicamente.  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>Para crear un trabajo del Agente SQL Server  
  
1.  En el Explorador de objetos, expanda el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic con el botón derecho en **Trabajos**y, después, haga clic en **Nuevo trabajo**.  
  
2.  En el cuadro **Nombre** del cuadro de diálogo **Nuevo trabajo** , escriba **Archivar mensajes del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Propietario** , confirme que el propietario es miembro del rol fijo de servidor **sysadmin** .  
  
4.  En el cuadro **Categoría** , haga clic en **Mantenimiento de bases de datos**.  
  
5.  En el cuadro **Descripción** , escriba **Archivar mensajes del Correo electrónico de base de datos**y, a continuación, haga clic en **Pasos**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 [Información general](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>Crear un paso para archivar los mensajes del Correo electrónico de base de datos  
  
1.  En la página **Pasos** , haga clic en **Nuevo**.  
  
2.  En el cuadro **Nombre del paso** , escriba **Copiar elementos del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Tipo** , seleccione **Script Transact-SQL (T-SQL)** .  
  
4.  En el cuadro **Base de datos** , seleccione **msdb**.  
  
5.  En el cuadro **Comando** , escriba la instrucción siguiente para crear una tabla con el nombre del mes anterior y filas anteriores al inicio del mes actual:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Haga clic en **Aceptar** para guardar el paso.  
  
 [Información general](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>Crear un paso para archivar los datos adjuntos del Correo electrónico de base de datos  
  
1.  En la página **Pasos** , haga clic en **Nuevo**.  
  
2.  En el cuadro **Nombre del paso** , escriba **Copiar datos adjuntos del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Tipo** , seleccione **Script Transact-SQL (T-SQL)** .  
  
4.  En el cuadro **Base de datos** , seleccione **msdb**.  
  
5.  En el cuadro **Comando** , escriba la instrucción siguiente para crear una tabla de datos adjuntos con el nombre del mes anterior y los archivos adjuntos correspondientes a los mensajes transferidos en el paso anterior:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Haga clic en **Aceptar** para guardar el paso.  
  
 [Información general](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>Crear un paso para archivar el registro del Correo electrónico de base de datos  
  
1.  En la página **Pasos** , haga clic en **Nuevo**.  
  
2.  En el cuadro **Nombre del paso** , escriba **Copiar el registro del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Tipo** , seleccione **Script Transact-SQL (T-SQL)** .  
  
4.  En el cuadro **Base de datos** , seleccione **msdb**.  
  
5.  En el cuadro **Comando** , escriba la instrucción siguiente para crear una tabla de registros con el nombre del mes anterior y las entradas de registro correspondientes a los mensajes transferidos en el paso anterior:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Haga clic en **Aceptar** para guardar el paso.  
  
 [Información general](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>Crear un paso para quitar las filas archivadas del Correo electrónico de base de datos  
  
1.  En la página **Pasos** , haga clic en **Nuevo**.  
  
2.  En el cuadro **Nombre del paso** , escriba **Eliminar filas del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Tipo** , seleccione **Script Transact-SQL (T-SQL)** .  
  
4.  En el cuadro **Base de datos** , seleccione **msdb**.  
  
5.  En el cuadro **Comando** , escriba la instrucción siguiente para quitar las filas anteriores al mes actual de las tablas del Correo electrónico de base de datos:  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  Haga clic en **Aceptar** para guardar el paso.  
  
 [Información general](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>Crear un paso para quitar los elementos archivados del registro de eventos del Correo electrónico de base de datos  
  
1.  En la página **Pasos** , haga clic en **Nuevo**.  
  
2.  En el cuadro **Nombre del paso** , escriba **Eliminar filas del registro de eventos del Correo electrónico de base de datos**.  
  
3.  En el cuadro **Tipo** , seleccione **Script Transact-SQL (T-SQL)** .  
  
4.  En el cuadro **Comando** , escriba la instrucción siguiente para quitar las filas anteriores al mes actual del registro de eventos del Correo electrónico de base de datos:  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  Haga clic en **Aceptar** para guardar el paso.  
  
 [Información general](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>Para programar el trabajo para ejecutar periódicamente  
  
1.  En el cuadro de diálogo **Nuevo trabajo** , haga clic en **Programaciones**.  
  
2.  En la página **Programaciones** , haga clic en **Nuevo**.  
  
3.  En el cuadro **Nombre** , escriba **Archivar mensajes del Correo electrónico de base de datos**.  
  
4.  En el cuadro **Tipo de programación** , seleccione **Periódica**.  
  
5.  En el área **Frecuencia** , seleccione las opciones para ejecutar el trabajo periódicamente, por ejemplo una vez al mes.  
  
6.  En el área **Frecuencia diaria**, seleccione **Sucede una vez a las \<hora>** .  
  
7.  Compruebe que las demás opciones están configuradas tal como desea y, a continuación, haga clic en **Aceptar** para guardar la programación.  
  
8.  Haga clic en **Aceptar** para guardar el trabajo.  
  
 [Información general](#Process_Overview)  
  
  
