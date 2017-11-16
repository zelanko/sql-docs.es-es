---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d97300f400557643da18e81201136649d629b681
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3724|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede %1! %2! '%3!' porque se está utilizando para la replicación.|  
  
## <a name="explanation"></a>Explicación  
 Cuando se replican objetos en una base de datos, se marcan como replicados en la tabla del sistema **sysarticles** (en publicaciones de instantáneas y transaccionales) o **sysmergearticles** (en publicaciones de combinación). Si intenta quitar un objeto replicado, se produce este error.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de que el objeto de la base de datos no está replicado antes de intentar quitarlo. Por ejemplo:  
  
-   Si el error se produce en la base de datos de publicaciones, quite el artículo de la publicación antes de quitar el objeto. Para obtener más información, vea [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Si el error se produce en la base de datos de suscripciones, quite la suscripción antes de quitar el objeto. Para obtener más información, vea [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md). En suscripciones de publicaciones transaccionales, es posible quitar la suscripción de un artículo individual en vez de toda la publicación. Para obtener más información, vea [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Si se produce este error en una base de datos que no está replicada, ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para asegurarse de que los objetos de la base de datos no están marcados como replicados.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

