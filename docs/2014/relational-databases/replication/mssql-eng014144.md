---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0d93f06a585bcc01c52438ff7b99bbd635532402
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049219"
---
# <a name="mssql_eng014144"></a>MSSQL_ENG014144
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|14144|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se puede quitar el suscriptor '%s'. Mantiene suscripciones en la base de datos de publicación '%2!'.|  
  
## <a name="explanation"></a>Explicación  
 Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha sido configurada como suscriptor no puede quitarse del rol de suscriptor mientras haya suscripciones activas configuradas para la instancia.  
  
## <a name="user-action"></a>Acción del usuario  
 Quite todas las suscripciones asociadas antes de intentar cambiar el estado del suscriptor de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
1.  Para buscar suscripciones, ejecute [sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) en la base de datos de publicación del publicador.  
  
2.  Para quitar suscripciones, ejecute [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql) en la base de datos de publicación.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
