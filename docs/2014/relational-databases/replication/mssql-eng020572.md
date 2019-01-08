---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 243b9b1658e2a0b34626e973799127b19ddc0e11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52806747"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20572|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Se ha reinicializado la suscripción del suscriptor '%s' al artículo '%s' en la publicación '%s' porque no pasó la validación.|  
  
## <a name="explanation"></a>Explicación  
 Los datos del suscriptor se validaron con los datos del publicador y no coinciden, por lo que se ha generado un error en la validación. Cuando especificó que la validación se debería realizar, seleccionó la opción de que se debería reinicializar una suscripción si se generaba un error en la validación. La reinicialización de una suscripción implica la aplicación de una instantánea nueva en el suscriptor. Para obtener más información acerca de la validación, consulte [Validate Replicated Data](validate-replicated-data.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Los datos del publicador y el suscriptor coincidirán después de aplicar una nueva instantánea en el suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
