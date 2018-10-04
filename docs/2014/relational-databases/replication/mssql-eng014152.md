---
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c94fbb3af4a1a8b21fbb498a6f0c50614bb688f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174925"
---
# <a name="mssqleng014152"></a>MSSQL_ENG014152
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14152|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Replicación-%s: el agente %s está programado para reintentar. %s|  
  
## <a name="explanation"></a>Explicación  
 Se ha programado el agente de replicación especificado para volver a intentar la operación solicitada. El proceso continúa intentándolo hasta que se alcanza la cantidad máxima configurada de reintentos del paso de trabajo.  
  
 Normalmente, un reintento tiene lugar debido a uno de los siguientes motivos:  
  
-   Se supera el valor **QueryTimeout** .  
  
-   Se supera el valor **LoginTimeout** .  
  
-   El proceso de replicación fue objeto del bloqueo.  
  
## <a name="user-action"></a>Acción del usuario  
 Si el mensaje de reintento no es frecuente, no es necesaria ninguna acción por parte del usuario.  
  
 Use [sp_help_jobstep](/sql/relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql) para ver la configuración actual de la cantidad máxima de reintentos del paso **Ejecutar agente** en el agente de replicación especificado. Puede utilizar el parámetro **@retry_attempts** del procedimiento almacenado [sp_update_jobstep](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) para ajustar la cantidad de reintentos de un paso de trabajo.  
  
 Si el mensaje de reintento se repite con frecuencia, solucione el problema al que se refiere el mensaje que está causando el reintento. Busque en el historial del agente los mensajes que indiquen los motivos por los que se tuvo que programar el reintento. En algunos casos tendrá que habilitar un registro más detallado para el agente de replicación. Para obtener más información acerca de la configuración del registro para replicación, vea el artículo [312292](http://support.microsoft.com/kb/312292)de Microsoft Knowledge Base.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
