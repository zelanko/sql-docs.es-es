---
title: Escalabilidad | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a4891c57-56bb-49f4-9bb5-f11b745279e5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1768c9db30f01b6c5cd0350614e2f3c3dc579acb
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="scalability"></a>Escalabilidad
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQL Server 2016 contiene mejoras de escalabilidad en el almacenamiento en disco para las tablas optimizadas para memoria.  
  
-   
            **Varios subprocesos para conservar las tablas optimizadas para memoria**  
  
     En la versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], había un subproceso de punto de control único sin conexión que examinaba los cambios del registro de transacciones de las tablas optimizadas para memoria y los conservaba en archivos de punto de control (como archivos delta y de datos). Con mayor número de NÚCLEOS, el subproceso de punto de control único sin conexión podría retrasarse.  
  
     En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], hay varios subprocesos simultáneos responsables de conservar los cambios en tablas optimizadas para memoria.  
  
-   **Recuperación multiproceso**  
  
     En la versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la aplicación del registro como parte de la operación de recuperación era de un solo subproceso. En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], la aplicación del registro es multiproceso.  
  
-   **Operación de COMBINACIÓN**  
  
     La operación de COMBINACIÓN ahora es multiproceso.  
  
-   **Vistas de administración dinámica**  
  
     [sys.dm_db_xtp_checkpoint_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md) y [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) han cambiado de forma significativa.  
  
 Se ha deshabilitado la Combinación manual como combinación multiproceso con la intención de soportar la carga.  
  
 El motor OLTP en memoria continúa utilizando el grupo de archivos optimizados para memoria basado en el grupo de archivos FILESTREAM, pero los archivos individuales se desacoplan de FILESTREAM. Estos archivos están totalmente administrados (como para creación, anulación y recolección de elementos no utilizados) por el motor OLTP en memoria. [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) no se admite.  
  
  
