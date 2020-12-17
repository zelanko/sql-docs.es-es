---
description: Sondear servidores
title: Sondear servidores
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: f28cb7829046b27ad0579ce546373834d6199d02
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477016"
---
# <a name="poll-servers"></a>Sondear servidores
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance/docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Cuando se implementa la administración multiservidor, los servidores de destino se ponen en contacto periódicamente con el servidor maestro para cargar información sobre los trabajos que se han ejecutado y descargar nuevos trabajos. El proceso de ponerse en contacto con el servidor maestro se denomina *sondeo de servidor* y tiene lugar a *intervalos de sondeo* regulares.  
  
## <a name="polling-intervals"></a>Intervalos de sondeo  
El intervalo de sondeo (de manera predeterminada un minuto) controla la frecuencia con la que el servidor de destino se conecta al servidor maestro para descargar instrucciones y cargar los resultados de la ejecución de trabajos.  
  
Cuando un servidor de destino sondea el servidor maestro, lee las operaciones asignadas al servidor de destino en la tabla **sysdownloadlist** de la base de datos **msdb** . Estas operaciones controlan trabajos multiservidor y diversos aspectos del comportamiento del servidor de destino. Algunos ejemplos de operaciones son eliminar, insertar e iniciar trabajos, y actualizar el intervalo de sondeo de un servidor de destino.  
  
Las operaciones se exponen en la tabla **sysdownloadlist** de una de las siguientes formas:  
  
-   Explícitamente mediante el procedimiento almacenado **sp_post_msx_operation** .  
  
-   Implícitamente mediante otros procedimientos almacenados de trabajo.  
  
Si utiliza procedimientos almacenados de trabajo para modificar pasos de trabajos o programaciones de trabajos multiservidor, o bien Objetos de administración distribuida de SQL (SQL-DMO) para controlar trabajos multiservidor, utilice este comando después de modificar los pasos o las programaciones de un trabajo multiservidor:  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Utilice este comando para mantener sincronizados los servidores de destino con la definición del trabajo actual.  
  
Si usa los siguientes elementos, no es necesario publicar las operaciones explícitamente:  
  
-   Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para controlar trabajos multiservidor.  
  
-   Procedimientos almacenados de trabajo que no modifican pasos de trabajos ni programaciones de trabajos.  
  
**Para forzar que un servidor de destino sondee el servidor maestro**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
[Administrar eventos](../../ssms/agent/manage-events.md)  
