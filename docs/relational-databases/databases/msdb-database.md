---
title: Base de datos msdb | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f3eef98f3440c54c5cd55fc922322d444c39a6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="msdb-database"></a>Base de datos msdb
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El Agente **utiliza la base de datos** msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar alertas y trabajos. Otras características como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSB](../../includes/sssb-md.md)] y Correo electrónico de base de datos también usan esta base de datos.  
  
 Por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene automáticamente un historial en línea de copias de seguridad y restauración completo dentro de las tablas de la base de datos **msdb**. Esta información incluye el nombre del autor de la copia de seguridad, la hora en que se realizó y los dispositivos o archivos en que está almacenada. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa esta información para sugerir un plan para restaurar una base de datos y aplicar las copias de seguridad de los registros de transacciones. Los eventos de copia de seguridad de todas las bases de datos se registran, aunque se hayan creado con aplicaciones personalizadas o herramientas de terceros. Por ejemplo, si usa una aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que llama a los objetos de Objetos de administración de SQL Server (SMO) para realizar operaciones de copia de seguridad, el evento se registrará en las tablas del sistema **msdb** , el registro de aplicaciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows y el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para ayudar a proteger la información que está almacenada en **msdb**, recomendamos que considere colocar el registro de transacciones de **msdb** en un almacén tolerante a errores.  
  
 La base de datos **msdb** utiliza el modelo de recuperación simple de forma predeterminada. Si utiliza las tablas del [historial de copias de seguridad y restauración](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md) , recomendamos utilizar el modelo de recuperación completa para **msdb**. Para obtener más información, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md). Observe que, cuando se instala o se actualiza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , y siempre que se utilice Setup.exe para volver a generar las bases de datos del sistema, el modelo de recuperación de **msdb** se establece automáticamente en simple.  
  
> [!IMPORTANT]  
>  Después de cualquier operación que actualice **msdb**, como la copia de seguridad o la restauración de una base de datos, recomendamos hacer una copia de seguridad de **el msdb**. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="physical-properties-of-msdb"></a>Propiedades físicas de la base de datos msdb  
 En la siguiente tabla se enumeran los valores de configuración iniciales de los archivos de registro y datos de **msdb** . El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Crecimiento del archivo|  
|----------|------------------|-------------------|-----------------|  
|Datos principales|MSDBData|MSDBData.mdf|Crecimiento automático del 10 por ciento hasta llenar el disco.|  
|Log|MSDBLog|MSDBLog.ldf|Crecimiento automático del 10 por ciento hasta un máximo de 2 terabytes.|  
  
 Para mover la base de datos **msdb** o los archivos de registro, vea [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options"></a>Opciones de base de datos  
 En la siguiente tabla se enumera el valor predeterminado de cada opción de base de datos en la base de datos **msdb** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|no|  
|ANSI_NULL_DEFAULT|OFF|Sí|  
|ANSI_NULLS|OFF|Sí|  
|ANSI_PADDING|OFF|Sí|  
|ANSI_WARNINGS|OFF|Sí|  
|ARITHABORT|OFF|Sí|  
|AUTO_CLOSE|OFF|Sí|  
|AUTO_CREATE_STATISTICS|ON|Sí|  
|AUTO_SHRINK|OFF|Sí|  
|AUTO_UPDATE_STATISTICS|ON|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sí|  
|CHANGE_TRACKING|OFF|no|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sí|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|no<br /><br /> Sí<br /><br /> Sí|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sí|  
|DB_CHAINING|ON|Sí|  
|ENCRYPTION|OFF|no|  
|MIXED_PAGE_ALLOCATION|ON|no|  
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|Sí|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|ENABLE_BROKER|Sí|  
|TRUSTWORTHY|ON|Sí|  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Restrictions  
 Las siguientes operaciones no se pueden realizar en la base de datos **msdb** :  
  
-   Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
  
-   Eliminar la base de datos.  
  
-   Eliminar el usuario **guest** de la base de datos.  
  
-   Habilitar el mecanismo de captura de cambios en los datos.  
  
-   Participar en el reflejo de la base de datos.  
  
-   Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
  
-   Cambiar el nombre de la base de datos o del grupo de archivos principal.  
  
-   Establecer la base de datos en OFFLINE.  
  
-   Establecer el grupo de archivos principal en READ_ONLY.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)  
  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
