---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9cdd464be0ae756faf3e66f8ac7e3cf8c1b63ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113795"
---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|27056|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El proceso de mezcla no pudo cambiar el historial de generación en '%1'. Para solucionar el problema, reinicie la sincronización con registro de historial detallado y especifique un archivo de salida para escribir en él.|  
  
## <a name="explanation"></a>Explicación  
 Este error suele ser el resultado de la contención de las tablas del sistema de replicación de mezcla, que han aumentado de tamaño de forma excesiva. El tamaño excesivo de las tablas del sistema se debe generalmente a un período prolongado de retención de la publicación, ya que los metadatos se deben almacenar en estas tablas hasta que se alcanza el período de retención.  
  
## <a name="user-action"></a>Acción del usuario  
 **Para solucionar el problema:**  
  
1.  Reduzca el valor de los parámetros -**DownloadGenerationsPerBatch** y **-UploadGenerationsPerBatch** del agente de mezcla para permitir que el procesamiento continúe mientras soluciona el problema subyacente que causa el error. Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para obtener más información, vea:  
  
    -   [Trabajar con perfiles del Agente de replicación](agents/replication-agent-profiles.md)  
  
    -   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md).  
  
2.  Especifique el menor valor posible para el período de retención de la publicación. Para más información, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
3.  Como parte del mantenimiento de la replicación de mezcla, compruebe ocasionalmente el crecimiento de las tablas del sistema asociadas con la replicación de mezcla: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**y **MSmerge_past_partition_mappings**. Vuelva a indizar estas tablas periódicamente. Para obtener más información, vea [Reorganizar y volver a generar índices](../indexes/indexes.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
