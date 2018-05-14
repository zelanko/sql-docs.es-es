---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 531a4df4ea6212090129b4ed8d172c16f2cfc11e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mssqleng014157"></a>MSSQL_ENG014157
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14157|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La suscripción creada por el suscriptor '%1!s!' a la publicación '%2!s!' expiró y ha sido eliminada.|  
  
## <a name="explanation"></a>Explicación  
 Un suscriptor debe sincronizarse con el publicador en el tiempo especificado en el período de conservación de la publicación. Si un suscriptor no se sincroniza en este período, la suscripción expira. Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="user-action"></a>Acción del usuario  
 La suscripción se debe volver a crear e inicializar para que el suscriptor pueda empezar a recibir cambios de datos de nuevo:  
  
-   Para obtener información sobre la creación de suscripciones, vea [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Para obtener información sobre la inicialización de suscripciones, vea [Initialize a Subscription](../../relational-databases/replication/initialize-a-subscription.md) (Inicializar una suscripción).  
  
 Si la base de datos de suscripciones contiene varios cambios que no se han sincronizado con el publicador, puede usar la [tablediff Utility](../../tools/tablediff-utility.md) para determinar qué filas de las bases de datos de publicaciones y suscripciones son diferentes.  
  
 Puede aumentar el período de conservación de la publicación para evitar tener suscripciones expiradas. Tenga cuidado al establecer un valor alto porque puede provocar que se almacenen más datos y metadatos, lo que afectaría al rendimiento. Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="see-also"></a>Ver también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
