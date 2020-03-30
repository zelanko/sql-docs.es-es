---
title: MSSQL_ENG014144 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014144 error
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c43395fffe934756bb69e0d094a3e6637adcedad
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286512"
---
# <a name="mssql_eng014144"></a>MSSQL_ENG014144
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
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
  
1.  Para buscar suscripciones, ejecute [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) en la base de datos de publicación del publicador.  
  
2.  Para quitar suscripciones, ejecute [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) en la base de datos de publicación.  

## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
