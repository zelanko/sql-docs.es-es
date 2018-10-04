---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f35215d5b5929c7a250f85b5aa8e7c1ea9c50ddc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132365"
---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14005|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo quitar la publicación. Hay una suscripción para ella.|  
  
## <a name="explanation"></a>Explicación  
 Ha intentado quitar una publicación que tiene asociadas una o varias suscripciones. Una publicación se puede quitar únicamente si no hay suscripciones asociadas.  
  
## <a name="user-action"></a>Acción del usuario  
 Quite las suscripciones antes de quitar la publicación. Si utiliza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para quitar la publicación, se le ofrecerá la opción de quitar automáticamente todas las suscripciones asociadas antes de quitar la publicación. Si utiliza procedimientos almacenados, primero debe quitar explícitamente las suscripciones. Para obtener más información, consulte [Delete a Push Subscription](delete-a-push-subscription.md) y [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
 Si parece no existir ninguna suscripción para la publicación o si ve este error cuando crea la publicación, es posible que tenga una suscripción anterior que no se limpiara completamente cuando se quitó. Ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) en la base de datos para eliminar todos los objetos y la configuración completa relacionados con la replicación.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
