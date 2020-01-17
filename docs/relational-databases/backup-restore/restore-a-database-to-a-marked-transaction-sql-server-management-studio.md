---
title: Restauración de bases de datos en una transacción marcada (SSMS)
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1e71815c79e626a1cebb60c7d5d50fda1cce132d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245084"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>Restauración de bases de datos en una transacción marcada (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando una base de datos se encuentra en estado de restauración, puede usar el cuadro de diálogo **Restaurar registro de transacciones** para restaurar la base de datos a una transacción marcada en las copias de seguridad de registros disponibles.  
  
> [!NOTE]  
>  Para obtener más información, vea [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) y [Recuperación de bases de datos relacionadas que contienen transacciones marcadas](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
### <a name="to-restore-a-marked-transaction"></a>Para restaurar una transacción marcada  
  
1.  Después de conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Bases de datos**y, en función de la base de datos, seleccione la base de datos de un usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, después, haga clic en **Restaurar**.  
  
4.  Haga clic en **Registro de transacciones**para abrir el cuadro de diálogo **Restaurar registro de transacciones** .  
  
5.  En la página **General** , en la sección **Restaurar en** , seleccione **Transacción marcada**para abrir el cuadro de diálogo **Seleccionar transacción marcada** . Este cuadro de diálogo muestra una cuadrícula en la que aparecen las transacciones marcadas disponibles en las copias de seguridad de los registros de transacciones seleccionados.  
  
     De forma predeterminada, la restauración se realiza hasta la transacción marcada, sin incluirla. Para restaurar también la transacción marcada, seleccione **Incluir transacción marcada**.  
  
     En la tabla siguiente se muestran los encabezados de columna de la cuadrícula y se describen sus valores.  
  
    |Encabezado|Value|  
    |------------|-----------|  
    |\<blank>|Muestra una casilla para seleccionar la marca.|  
    |**Marca de transacción**|Nombre de la transacción marcada especificada por el usuario cuando se confirmó la transacción.|  
    |**Date**|Fecha y hora de confirmación de la transacción. La fecha y hora de la transacción se muestran tal como están registradas en la tabla **msdbgmarkhistory** , no en la fecha y hora del equipo cliente.|  
    |**Descripción**|Descripción de la transacción marcada especificada por el usuario al confirmar la transacción (si la hay).|  
    |**LSN**|Número de flujo de registro de la transacción marcada.|  
    |**Base de datos**|Nombre de la base de datos en la que se confirmó la transacción marcada.|  
    |**Nombre de usuario**|Nombre del usuario de la base de datos que confirmó la transacción marcada.|  
  
## <a name="see-also"></a>Consulte también  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
