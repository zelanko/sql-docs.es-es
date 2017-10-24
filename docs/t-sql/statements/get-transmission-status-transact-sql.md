---
title: GET_TRANSMISSION_STATUS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATUS_TSQL
- TRANSMISSION
- TRANSMISSION_TSQL
- GET_TRANSMISSION_STATUS
- STATUS
- GET_TRANSMISSION_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], transmission status
- Service Broker errors, transmission status
- transmission status information
- status information [SQL Server], conversations
- GET_TRANSMISSION_STATUS statement
ms.assetid: 621805d5-49ed-4764-b3cb-2ae4a3bf797e
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6d5152cca3f4ddb1afe0d8042c84743c31abf9b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="gettransmissionstatus-transact-sql"></a>GET_TRANSMISSION_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el estado de la última transmisión de un lado de la conversación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GET_TRANSMISSION_STATUS ( conversation_handle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_id*  
 Es el identificador de conversación. Este parámetro es de tipo **uniqueidentifier**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nchar**  
  
## <a name="remarks"></a>Comentarios  
 Devuelve una cadena que describe el estado del último intento de transmisión de la conversación especificada. Devuelve una cadena vacía si el último intento de transmisión se realizó correctamente, si todavía no se ha realizado ningún intento de transmisión, o si la *conversation_handle* no existe.  
  
 La información devuelta por esta función es la misma que se muestra en la columna last_transmission_error de la vista de administración sys.transmission_queue. No obstante, esta función se puede utilizar para encontrar el estado de transmisión de conversaciones que actualmente no tienen mensajes en la cola de transmisión.  
  
> [!NOTE]  
>  GET_TRANSMISSION_STATUS no proporciona información de mensajes que no tienen un extremo de conversación en la instancia actual. Es decir, no hay información disponible de los mensajes que se reenvían.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se notifica el estado de transmisión de la conversación con el identificador de conversación `58ef1d2d-c405-42eb-a762-23ff320bddf0`.  
  
```  
SELECT Status =  
    GET_TRANSMISSION_STATUS('58ef1d2d-c405-42eb-a762-23ff320bddf0') ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
 ```
 Status  
 ------------------------------- 
 The Service Broker protocol transport is disabled or not configured.
 ```  
  
 En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está configurado para permitir que [!INCLUDE[ssSB](../../includes/sssb-md.md)] se comunique en la red.  
  
## <a name="see-also"></a>Vea también  
 [Sys.conversation_endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [Sys.transmission_queue &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  

