---
title: Perfiles del Agente de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 95166948ff2d447eaac439442230af91d75c1bf3
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922863"
---
# <a name="replication-agent-profiles"></a>Perfiles del Agente de replicación
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Cuando se configura la replicación, se instala un conjunto de perfiles de agente en el distribuidor. Un perfil de agente contiene un conjunto de parámetros que se usan cada vez que se ejecuta un agente: cada agente inicia una sesión en el distribuidor durante su proceso de inicio y consulta los parámetros de su perfil. En las suscripciones de mezcla que utilizan la sincronización web, los perfiles se descargan y almacenan en el suscriptor. Si se cambia el perfil, éste se actualiza en el suscriptor la próxima vez que se ejecuta el Agente de mezcla. Para obtener más información acerca de la sincronización web, vea [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 La replicación proporciona un perfil predeterminado para cada agente y perfiles predefinidos adicionales para el Agente de registro del LOG, el Agente de distribución y el Agente de mezcla. Además de los perfiles proporcionados, puede crear perfiles adecuados a los requisitos de su aplicación. Un perfil de agente permite cambiar fácilmente los principales parámetros de todos los agentes asociados con ese perfil. Por ejemplo, si tiene 20 agentes de instantáneas y necesita cambiar el valor de tiempo de espera de la consulta (el parámetro **-QueryTimeout** ), puede actualizar el perfil utilizado por los agentes de distribución, con lo que todos los agentes de instantáneas comenzarán automáticamente a utilizar el nuevo valor la próxima vez que se ejecuten.  
  
 También puede tener varios perfiles para distintas instancias de un agente. Por ejemplo, un agente de mezcla que se conecta al publicador y distribuidor a través de una conexión de acceso telefónico podría utilizar un conjunto de parámetros que se ajusten mejor a los vínculos de comunicaciones más lentos mediante el perfil de **conexión lenta** .  
  
> [!NOTE]  
>  Si especifica un valor para un parámetro de agente en la línea de comandos, ese valor reemplaza al valor establecido para el mismo parámetro en el perfil del agente.  
  
 **Para utilizar y modificar perfiles de agente**  
  
-   [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>Perfiles del Agente de instantáneas  
 En la siguiente tabla se muestran los parámetros definidos en el perfil predeterminado del Agente de instantáneas. Para obtener más información acerca de estos parámetros, vea [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
||default|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>Perfiles del Agente de registro del LOG  
 En la siguiente tabla se muestran los parámetros definidos en los perfiles del Agente de registro del LOG. Cada columna de la tabla representa un perfil con nombre. Para obtener más información acerca de estos parámetros, vea [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
||default|historial detallado|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>Perfiles del Agente de distribución  
 En la siguiente tabla se muestran los parámetros definidos en los perfiles del Agente de distribución. Cada columna de la tabla representa un perfil con nombre. Para obtener más información acerca de estos parámetros, vea [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
||default|historial detallado|Administrador de sincronización de Windows|Continuar después de errores de coherencia de datos.|Perfil de distribución para secuencias OLEDB|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32 768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32 768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>Perfiles del Agente de mezcla  
 En la siguiente tabla se muestran los parámetros definidos en los perfiles del Agente de mezcla. Cada columna de la tabla representa un perfil con nombre. Para obtener más información acerca de estos parámetros, vea [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
||default|historial detallado|Administrador de sincronización de Windows|validación del recuento de filas|validación del recuento de filas y de la suma de comprobación|conexión lenta|grandes volúmenes entre servidores|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|1|1|1|1|1|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|1|1|1|1|1|1|1|  
|**-HistoryVerboseLevel**|2|3|1|1|2|1|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|1|1|1|1|1|1|1|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>Perfiles del Agente de lectura de cola  
 En la siguiente tabla se muestran los parámetros definidos en el perfil predeterminado del Agente de lectura de cola. Para obtener más información acerca de estos parámetros, vea [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md).  
  
||default|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>Consulte también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
