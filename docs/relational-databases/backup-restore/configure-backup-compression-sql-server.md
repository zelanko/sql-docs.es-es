---
title: "Configurar la compresión de copia de seguridad (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 08c6e1ccb56a08309d2c904a8566884372dc3778
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="configure-backup-compression-sql-server"></a>Configurar la compresión de copia de seguridad (SQL Server)
  En la instalación, la compresión de la copia de seguridad está deshabilitada de forma predeterminada. El comportamiento predeterminado para la compresión de la copia de seguridad lo define la opción de configuración de nivel de servidor **backup compression default** . No obstante, puede invalidar el valor predeterminado de nivel de servidor al crear una copia de seguridad única o programar una serie de copias de seguridad rutinarias. Para cambiar el valor predeterminado de nivel de servidor, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Invalidar el valor predeterminado de compresión de copia de seguridad  
 Puede cambiar el comportamiento de la compresión de copia de seguridad para una copia de seguridad individual, trabajo de copia de seguridad o configuración de trasvase de registros.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Para invalidar el valor predeterminado de compresión de copia de seguridad de servidor al crear una copia de seguridad, use WITH NO_COMPRESSION o WITH COMPRESSION en la instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md).  
  
     En una configuración de trasvase de registros, puede controlar el comportamiento de la compresión de copia de seguridad de las copias de seguridad de registros mediante [sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Para obtener más información sobre cómo ver o configurar la opción predeterminada de compresión de copia de seguridad de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     Puede invalidar el valor predeterminado de la compresión de copia de seguridad de servidor al crear una copia de seguridad si especifica **Comprimir copia de seguridad** o **No comprimir copia de seguridad** en cualquiera de los cuadros de diálogo siguientes:  
  
    -   [Copia de seguridad de base de datos (página Opciones)](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)  
  
         Al hacer una copia de seguridad de una base de datos, puede controlar la compresión de copia de seguridad de una base de datos, archivo o registro.  
  
    -   [Usar el Asistente para planes de mantenimiento](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         El Asistente para planes de mantenimiento le permite controlar la compresión de la copia de seguridad para cada copia de seguridad completa o diferencial de la base de datos o de registros programada.  
  
    -   [Tarea Copia de seguridad de la base de datos](../../integration-services/control-flow/back-up-database-task.md)de Integration Services (SSIS)  
  
         Puede controlar el comportamiento de la compresión de copia de seguridad al crear un paquete para hacer un copia de seguridad de una o varias bases de datos.  
  
    -   [Configuración de copias de seguridad de trasvase de registros de transacciones](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)  
  
         Puede controlar el comportamiento de compresión de las copias de seguridad de registros.  
  
  
## <a name="see-also"></a>Vea también  
 [Compresión de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
