---
title: "MSSQL_ENG003724 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG003724"
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG003724
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3724|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede %1! %2! '%3!' porque se está utilizando para la replicación.|  
  
## Explicación  
 Cuando se replican objetos en una base de datos, se marcan como replicados en la tabla del sistema **sysarticles** (para instantáneas y publicaciones transaccionales) o **sysmergearticles** (para publicaciones de mezcla). Si intenta quitar un objeto replicado, se produce este error.  
  
## Acción del usuario  
 Asegúrese de que el objeto de la base de datos no está replicado antes de intentar quitarlo. Por ejemplo:  
  
-   Si el error se produce en la base de datos de publicaciones, quite el artículo de la publicación antes de quitar el objeto. Para obtener más información, consulte [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Si el error se produce en la base de datos de suscripciones, quite la suscripción antes de quitar el objeto. Para obtener más información, consulte [suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md). En suscripciones de publicaciones transaccionales, es posible quitar la suscripción de un artículo individual en vez de toda la publicación. Para obtener más información, consulte [sp_dropsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Si este error se produce en una base de datos que no se replica, ejecute [sp_removedbreplication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para asegurarse de que los objetos de la base de datos no están marcados como replicados.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  