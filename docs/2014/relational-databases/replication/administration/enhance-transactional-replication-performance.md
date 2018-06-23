---
title: Aumentar el rendimiento de la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
caps.latest.revision: 39
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bb1f7f7d5caa95b0abe7d070ab11b2012fb669a2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104254"
---
# <a name="enhance-transactional-replication-performance"></a>Aumentar el rendimiento de la replicación transaccional
  Una vez que haya considerado las sugerencias generales sobre el rendimiento que se describen en [Aumentar el rendimiento general de la replicación](enhance-general-replication-performance.md), tenga en cuenta estas áreas adicionales específicas de la replicación transaccional.  
  
## <a name="database-design"></a>Diseño de la base de datos  
  
-   Minimice el tamaño de la transacción en el diseño de la aplicación.  
  
     De manera predeterminada, la replicación transaccional propaga los cambios en función de los límites de las transacciones. Si las transacciones son más pequeñas, es menos probable que el Agente de distribución tenga que volver a enviar una transacción debido a problemas de red. Si el agente tiene que volver a enviar una transacción, la cantidad de datos que se enviarán será menor.  
  
## <a name="distributor-configuration"></a>Configuración del distribuidor  
  
-   Configure el distribuidor en un servidor dedicado.  
  
     Puede reducir la carga de procesamiento en el publicador configurando un distribuidor remoto. Para más información, consulte [Configure Distribution](../configure-distribution.md).  
  
-   Ajustar la base de datos de distribución a un tamaño apropiado.  
  
     Pruebe la replicación con una carga típica para el sistema con el fin de determinar cuánto espacio se necesita para almacenar comandos. Asegúrese de que la base de datos es lo suficientemente grande para almacenar comandos sin recurrir al crecimiento automático con frecuencia. Para más información sobre cómo cambiar el tamaño de una base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="publication-design"></a>Diseño de la publicación  
  
-   Replique la ejecución de los procedimientos almacenados al realizar actualizaciones por lotes en las tablas publicadas.  
  
     Si tiene actualizaciones por lotes que afectan ocasionalmente a un gran número de filas en el suscriptor, considere la posibilidad de actualizar la tabla publicada mediante un procedimiento almacenado y publique la ejecución del procedimiento almacenado. En vez de enviar una actualización o eliminación para cada fila afectada, el Agente de distribución ejecutará el mismo procedimiento en el suscriptor con los mismos valores de parámetros. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Reparta los artículos entre varias publicaciones.  
  
     Si no puede utilizar el parámetro **-SubscriptionStreams** que se describe más adelante en este tema, considere la posibilidad de crear varias publicaciones. Repartir artículos entre dichas publicaciones permite que la replicación aplique en paralelo los cambios a los suscriptores.  
  
## <a name="subscription-considerations"></a>Consideraciones acerca de las suscripciones  
  
-   Utilice agentes independientes en lugar de agentes compartidos si tiene varias publicaciones en el mismo publicador (este es el valor predeterminado del Asistente para nueva publicación).  
  
