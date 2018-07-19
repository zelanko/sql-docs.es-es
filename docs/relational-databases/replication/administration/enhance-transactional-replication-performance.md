---
title: Aumentar el rendimiento de la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9314c7ffa3a25aa9feb0e8632c68667a4662f86e
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356057"
---
# <a name="enhance-transactional-replication-performance"></a>Aumentar el rendimiento de la replicación transaccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una vez que haya considerado las sugerencias generales sobre el rendimiento que se describen en [Aumentar el rendimiento general de la replicación](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), tenga en cuenta estas áreas adicionales específicas de la replicación transaccional.  
  
## <a name="database-design"></a>Diseño de la base de datos  
  
-   Minimice el tamaño de la transacción en el diseño de la aplicación.  
  
     De manera predeterminada, la replicación transaccional propaga los cambios en función de los límites de las transacciones. Si las transacciones son más pequeñas, es menos probable que el Agente de distribución vuelva a enviar una transacción debido a problemas de red. Si el agente tiene que volver a enviar una transacción, la cantidad de datos que se enviarán será menor. 

  
## <a name="distributor-configuration"></a>Configuración del distribuidor  
  
-   Configure el distribuidor en un servidor dedicado.  
  
     Puede reducir la carga de procesamiento en el publicador configurando un distribuidor remoto. Para más información, consulte [Configure Distribution](../../../relational-databases/replication/configure-distribution.md).  
  
-   Ajustar la base de datos de distribución a un tamaño apropiado.  
  
     Pruebe la replicación con una carga típica para el sistema con el fin de determinar cuánto espacio se necesita para almacenar comandos. Asegúrese de que la base de datos es lo suficientemente grande para almacenar comandos sin recurrir al crecimiento automático con frecuencia. Para más información sobre cómo cambiar el tamaño de una base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="publication-design"></a>Diseño de la publicación  
  
