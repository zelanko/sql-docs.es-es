---
title: Solución de problemas de un registro de transacciones lleno 9002
ms.custom: seo-lt-2019
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ad8b68338987256f1c7fa01f1f0d56242cef6a7f
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056072"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Solucionar problemas de un registro de transacciones lleno (Error 9002 de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se tratan las posibles respuestas a un registro de transacciones lleno y se sugiere cómo evitar esta situación en el futuro. 
  
  Cuando el registro de transacciones se llena, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] genera un **error 9002**. El registro se puede llenar cuando la base de datos está en línea o en recuperación. Si el registro se llena cuando la base de datos está en línea, la base de datos seguirá en conexión, pero solo se puede leer y no actualizar. Si el registro se llena durante la recuperación, [!INCLUDE[ssDE](../../includes/ssde-md.md)] marca la base de datos como RESOURCE PENDING. En ambos casos, es necesaria la intervención del usuario para proporcionar espacio de registro.  
  
## <a name="responding-to-a-full-transaction-log"></a>Respuesta a un registro de transacciones lleno  
 La respuesta apropiada a un registro de transacciones lleno depende en parte de la condición o condiciones que han causado que el registro se llene. 
 
 Para descubrir qué impide el truncamiento del registro en un caso determinado, use las columnas **log_reuse_wait** y **log_reuse_wait_desc** de la vista de catálogo **sys.database**. Para obtener más información, vea [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md). Para obtener la descripción de los factores que pueden retrasar el truncamiento del registro, vea [Registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> **IMPORTANTE:**  
>  Si la base de datos estaba en recuperación cuando se produjo el error 9002, una vez resuelto el problema, recupere la base de datos mediante [ALTER DATABASE *nombre_de_base_de_datos* SET ONLINE](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 Las alternativas de respuesta ante un registro de transacciones lleno incluyen:  
  
-   Realizar copias de seguridad del registro.  
  
-   Liberar espacio en disco para que el registro pueda crecer automáticamente.  
  
-   Mover el archivo de registro a una unidad de disco con suficiente espacio.  
  
-   Aumentar el tamaño de un archivo de registro.  
  
-   Agregar un archivo de registro en un disco diferente.  
  
-   Terminar o eliminar una transacción de larga duración.  
  
 Estas alternativas se describen en las secciones siguientes. Elija la respuesta más apropiada para la situación.  
  
## <a name="back-up-the-log"></a>Crear copia de seguridad del registro  
 En el modelo de recuperación completa o en el optimizado para cargas masivas de registros, si no se ha realizado recientemente ninguna copia de seguridad del registro de transacciones, puede que la copia de seguridad sea la que evita el truncamiento del registro. Si nunca realizó una copia de seguridad del registro, **debe crear dos copias de seguridad de registros** para que [!INCLUDE[ssDE](../../includes/ssde-md.md)] pueda truncar el registro en el punto de la última copia de seguridad. El truncamiento del registro libera espacio para nuevas entradas del registro. Para evitar que el registro se vuelva a llenar, realice copias de seguridad con frecuencia.  
  
 **Para crear una copia de seguridad del registro de transacciones**  
  
> **IMPORTANTE**  
>  Si la base de datos está dañada, vea [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Liberar espacio en disco  
 Puede liberar espacio en la unidad de disco que contiene el archivo de registro de transacciones de la base de datos eliminando o desplazando otros archivos. La liberación de espacio de disco permite que el sistema de recuperación amplíe automáticamente el archivo de registro.  
  
### <a name="move-the-log-file-to-a-different-disk"></a>Mover el archivo de registro a otro disco  
 Si no puede liberar suficiente espacio en la unidad de disco que contiene el archivo de registro, considere la posibilidad de desplazarlo a otra unidad con suficiente espacio.  
  
> **IMPORTANTE:** Los archivos de registro no se deben almacenar en sistemas de archivo comprimidos.  
  
 **Mover un archivo de registro**  
  
-   [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>Aumentar el tamaño del archivo de registro  
 Si hay espacio disponible en el disco del registro, puede aumentar el tamaño del archivo de registro. El tamaño máximo de los archivos de registro es de dos terabytes (TB) por cada archivo.  
  
 **Aumentar el tamaño del archivo**  
  
 Si el crecimiento automático está deshabilitado, la base de datos está en línea y hay suficiente espacio en el disco, puede:  
  
-   Aumentar manualmente el tamaño del archivo para producir un solo incremento de tamaño.  
  
-   Habilitar el crecimiento automático utilizando la instrucción ALTER DATABASE para establecer un incremento de tamaño distinto de cero para la opción FILEGROWTH.  
  
> **NOTA** En cualquier caso, si se alcanzó el límite del tamaño actual, aumente el valor MAXSIZE.  
  
### <a name="add-a-log-file-on-a-different-disk"></a>Agregar un archivo de registro en otro disco  
 Agregue un nuevo archivo de registro a la base de datos en otro disco que tenga suficiente espacio mediante ALTER DATABASE <nombreDeBaseDeDatos> ADD LOG FILE.  
  
 **Agregar un archivo de registro**  
  
-   [Agregar archivos de datos o de registro a una base de datos](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>Completar o terminar una transacción de larga ejecución
### <a name="discovering-long-running-transactions"></a>Descubrir transacciones de ejecución prolongada
Una transacción de ejecución muy prolongada puede hacer que el registro de transacciones se llene. Para buscar las transacciones de ejecución prolongada, use una de las opciones siguientes:
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md).**
Esta vista de administración dinámica devuelve información sobre las transacciones en la base de datos. En una transacción de ejecución prolongada, las columnas de especial interés incluyen la hora de la primera entrada del registro [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md), el estado actual de la transacción [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)y el [número de flujo de registro (LSN)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) del registro inicial del registro de transacciones [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md).

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md).**
Esta instrucción permite identificar el Id. de usuario del propietario de la transacción, por lo que se puede realizar un seguimiento del origen de la misma para terminarla de forma más ordenada (confirmándola en lugar de revirtiéndola).

### <a name="kill-a-transaction"></a>Terminar una transacción
Hay veces en que simplemente tiene que finalizar el proceso; puede que tenga que usar la instrucción [KILL](../../t-sql/language-elements/kill-transact-sql.md) . Use esta instrucción con sumo cuidado, especialmente cuando se estén ejecutando procesos críticos que no desea terminar. Para más información, consulte [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)

## <a name="see-also"></a>Vea también  
[Artículo de soporte técnico de KB: Un registro de transacciones crece de manera inesperada o se llena en SQL Server](https://support.microsoft.com/kb/317375) [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Administrar el tamaño del archivo de registro de transacciones](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
