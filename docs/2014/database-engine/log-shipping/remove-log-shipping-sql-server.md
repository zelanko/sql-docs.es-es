---
title: Quitar el trasvase de registros (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8f74727ab5978559e75cab4cd495cf6d200a356
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326225"
---
# <a name="remove-log-shipping-sql-server"></a>Quitar el trasvase de registros de (SQL Server)
  En este tema se describe cómo quitar el trasvase de registros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para quitar el trasvase de registros, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Los procedimientos almacenados de trasvase de registros requieren que se pertenezca al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-remove-log-shipping"></a>Para quitar el trasvase de registros  
  
1.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que sea actualmente el servidor principal de trasvase de registros y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos principal de trasvase de registros y, después, haga clic en **Propiedades**.  
  
3.  En **Seleccionar una página**, haga clic en **Trasvase de registro de transacciones**.  
  
4.  Desactive la casilla **Habilitar ésta como base de datos principal en una configuración de trasvase de registros** .  
  
5.  Haga clic en **Aceptar** para quitar el trasvase de registros de esta base de datos principal.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-remove-log-shipping"></a>Para quitar el trasvase de registros  
  
1.  En el servidor principal de trasvase de registros, ejecute [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) para eliminar la información sobre la base de datos secundaria en el servidor principal.  
  
2.  En el servidor secundario de trasvase de registros, ejecute [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) para eliminar la base de datos secundaria.  
  
    > [!NOTE]  
    >  Si no hay ninguna otra base de datos secundaria con el mismo identificador secundario, se invoca **sp_delete_log_shipping_secondary_primary** desde **sp_delete_log_shipping_secondary_database** y elimina la entrada del identificador secundario y los trabajos de copia y restauración.  
  
3.  En el servidor principal de trasvase de registros, ejecute **sp_delete_log_shipping_primary_database** para eliminar la información sobre la configuración de trasvase de registros en el servidor principal. Esto también se elimina el trabajo de copia de seguridad.  
  
4.  En el servidor principal de trasvase de registros, deshabilite el trabajo de copia de seguridad. Para obtener más información, consulte [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
5.  En el servidor secundario de trasvase de registros, deshabilite los trabajos de copia y restauración.  
  
6.  Opcionalmente, si ya utiliza la base de datos secundaria de trasvase de registros, puede eliminarla del servidor secundario.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Actualizar el trasvase de registros a SQL Server 2014 &#40;Transact-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Configurar el trasvase de registros &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [Agregar una base de datos secundaria a la configuración de trasvase de registros &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Quitar una base de datos secundaria desde una configuración de trasvase de registros &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Supervisar el trasvase de registros &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Tablas y procedimientos almacenados de trasvase de registros](log-shipping-tables-and-stored-procedures.md)  
  
  
