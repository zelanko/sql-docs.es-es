---
title: "Cambiar los roles entre el servidor de trasvase de registros primario y secundario (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "trasvase de registros [SQL Server], cambios de rol"
  - "archivos de datos secundarios [SQL Server], roles cambiados entre"
  - "bases de datos principales [SQL Server]"
  - "cambios de rol inicial [SQL Server]"
  - "trasvase de registros [SQL Server], conmutación por error"
  - "conmutación por error [SQL Server], trasvase de registros"
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
caps.latest.revision: 20
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 20
---
# Cambiar los roles entre el servidor de trasvase de registros primario y secundario (SQL Server)
  Después de haber realizado la conmutación por error de una configuración de trasvase de registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un servidor secundario, puede configurar la base de datos secundaria para que actúe como base de datos principal. De este modo, podrá intercambiar la base de datos primaria y la secundaria cuando sea necesario.  
  
## Realizar el cambio de rol inicial  
 La primera vez que desee conmutar por error a una base de datos secundaria para convertirla en su nueva base de datos principal, debe realizar una serie de pasos. Una vez realizados, podrá intercambiar fácilmente los roles entre la base de datos principal y la base de datos secundaria.  
  
1.  Realice manualmente la conmutación por error de la base de datos principal a la secundaria. Asegúrese de realizar una copia de seguridad del registro de transacciones activo en su servidor principal mediante NORECOVERY. Para obtener más información, vea [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md).  
  
2.  Deshabilite el trabajo de copia de seguridad de trasvase de registros en el servidor principal, así como los trabajos de copia y restauración en el servidor secundario original.  
  
3.  En la base de datos secundaria (la que desea convertir en principal), configure el trasvase de registros mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Configurar el trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md). Siga estos pasos:  
  
    1.  Utilice el mismo recurso compartido para crear copias de seguridad que el utilizado para el servidor principal original.  
  
    2.  Cuando agregue la base de datos secundaria, en el cuadro de diálogo **Configuración de base de datos secundaria** , escriba el nombre de la base de datos principal original en el cuadro **Base de datos secundaria** .  
  
    3.  En el cuadro de diálogo **Configuración de base de datos secundaria** , seleccione **No, la base de datos secundaria está inicializada**.  
  
4.  Si la supervisión del trasvase de registros estaba habilitada en la anterior configuración de trasvase de registros, vuelva a configurarla para supervisar la nueva configuración de trasvase de registros.  Ejecute los siguientes comandos, y reemplace *database_name* por el nombre de la base de datos:  
  
    1.  **En el nuevo servidor principal**  
  
         Ejecute las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes:  
  
        ```  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
    2.  **En el nuevo servidor secundario**  
  
         Ejecute las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes:  
  
        ```  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
## Intercambiar roles  
 Una vez realizados los pasos anteriores para realizar el cambio inicial de roles, ya puede cambiar los roles entre la base de datos principal y la secundaria. A tal efecto, siga los pasos descritos a continuación. Para realizar el cambio de un rol, realice estos pasos generales:  
  
1.  Conecte en línea la base de datos secundaria y realice una copia de seguridad del registro de transacciones en el servidor principal mediante NORECOVERY.  
  
2.  Deshabilite el trabajo de copia de seguridad de trasvase de registros en el servidor principal, así como los trabajos de copia y restauración en el servidor secundario original.  
  
3.  Habilite el trabajo de copia de seguridad de trasvase de registros en el servidor secundario (el nuevo servidor principal), así como los trabajos de copia y restauración en el servidor primario (el nuevo servidor secundario).  
  
> [!IMPORTANT]  
>  Al cambiar una base de datos secundaria a la base de datos principal, para proporcionar una experiencia coherente a los usuarios y las aplicaciones, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos; por ejemplo los inicios de sesión y los trabajos, en la nueva instancia del servidor principal. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Administración de inicios de sesión y trabajos tras la conmutación de roles &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## Vea también  
 [Tablas y procedimientos almacenados de trasvase de registros](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  