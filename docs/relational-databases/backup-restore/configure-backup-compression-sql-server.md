---
title: Configurar la compresión de copia de seguridad (SQL Server) | Microsoft Docs
description: En este artículo se describe cómo invalidar el valor predeterminado de nivel de servidor al crear una copia de seguridad única o programar una serie de copias de seguridad rutinarias en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 430905eb-d218-458c-bd48-aeee6fbb7446
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a97a4b529921ab61f0f5dce83a059f5e9129b9a9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748482"
---
# <a name="configure-backup-compression-sql-server"></a>Configurar la compresión de copia de seguridad (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En la instalación, la compresión de la copia de seguridad está deshabilitada de forma predeterminada. El comportamiento predeterminado para la compresión de la copia de seguridad lo define la opción de configuración de nivel de servidor **backup compression default** . No obstante, puede invalidar el valor predeterminado de nivel de servidor al crear una copia de seguridad única o programar una serie de copias de seguridad rutinarias. Para cambiar el valor predeterminado de nivel de servidor, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  
  
## <a name="override-the-backup-compression-default"></a>Invalidar el valor predeterminado de compresión de copia de seguridad  
 Puede cambiar el comportamiento de la compresión de copia de seguridad para una copia de seguridad individual, trabajo de copia de seguridad o configuración de trasvase de registros.  
  
-   **[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
     Para reemplazar el valor predeterminado de compresión de copia de seguridad de servidor al crear una copia de seguridad, use WITH NO_COMPRESSION o WITH COMPRESSION en la instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md).  
  
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
  
  
## <a name="see-also"></a>Consulte también  
 [Compresión de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)  
  
  
