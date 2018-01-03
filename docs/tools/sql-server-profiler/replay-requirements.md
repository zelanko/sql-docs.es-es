---
title: "Requisitos de reproducción | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event classes [SQL Server], replaying traces
- traces [SQL Server], replaying
- replaying traces
- TSQL_Replay template [SQL Server]
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d76f9ac6450ffd473b91831416a26f6f313ccad7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="replay-requirements"></a>Replay Requirements
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Para reproducir los datos de seguimiento con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o Distributed Replay Utility, un conjunto específico de clases de eventos y columnas se deben capturar en el seguimiento. Esta configuración se habilita de forma predeterminada si se usa la plantilla de seguimiento **TSQL_Replay** para configurar un seguimiento que se usará posteriormente para la reproducción. En este tema se describe esta configuración y otros requisitos de reproducción.  
  
> [!NOTE]  
>  Recomendamos usar la Utilidad de reproducción distribuida para reproducir una aplicación de OLTP que se use mucho (con muchas conexiones simultáneas activas o un alto rendimiento). La utilidad puede reproducir datos de seguimiento desde varios equipos, simulando mejor una carga de trabajo esencial. Para obtener más información, vea [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="event-classes-required-for-replay"></a>Clases de eventos requeridos para reproducción  
 Para que [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]los reproduzca, se deben capturar el siguiente conjunto de clases de eventos y cualquier otra clase de eventos que desee supervisar en el seguimiento:  
  
-   **CursorClose**(solo cuando se reproduzcan cursores en el servidor)  
  
-   **CursorExecute** (solo cuando se reproduzcan cursores en el servidor)  
  
-   **CursorOpen** (solo cuando se reproduzcan cursores en el servidor)  
  
-   **CursorPrepare** (solo cuando se reproduzcan cursores en el servidor)  
  
-   **CursorUnprepare** (solo cuando se reproduzcan cursores en el servidor)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (solo cuando se reproduzcan instrucciones SQL preparadas en el servidor)  
  
-   **Prepare SQL** (solo cuando se reproduzcan instrucciones SQL preparadas en el servidor)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>Columnas de datos requeridas para la reproducción  
 Además de otras columnas de datos que desee capturar, debe capturar las siguientes columnas de datos en un seguimiento para poder reproducirlas:  
  
-   **Clase de eventos**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **Application Name**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **Id. de base de datos**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **ServerName**  
  
-   **Binary Data**  
  
-   **SPID**  
  
-   **Start Time**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **Error**  
  
> [!NOTE]  
>  Use la plantilla de seguimiento **TSQL_Replay** para los seguimientos que capturen datos para su reproducción.  
  
## <a name="other-replay-requirements"></a>Otros requisitos de reproducción  
 En Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la reproducción comprueba la presencia de los eventos y las columnas obligatorios. Este cambio permite mejorar la precisión de la reproducción y elimina el trabajo de estimación de la reproducción de solución de problemas cuando faltan datos obligatorios. La reproducción devuelve un error y detiene la reproducción de un archivo cuando faltan datos obligatorios en un seguimiento.  
  
 Para reproducir un seguimiento en un servidor (destino) en el cual se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distinto del servidor del que se realiza el seguimiento originalmente (origen), asegúrese de que se cumplen los requisitos siguientes:  
  
-   Todos los inicios de sesión y usuarios contenidos en el seguimiento deben estar ya creados en el destino y en la misma base de datos que en el origen.  
  
-   Todos los inicios de sesión y usuarios del destino deben tener los mismos permisos que tenían en el origen.  
  
-   Todas las contraseñas de inicio de sesión deben ser las mismas que las del usuario que ejecute la reproducción.  
  
-   Los Id. de base de datos del destino deben ser los mismos que los del origen. Sin embargo, si no son los mismos, se puede realizar la coincidencia basándose en **DatabaseName** , si está presente en el seguimiento.  
  
-   La base de datos predeterminada para cada inicio de sesión contenido en el seguimiento debe estar establecida (en el destino) en la base de datos de destino respectiva del inicio de sesión. Por ejemplo, el seguimiento que se va a reproducir contiene actividad de inicio de sesión, **Fred**, en la base de datos **Fred_Db** del origen. Por tanto, en el destino, la base de datos predeterminada del inicio de sesión, **Fred**, debe estar establecida en la base de datos que coincida con **Fred_Db** (aunque el nombre de la base de datos sea diferente). Para establecer la base de datos predeterminada del inicio de sesión, use el procedimiento almacenado del sistema **sp_defaultdb** .  
  
 La reproducción de eventos asociados a inicios de sesión que faltan o que son incorrectos tendrá como resultado errores de reproducción, pero la operación de reproducción continuará.  
  
 Para obtener información acerca de los permisos necesarios para reproducir un seguimiento, vea [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="see-also"></a>Vea también  
 [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproducir un archivo de seguimiento &#40; Analizador de SQL Server &#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Referencia de clase de eventos SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
