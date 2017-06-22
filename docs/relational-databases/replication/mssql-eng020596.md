---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5eae24c46d8a92eb3906ba83ebac735c1ee563a9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20596|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Solo '%1!' o los miembros de db_owner pueden quitar el agente anónimo.|  
  
## <a name="explanation"></a>Explicación  
 No tiene suficientes permisos para quitar el agente de la suscripción anónima. El inicio de sesión usado al llamar a [sp_dropanonymousagent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) debe ser un miembro del rol fijo de servidor **sysadmin** del distribuidor o del rol fijo de base de datos **db_owner** de la base de datos de distribución, o bien el usuario debe ser el que inició la primera ejecución del agente.  
  
## <a name="user-action"></a>Acción del usuario  
 Inicie sesión con las credenciales correctas y ejecute **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
