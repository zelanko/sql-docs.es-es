---
description: MSSQL_ENG020574
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 86f4947b3779ca0b091db4ae372b5fcb70ad84a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484857"
---
# <a name="mssql_eng020574"></a>MSSQL_ENG020574
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|Atributo|Value|  
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
  
  
