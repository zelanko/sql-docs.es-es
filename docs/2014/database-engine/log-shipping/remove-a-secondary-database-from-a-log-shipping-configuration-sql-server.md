---
title: Quitar una base de datos secundaria desde una configuración del trasvase de registros (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0849d4e10df746dd98e271bb3eb35696cb20337b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157845"
---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>Quitar una base de datos secundaria desde una configuración del trasvase de registros (SQL Server)
  En este tema se describe cómo quitar una base de datos secundaria de trasvase de registros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para quitar una base de datos secundaria de trasvase de registros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Los procedimientos almacenados de trasvase de registros requieren que se pertenezca al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>Para quitar una base de datos secundaria de trasvase de registros  
  
1.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que sea actualmente el servidor principal de trasvase de registros y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos principal de trasvase de registros y, después, haga clic en **Propiedades**.  
  
3.  En **Seleccionar una página**, haga clic en **Trasvase de registro de transacciones**.  
  
4.  En **Instancias de servidores secundarios y bases de datos**, haga clic en la base de datos que desea quitar.  
  
5.  Haga clic en **Quitar**.  
  
6.  Haga clic en **Aceptar** para actualizar la configuración.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-remove-a-secondary-database"></a>Para quitar una base de datos secundaria  
  
1.  En el servidor principal, ejecute [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) para eliminar la información sobre la base de datos secundaria en el servidor principal.  
  
2.  En el servidor secundario, ejecute [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) para eliminar la base de datos secundaria.  
  
    > [!NOTE]  
    >  Si no hay ninguna otra base de datos secundaria con el mismo identificador secundario, se invoca **sp_delete_log_shipping_secondary_primary** desde **sp_delete_log_shipping_secondary_database** y elimina la entrada del identificador secundario y los trabajos de copia y restauración.  
  
3.  En el servidor secundario, deshabilite los trabajos de copia y restauración. Para obtener más información, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Actualizar el trasvase de registros a SQL Server 2014 &#40;Transact-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar el trasvase de registros &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [Agregar una base de datos secundaria a la configuración de trasvase de registros &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Quitar el trasvase de registros &#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [Ver el informe de trasvase de registros &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [Supervisar el trasvase de registros &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Tablas y procedimientos almacenados de trasvase de registros](log-shipping-tables-and-stored-procedures.md)  
  
  
