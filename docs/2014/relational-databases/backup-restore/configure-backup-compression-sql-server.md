---
title: Configurar la compresión de copia de seguridad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 394b0f6016cd0820142f958fba0ea69cb2db9a7d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106116"
---
# <a name="configure-backup-compression-sql-server"></a>Configurar la compresión de copia de seguridad (SQL Server)
  En la instalación, la compresión de la copia de seguridad está deshabilitada de forma predeterminada. El comportamiento predeterminado para la compresión de la copia de seguridad lo define la opción de configuración de nivel de servidor **backup compression default** . No obstante, puede invalidar el valor predeterminado de nivel de servidor al crear una copia de seguridad única o programar una serie de copias de seguridad rutinarias. Para cambiar el valor predeterminado de nivel de servidor, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Invalidar el valor predeterminado de compresión de copia de seguridad  
 Puede cambiar el comportamiento de la compresión de copia de seguridad para una copia de seguridad individual, trabajo de copia de seguridad o configuración de trasvase de registros.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Para invalidar el valor predeterminado de compresión de copia de seguridad de servidor al crear una copia de seguridad, use WITH NO_COMPRESSION o WITH COMPRESSION en la instrucción [BACKUP](/sql/t-sql/statements/backup-transact-sql).  
  
     En una configuración de trasvase de registros, puede controlar el comportamiento de la compresión de copia de seguridad de las copias de seguridad de registros mediante [sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)[sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql).  
  
-   **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
     Para obtener más información sobre cómo ver o configurar la opción predeterminada de compresión de copia de seguridad de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
     Puede invalidar el valor predeterminado de la compresión de copia de seguridad de servidor al crear una copia de seguridad si especifica **Comprimir copia de seguridad** o **No comprimir copia de seguridad** en cualquiera de los cuadros de diálogo siguientes:  
  
    -   [Copia de seguridad de base de datos (página Opciones)](back-up-database-backup-options-page.md)  
  
         Al hacer una copia de seguridad de una base de datos, puede controlar la compresión de copia de seguridad de una base de datos, archivo o registro.  
  
    -   [Usar el Asistente para planes de mantenimiento](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
         El Asistente para planes de mantenimiento le permite controlar la compresión de la copia de seguridad para cada copia de seguridad completa o diferencial de la base de datos o de registros programada.  
  
    -   [Tarea Copia de seguridad de la base de datos](../../integration-services/control-flow/back-up-database-task.md)de Integration Services (SSIS)  
  
         Puede controlar el comportamiento de la compresión de copia de seguridad al crear un paquete para hacer un copia de seguridad de una o varias bases de datos.  
  
    -   [Configuración de copias de seguridad de trasvase de registros de transacciones](../databases/log-shipping-transaction-log-backup-settings.md)  
  
         Puede controlar el comportamiento de compresión de las copias de seguridad de registros.  
  
  
## <a name="see-also"></a>Vea también  
 [Compresión de copia de seguridad &#40;SQL Server&#41;](backup-compression-sql-server.md)  
  
  
