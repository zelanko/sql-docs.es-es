---
title: MSSQL_ENG014120 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1c527572f790e03e576b83f212e3915406c87bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mssqleng014120"></a>MSSQL_ENG014120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14120|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo quitar la base de datos de distribución '%s'. Esta base de datos está asociada a un publicador.|  
  
## <a name="explanation"></a>Explicación  
 La base de datos de distribución almacena metadatos y datos del historial de todos los tipos de replicación y transacciones para la replicación transaccional. Este error se produce si intenta quitar una base de datos de distribución que está asociada a uno o más publicadores.  
  
## <a name="user-action"></a>Acción del usuario  
 Para quitar una base de datos de distribución, primero debe quitar la asociación entre el distribuidor y el publicador. Para obtener más información, vea [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
