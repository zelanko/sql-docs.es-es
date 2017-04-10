---
title: "Copia de seguridad de la base de datos (p&#225;gina Opciones multimedia) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "swb.backupdatabase.mediaoptions.f1"
  - "sql13.swb.backupdatabase.mediaoptions.f1"
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Copia de seguridad de la base de datos (p&#225;gina Opciones multimedia)
  Utilice la página  **Opciones multimedia** del cuadro de diálogo **Copia de seguridad de base de datos** para ver o modificar las opciones multimedia de la base de datos.  
  
 **Para crear una copia de seguridad mediante SQL Server Management Studio**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Puede definir un plan de mantenimiento de base de datos para crear copias de seguridad. Para obtener más información, vea [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md) y [Usar el Asistente para planes de mantenimiento](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Cuando especifica una tarea de copia de seguridad con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [BACKUP](../../t-sql/statements/backup-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente si hace clic en el botón **Script** y, después, selecciona un destino para el script.  
  
## Opciones  
  
### Sobrescribir medios  
 Las opciones del panel **Sobrescribir medios** controlan la forma en que las copias de seguridad se escriben en los medios. Si seleccionó la dirección URL (Almacenamiento de Windows Azure) como el destino de la copia de seguridad en la página General del cuadro de diálogo Copia de seguridad de base de datos, las opciones de la sección Sobrescribir medios estarán deshabilitadas. Puede sobrescribir una copia de seguridad con la instrucción Transact-SQL **BACKUP TO URL.. WITH FORMAT**. Para más información, consulte [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
 Solo la opción **Hacer copia de seguridad en un nuevo medio y borrar todos los conjuntos de copia de seguridad existentes** se admite con las opciones de cifrado. Si selecciona las opciones de la sección **Hacer copia de seguridad en un medio existente** , las opciones de cifrado en la página **Opciones de copia de seguridad** se deshabilitarán.  
  
> [!NOTE]  
>  Para obtener más información sobre los conjuntos de medios, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 **Hacer copia de seguridad en el conjunto de medios existente**  
 Realiza una copia de seguridad de una base de datos en un conjunto de medios existente. Si se selecciona este botón de opción, se activan tres opciones.  
  
 Elija una de las opciones siguientes:  
  
 **Anexar al conjunto de copia de seguridad existente**  
 Anexa el conjunto de copias de seguridad al conjunto de medios existente, manteniendo las copias de seguridad anteriores.  
  
 **Sobrescribir todos los conjuntos de copia de seguridad existentes**  
 Reemplaza las copias de seguridad anteriores del conjunto de medios existente por la copia de seguridad actual.  
  
 **Comprobar nombre de conjunto de medios y fecha de expiración de conjunto de copia**  
 Opcionalmente, si se realiza una copia de seguridad en un conjunto de medios existente, solicite que la operación de copia de seguridad compruebe el nombre y la fecha de expiración de los conjuntos de copia de seguridad.  
  
 **Nombre del conjunto de medios**  
 Si la opción **Comprobar nombre de conjunto de medios y fecha de expiración de conjunto de copia de seguridad** está seleccionada, de forma opcional, especifique el nombre del conjunto de medios establecido para usarse para la operación de copia de seguridad.  
  
 **Hacer copia de seguridad en un nuevo conjunto de medios y borrar todos los conjuntos de copia de seguridad existentes**  
 Se utiliza un conjunto de medios nuevo y se borran los conjuntos de copia de seguridad anteriores.  
  
 Si hace clic en esta opción, se activan las opciones siguientes:  
  
 **Nuevo nombre del conjunto de medios**  
 Opcionalmente, escriba un nombre nuevo para el conjunto de medios.  
  
 **Nueva descripción del conjunto de medios**  
 Opcionalmente, escriba una descripción significativa del conjunto de medios nuevo. Esta descripción debe ser muy específica para poder comunicar el contenido con precisión.  
  
### Confiabilidad  
 Las opciones del panel **Registro de transacciones** controlan la administración de errores mediante la operación de copia de seguridad.  
  
 **Comprobar copia de seguridad al finalizar**  
 Comprueba que el conjunto de copias de seguridad está completo y que todos los volúmenes son legibles.  
  
 **Realizar suma de comprobación antes de escribir en los medios**  
 Comprueba las sumas de comprobación antes de escribir en los medios de copia de seguridad. Seleccionar esta opción equivale a especificar la opción CHECKSUM en la instrucción BACKUP de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si se selecciona esta opción, es posible que aumente la carga de trabajo y que disminuya el rendimiento de la copia de seguridad de la operación de copia de seguridad. Para obtener más información sobre las sumas de comprobación de copias de seguridad, vea [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 **Continuar después de un error**  
 La operación de copia de seguridad debe continuar, aunque se detecten uno o varios errores.  
  
### Registro de transacciones  
 Las opciones del panel **Registro de transacciones** controlan el comportamiento de una copia de seguridad del registro de transacciones. Estas opciones solo son relevantes en el modelo de recuperación completa o en el modelo de recuperación optimizado para cargas masivas de registros. Se activan solo si se seleccionó **Registro de transacciones** en el campo **Tipo de copia de seguridad** de la página [General](../../relational-databases/backup-restore/back-up-database-general-page.md) del cuadro de diálogo **Copia de seguridad de base de datos** .  
  
> [!NOTE]  
>  Para obtener más información sobre las copias de seguridad del registro de transacciones, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 **Truncar el registro de transacciones**  
 Realice una copia de seguridad del registro de transacciones y trúnquelo para liberar espacio de registro. La base de datos permanece en línea. Esta es la opción predeterminada.  
  
 **Realizar copia de seguridad del final del registro y dejar la base de datos en estado de restauración**  
 Realice una copia de seguridad del final del registro y deje la base de datos en estado de restauración. Esta opción crea una *copia del final del registro*, que realiza una copia de seguridad de los registros de los que todavía no se ha realizado ninguna (registro activo), generalmente, para la preparación de la restauración de una base de datos. La base de datos no estará disponible para los usuarios hasta que haya finalizado su restauración.  
  
 Seleccionar esta opción es equivalente a especificar WITH NO_TRUNCATE, NORECOVERY en una instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]). Para obtener más información, vea [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### Unidad de cinta  
 Las opciones del panel **Unidad de cinta** controlan la administración de cintas durante la operación de copia de seguridad. Se activan solo si se seleccionó **Cinta** en el panel **Destino** de la página [General](../../relational-databases/backup-restore/back-up-database-general-page.md) del cuadro de diálogo **Copia de seguridad de base de datos** .  
  
> [!NOTE]  
>  Para obtener más información sobre cómo usar dispositivos de cinta, vea [Dispositivos de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Descargar la cinta después de realizar la copia de seguridad**  
 Una vez finalizada la copia de seguridad, descargue la cinta.  
  
 **Rebobinar la cinta antes de descargar**  
 Antes de descargar la cinta, se libera y rebobina. Solo se habilitará si está seleccionada la opción **Descargar la cinta después de realizar la copia de seguridad** .  
  
## Vea también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  