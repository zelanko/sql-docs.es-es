---
title: Solucionar problemas de un registro de transacciones lleno (Error 9002 de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2c0dc1566693ad8d8c86d7efe47403248788b076
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759517"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Solucionar problemas de un registro de transacciones lleno (Error 9002 de SQL Server)
  En este tema se tratan las posibles respuestas a un registro de transacciones lleno y se sugiere cómo evitar esta situación en el futuro. Cuando el registro de transacciones se llena, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] genera un error 9002. El registro se puede llenar cuando la base de datos está en línea o en recuperación. Si el registro se llena cuando la base de datos está en línea, la base de datos seguirá en conexión, pero solo se puede leer y no actualizar. Si el registro se llena durante la recuperación, [!INCLUDE[ssDE](../../includes/ssde-md.md)] marca la base de datos como RESOURCE PENDING. En ambos casos, es necesaria la intervención del usuario para proporcionar espacio de registro.  
  
## <a name="responding-to-a-full-transaction-log"></a>Respuesta a un registro de transacciones lleno  
 La respuesta apropiada a un registro de transacciones lleno depende en parte de la condición o condiciones que han causado que el registro se llene. Para descubrir qué impide el truncamiento del registro en un caso determinado, use las columnas **log_reuse_wait** y **log_reuse_wait_desc** de la vista de catálogo **sys.database**. Para obtener más información, vea [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql). Para obtener la descripción de los factores que pueden retrasar el truncamiento del registro, vea [Registro de transacciones &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
> [!IMPORTANT]  
>  Si la base de datos estaba en recuperación cuando se produjo el error 9002, una vez resuelto el problema, recupere la base de datos mediante ALTER DATABASE *database_name* SET ONLINE.  
  
 Las alternativas de respuesta ante un registro de transacciones lleno incluyen:  
  
-   Realizar copias de seguridad del registro.  
  
-   Liberar espacio en disco para que el registro pueda crecer automáticamente.  
  
-   Mover el archivo de registro a una unidad de disco con suficiente espacio.  
  
-   Aumentar el tamaño de un archivo de registro.  
  
-   Agregar un archivo de registro en un disco diferente.  
  
-   Terminar o eliminar una transacción de larga duración.  
  
 Estas alternativas se describen en las secciones siguientes. Elija la respuesta más apropiada para la situación.  
  
### <a name="backing-up-the-log"></a>Realizar copias de seguridad del registro  
 En el modelo de recuperación completa o en el optimizado para cargas masivas de registros, si no se ha realizado recientemente ninguna copia de seguridad del registro de transacciones, puede que la copia de seguridad sea la que evita el truncamiento del registro. Si nunca se ha realizado una copia de seguridad del registro, debe crear dos copias de seguridad de registros para que [!INCLUDE[ssDE](../../includes/ssde-md.md)] pueda truncar el registro en el punto de la última copia de seguridad. El truncamiento del registro libera espacio para nuevas entradas del registro. Para evitar que el registro se vuelva a llenar, realice copias de seguridad con frecuencia.  
  
 **Para crear una copia de seguridad del registro de transacciones**  
  
> [!IMPORTANT]  
>  Si la base de datos está dañada, vea [Copias del final del registro &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md).  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Liberar espacio en disco  
 Puede liberar espacio en la unidad de disco que contiene el archivo de registro de transacciones de la base de datos eliminando o desplazando otros archivos. La liberación de espacio de disco permite que el sistema de recuperación amplíe automáticamente el archivo de registro.  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>Mover el archivo de registro a otro disco  
 Si no puede liberar suficiente espacio en la unidad de disco que contiene el archivo de registro, considere la posibilidad de desplazarlo a otra unidad con suficiente espacio.  
  
> [!IMPORTANT]  
>  Los archivos de registro no se deben almacenar en sistemas de archivo comprimidos.  
  
 **Para mover un archivo de registro**  
  
-   [Mover archivos de base de datos](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>Aumentar el tamaño de un archivo de registro  
 Si hay espacio disponible en el disco del registro, puede aumentar el tamaño del archivo de registro. El tamaño máximo de los archivos de registro es de dos terabytes (TB) por cada archivo.  
  
 **Para aumentar el tamaño de archivo**  
  
 Si el crecimiento automático está deshabilitado, la base de datos está en línea y hay suficiente espacio en el disco, puede:  
  
-   Aumentar manualmente el tamaño del archivo para producir un solo incremento de tamaño.  
  
-   Habilitar el crecimiento automático utilizando la instrucción ALTER DATABASE para establecer un incremento de tamaño distinto de cero para la opción FILEGROWTH.  
  
> [!NOTE]  
>  En cualquier caso, si se ha alcanzado el límite del tamaño actual, aumente el valor MAXSIZE.  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>Agregar un archivo de registro en otro disco  
 Agregue un nuevo archivo de registro a la base de datos en otro disco que tenga suficiente espacio mediante ALTER DATABASE <nombreDeBaseDeDatos> ADD LOG FILE.  
  
 **Para agregar un archivo de registro**  
  
-   [Agregar archivos de datos o de registro a una base de datos](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Administrar el tamaño del archivo de registro de transacciones](manage-the-size-of-the-transaction-log-file.md)   
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