-   Ejecute los agentes continuamente en lugar de utilizar programaciones muy frecuentes.  
  
     Configurar los agentes para que se ejecuten continuamente en vez de crear programaciones frecuentes (por ejemplo, cada minuto) mejora el rendimiento de la replicación, ya que el agente no tiene que iniciarse y detenerse. Si configura el Agente de distribución para que se ejecute continuamente, los cambios se propagan con latencia baja a los demás servidores conectados en la topología. Para obtener más información, vea:  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificar programaciones de sincronización](../specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>Parámetros del Agente de distribución y del Agente de registro del LOG  
  
-   Para resolver los cuellos de botella accidentales que solo ocurren una vez, use el parámetro **–MaxCmdsInTran** para el Agente de registro del LOG.  
  
     El parámetro **–MaxCmdsInTran** especifica el número máximo de instrucciones agrupadas en una transacción cuando el Agente de registro del LOG escribe comandos en la base de datos de distribución. El uso de este parámetro permite al Agente de registro del LOG y al Agente de distribución dividir las transacciones grandes (compuestas por muchos comandos) del publicador en varias transacciones más pequeñas cuando se aplican comandos en el suscriptor. Especificando este parámetro se puede reducir la contención en el distribuidor y la latencia entre el publicador y el suscriptor. Puesto que la transacción original se aplica en unidades más pequeñas, el suscriptor puede obtener acceso a las filas de una transacción lógica del publicador de gran tamaño antes de que finalice la transacción original, lo que interrumpe la estricta atomicidad transaccional. El valor predeterminado es **0**, que conserva los límites de la transacción del publicador. Este parámetro no se aplica a los publicadores de Oracle.  
  
    > [!WARNING]  
    >  `MaxCmdsInTran` no se ha diseñado para estar siempre activado. Su función es evitar los casos en los que alguien ha realizado accidentalmente un gran número de operaciones DML en una sola transacción (lo que produce un retraso en la distribución de comandos hasta que toda la transacción está en la base de datos de distribución, se establecen los bloqueos, etc.). Si se encuentra habitualmente esta situación, debe revisar las aplicaciones y buscar formas de reducir el tamaño de las transacciones.  
  
-   Use el parámetro **–SubscriptionStreams** en el Agente de distribución.  
  
     El parámetro **–SubscriptionStreams** puede mejorar considerablemente el rendimiento de la replicación. Permite establecer varias conexiones con un suscriptor para aplicar lotes de cambios en paralelo, al tiempo que mantiene muchas de las características transaccionales presentes cuando se usa un solo subproceso. Si una de las conexiones no se puede ejecutar o confirmar, todas las conexiones anularán el lote actual y el agente utilizará un solo flujo para volver a intentar los lotes con errores. Antes de que finalice esta fase de reintento, pueden aparecer incoherencias transaccionales temporales en el suscriptor. Una vez que se han confirmado correctamente los lotes con errores, el suscriptor vuelve al estado de coherencia transaccional.  
  
     Se puede especificar un valor para este parámetro del agente mediante el **@subscriptionstreams** de [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql).  
  
-   Aumente el valor del parámetro **-ReadBatchSize** del Agente de registro del LOG.  
  
     El Agente de registro del LOG y el Agente de distribución aceptan tamaños de lotes en las operaciones de lectura y confirmación de transacciones. Los lotes contienen, de forma predeterminada, 500 transacciones. El Agente de lectura del LOG lee el número de transacciones especificado en el registro, estén o no marcadas para la replicación. Cuando se escribe un gran número de transacciones en una base de datos de publicación, pero solo un pequeño subconjunto de ellas está marcado para replicación, deberá utilizar el parámetro **-ReadBatchSize** para aumentar el tamaño del lote leído del Agente de registro del LOG. Este parámetro no se aplica a los publicadores de Oracle.  
  
-   Aumente el valor del parámetro **-CommitBatchSize** del Agente de distribución.  
  
     Confirmar un conjunto de transacciones tiene una sobrecarga fija; al confirmar un número mayor de transacciones con menos frecuencia, la sobrecarga se reparte entre un mayor volumen de datos. No obstante, las ventajas de aumentar este parámetro disminuyen ya que el costo de aplicar los cambios está determinado por otros factores, como la E/S máxima del disco que contiene el registro. Además, existe un desequilibrio que hay que tener en cuenta: cualquier error que provoque que el Agente de distribución vuelva a comenzar debe revertir y volver a aplicar un mayor número de transacciones. En las redes no confiables, un valor más reducido puede provocar menos errores y que sea necesario revertir y volver a aplicar un menor número de transacciones en caso de producirse un error.  
  
-   Reduzca el valor del parámetro **-PollingInterval** del Agente de registro del LOG.  
  
     El parámetro **-PollingInterval** especifica con qué frecuencia se consulta el registro de transacciones de una base de datos publicada para que las transacciones se repliquen. El valor predeterminado es 5 segundos. Si reduce este valor, el registro se sondea más a menudo, lo que puede dar lugar a una menor latencia para el envío de transacciones de la base de datos de publicaciones a la de distribución. No obstante, debe equilibrar la necesidad de una menor latencia frente al aumento de carga en el servidor debido a sondeos más frecuentes.  
  
 Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para obtener más información, vea:  
  
-   [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md)  
  
-   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
  
