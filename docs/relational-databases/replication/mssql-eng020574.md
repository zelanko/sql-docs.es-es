---
title: MSSQL_ENG020574 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d59d9f277c027b0c10f578016348062de32aa47d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288057"
---
# <a name="mssql_eng020574"></a>MSSQL_ENG020574
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|20574|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La suscripción del suscriptor '%s' al artículo '%s' en la publicación '%s' no pasó la validación de datos.|  
  
## <a name="explanation"></a>Explicación  
 Los datos del suscriptor se validaron con los datos del publicador y no coinciden, por lo que se ha generado un error en la validación. Para obtener más información acerca de la validación, consulte [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Se recomienda hacer lo siguiente:  
  
-   Determine el motivo por el que se ha producido un error en la validación.  
  
-   Corrija el problema subyacente que ha causado el error.  
  
-   Establezca la convergencia de los datos reinicializando la suscripción o mediante otro método.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