-   Replique la ejecución de los procedimientos almacenados al realizar actualizaciones por lotes en las tablas publicadas.  
  
     Si tiene actualizaciones por lotes que afectan ocasionalmente a un gran número de filas en el suscriptor, considere la posibilidad de actualizar la tabla publicada mediante un procedimiento almacenado y publique la ejecución del procedimiento almacenado. En vez de enviar una actualización o eliminación para cada fila afectada, el Agente de distribución ejecutará el mismo procedimiento en el suscriptor con los mismos valores de parámetros. Para más información, vea [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
-   Reparta los artículos entre varias publicaciones.  
  
     Si no puede utilizar el [parámetro **-SubscriptionStreams**](#subscriptionstreams) que se describe más adelante en este tema, considere la posibilidad de crear varias publicaciones. Repartir artículos entre dichas publicaciones permite que la replicación aplique en paralelo los cambios a los suscriptores.  
  
## <a name="subscription-considerations"></a>Consideraciones acerca de las suscripciones  
  
-   Utilice agentes independientes en lugar de agentes compartidos si tiene varias publicaciones en el mismo publicador (este es el valor predeterminado del Asistente para nueva publicación).  
  
-   Ejecute los agentes continuamente en lugar de utilizar programaciones frecuentes.  
  
     Configurar los agentes para que se ejecuten continuamente en vez de crear programaciones frecuentes (por ejemplo, cada minuto) mejora el rendimiento de la replicación, ya que el agente no tiene que iniciarse y detenerse. Si configura el Agente de distribución para que se ejecute continuamente, los cambios se propagan con latencia baja a los demás servidores conectados en la topología. Para obtener más información, vea:  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificar programaciones de sincronización](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>Parámetros del Agente de distribución y del Agente de registro del LOG  
Los parámetros de perfil del Agente a menudo se ajustan para aumentar el rendimiento del Agente de distribución y del Agente de registro del LOG con sistemas OLTP de alto tráfico. 

Se realizaron pruebas para determinar los mejores valores para mejorar el rendimiento del Agente de distribución y del Agente de registro del LOG. Este pruebas concluyeron que la carga de trabajo era un factor determinante para determinar qué valores funcionaron en qué situación y, por lo tanto, no hay un ajuste de valor único que mejore el rendimiento para cada situación. 

Las conclusiones: 
- Para un *Agente de registro del LOG* con cargas de trabajo de transacciones más pequeñas (menos de 500 comandos), un valor mayor de **ReadBatchSize** puede beneficiar el rendimiento. Sin embargo, para cargas de trabajo con transacciones de grandes dimensiones, cambiar este valor no mejorará el rendimiento. 
    - Cuando hay varios Agentes de registro del LOG y varios Agentes de distribución que se ejecutan en paralelo en el mismo servidor, un valor mayor de **ReadBatchSize** provoca contención en la base de datos de distribución. 
- Para el *Agente de distribución*
    - Aumentar el valor de **CommitBatchSize** puede mejorar el rendimiento. El inconveniente es que, si se produce un error, el Agente de distribución debe revertir y volver a empezar para aplicar nuevamente un mayor número de transacciones. 
    - Aumentar el valor de **SubscriptionStreams** sí ayuda en el rendimiento general del Agente de distribución, ya que varias conexiones al suscriptor aplican lotes de cambios en paralelo. Sin embargo, dependiendo del número de procesadores y otras condiciones de metadatos (por ejemplo, la clave principal, claves externas, restricciones únicas e índices), el valor más alto de SubscriptionStreams realmente podría tener un efecto adverso. Además, si no se puede ejecutar ni confirmar una secuencia, el Agente de distribución retrocede para usar una secuencia única para reintentar los lotes con errores.


Para más información sobre estas pruebas, consulte el blog [Optimizing replication agent profile parameters for better performance](https://blogs.msdn.microsoft.com/sql_server_team/optimizing-replication-agent-profile-parameters-for-better-performance/) (Optimizar los parámetros de perfil del agente de replicación para mejorar el rendimiento).


### <a name="log-reader-agent"></a>Agente de registro del LOG

#### <a name="readbatchsize"></a>ReadBatchSize
- Aumente el valor del parámetro **-ReadBatchSize** del Agente de registro del LOG.  
  
El Agente de registro del LOG y el Agente de distribución aceptan tamaños de lotes en las operaciones de lectura y confirmación de transacciones. Los lotes contienen, de forma predeterminada, 500 transacciones. El Agente de lectura del LOG lee el número de transacciones especificado en el registro, estén o no marcadas para la replicación. Cuando se escribe un gran número de transacciones en una base de datos de publicación, pero solo un pequeño subconjunto de ellas está marcado para replicación, deberá utilizar el parámetro **-ReadBatchSize** para aumentar el tamaño del lote leído del Agente de registro del LOG. Este parámetro no se aplica a los publicadores de Oracle.  

   - Las cargas de trabajo de transacciones más pequeñas (menos de 500 comandos) ven un aumento en la cantidad de comandos que se procesan por segundo cuando **ReadBatchSize** aumenta hasta 5000. 
   - Para cargas de trabajo mayores (transacciones con 500 a 1000 comandos), aumentar el valor **ReadBatchSize** tiene pocas mejoras de rendimiento. Aumentar el valor **ReadBatchSize** da como resultado un mayor número de transacciones que se escriben en la base de datos de distribución en un ida y vuelta. Esto aumenta las transacciones de tiempo y los comandos son visibles para el Agente de distribución e introduce la latencia en el proceso de replicación.  

#### <a name="pollinginterval"></a>PollingInterval
- Reduzca el valor del parámetro **-PollingInterval** del Agente de registro del LOG.  
  
El parámetro **-PollingInterval** especifica con qué frecuencia se consulta el registro de transacciones de una base de datos publicada para que las transacciones se repliquen. El valor predeterminado es 5 segundos. Si reduce este valor, el registro se sondea más a menudo, lo que puede dar lugar a una menor latencia para el envío de transacciones de la base de datos de publicaciones a la de distribución. No obstante, debe equilibrar la necesidad de una menor latencia frente al aumento de carga en el servidor debido a sondeos más frecuentes.   
  
#### <a name="maxcmdsintran"></a>MaxCmdsInTran
- Para resolver los cuellos de botella accidentales que solo ocurren una vez, use el parámetro **–MaxCmdsInTran** para el Agente de registro del LOG.  
  
El parámetro **–MaxCmdsInTran** especifica el número máximo de instrucciones agrupadas en una transacción cuando el Agente de registro del LOG escribe comandos en la base de datos de distribución. El uso de este parámetro permite al Agente de registro del LOG y al Agente de distribución dividir las transacciones grandes (compuestas por muchos comandos) del publicador en varias transacciones más pequeñas cuando se aplican comandos en el suscriptor. Especificando este parámetro se puede reducir la contención en el distribuidor y la latencia entre el publicador y el suscriptor. Puesto que la transacción original se aplica en unidades más pequeñas, el suscriptor puede obtener acceso a las filas de una transacción lógica del publicador de gran tamaño antes de que finalice la transacción original, lo que interrumpe la estricta atomicidad transaccional. El valor predeterminado es **0**, que conserva los límites de la transacción del publicador. Este parámetro no se aplica a los publicadores de Oracle.  
  
   > [!WARNING]  
   >  **MaxCmdsInTran** no se ha diseñado para estar siempre activado. Su función es evitar los casos en los que alguien ha realizado accidentalmente un gran número de operaciones DML en una sola transacción (lo que produce un retraso en la distribución de comandos hasta que toda la transacción está en la base de datos de distribución, se establecen los bloqueos, etc.). Si se encuentra habitualmente esta situación, revise las aplicaciones y busque formas de reducir el tamaño de las transacciones.  
  
### <a name="distribution-agent"></a>Agente de distribución

#### <a name="subscriptionstreams"></a>SubscriptionStreams
- Aumente el parámetro **–SubscriptionStreams** en el Agente de distribución.  
  
El parámetro **–SubscriptionStreams** puede mejorar considerablemente el rendimiento de la replicación. Permite establecer varias conexiones con un suscriptor para aplicar lotes de cambios en paralelo, al tiempo que mantiene muchas de las características transaccionales presentes cuando se usa un solo subproceso. Si una de las conexiones no se puede ejecutar o confirmar, todas las conexiones anularán el lote actual y el agente utilizará un solo flujo para volver a intentar los lotes con errores. Antes de que finalice esta fase de reintento, pueden aparecer incoherencias transaccionales temporales en el suscriptor. Una vez que se han confirmado correctamente los lotes con errores, el suscriptor vuelve al estado de coherencia transaccional.  
  
Se puede especificar un valor para este parámetro del agente mediante el **@subscriptionstreams** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).  

Para más información sobre cómo implementar secuencias de suscripción, consulte el artículo sobre cómo [navegar por la configuración subscriptionStream de replicación de SQL](https://blogs.msdn.microsoft.com/repltalk/2010/03/01/navigating-sql-replication-subscriptionstreams-setting).
  
#### <a name="commitbatchsize"></a>CommitBatchSize
- Aumente el valor del parámetro **-CommitBatchSize** del Agente de distribución.  
  
Confirmar un conjunto de transacciones tiene una sobrecarga fija; al confirmar un número mayor de transacciones con menos frecuencia, la sobrecarga se reparte entre un mayor volumen de datos.  Aumentar el valor CommitBatchSize (hasta 200) puede mejorar el rendimiento a medida que más transacciones se confirman en el suscriptor. No obstante, las ventajas de aumentar este parámetro disminuyen ya que el costo de aplicar los cambios está determinado por otros factores, como la E/S máxima del disco que contiene el registro. Además, existe un desequilibrio que hay que tener en cuenta: cualquier error que provoque que el Agente de distribución vuelva a comenzar debe revertir y volver a aplicar un mayor número de transacciones. En las redes no confiables, un valor más reducido puede provocar menos errores y que sea necesario revertir y volver a aplicar un menor número de transacciones en caso de producirse un error.  
  

##<a name="see-more"></a>Ver más
  
[Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
[Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
[Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
