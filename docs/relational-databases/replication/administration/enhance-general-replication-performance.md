---
title: Aumentar el rendimiento de la replicación general | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Snapshot Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- performance [SQL Server replication], general considerations
- transactional replication, performance
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8ac6758c3856858f6b10b17184705022aa51a62e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76288195"
---
# <a name="enhance-general-replication-performance"></a>Aumentar el rendimiento de la replicación general
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Puede aumentar el rendimiento general de todos los tipos de replicación en su aplicación y en la red siguiendo las directrices descritas en este tema.  
  
## <a name="server-and-network"></a>Servidor y red  
  
-   Defina la cantidad mínima y máxima de memoria asignada a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].  
  
     De forma predeterminada, el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] cambia dinámicamente sus necesidades de memoria según los recursos del sistema disponibles. Para evitar la disponibilidad insuficiente de memoria durante las actividades de replicación, utilice la opción **min server memory** para establecer la memoria mínima disponible. Para evitar que el sistema operativo tenga que paginar en el disco para disponer de memoria, puede definir también una cantidad máxima de memoria con la opción **max server memory** . Para obtener más información, consulte [Opciones de configuración del servidor de memoria del servidor](../../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
-   Garantice una asignación adecuada de los archivos de datos y los archivos de registro de la base de datos. Utilice una unidad de disco independiente para el registro de transacciones de todas las bases de datos implicadas en la replicación.  
  
     Puede reducir el tiempo que se tarda en escribir las transacciones si almacena los archivos de registro en una unidad de disco diferente de la unidad en la que almacena la base de datos. Puede reflejar esa unidad mediante una matriz redundante de discos económicos (RAID-1) si requiere tolerancia a errores. Utilice RAID 0 ó 0+1 (según el grado de tolerancia a errores necesario) con otros archivos de la base de datos. Esta práctica es recomendable con independencia de si se utiliza o no la replicación.  
  
-   Considere la posibilidad de agregar memoria a los servidores que se usan en la replicación, en especial al distribuidor.  
  
-   Utilice equipos con varios procesadores.  
  
     Los agentes de replicación pueden aprovechar los procesadores adicionales del servidor. Si la CPU tiene un uso intensivo, considere la posibilidad de instalar una CPU más rápida o varias CPU.  
  
-   Utilice una red rápida.  
  
     La red puede suponer un cuello de botella importante para el rendimiento, en especial para la replicación transaccional. La propagación de cambios a los suscriptores puede mejorarse significativamente utilizando una red rápida de 100 Mbps o superior. Si la red es lenta, especifique una configuración de red y parámetros de agente apropiados.  
  
## <a name="database-design"></a>Diseño de la base de datos  
  
-   Siga las prácticas recomendadas para el diseño de la base de datos.  
  
     Una base de datos replicada por lo general se beneficia de las mismas optimizaciones de rendimiento que una base de datos no replicada. No obstante, los índices deben utilizarse con precaución en el suscriptor: la columna de clave principal del suscriptor debe indizarse, pero los índices adicionales pueden afectar al rendimiento de inserción, actualización y eliminación.  
  
-   Considere la posibilidad de establecer la opción READ_COMMITTED_SNAPSHOT de la base de datos.  
  
     Para ayudar a reducir la contención entre la actividad de los usuarios y la actividad del agente de replicación, configure esta opción para las bases de datos de suscripciones y publicaciones:  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Tenga cuidado con la lógica de negocios de los desencadenadores.  
  
     La lógica de negocios de los desencadenadores definidos por el usuario en el Suscriptor puede ralentizar la replicación de los cambios en el suscriptor.  
  
    -   En la replicación transaccional, puede ser más eficaz incluir esta lógica en procedimientos almacenados personalizados que se utilizan para aplicar los comandos replicados. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
    -   En la replicación de mezcla, puede ser más eficaz utilizar controladores de lógica de negocios. Para obtener más información, consulte [Ejecutar lógica de negocios durante la sincronización de mezcla](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
     Si utiliza desencadenadores para mantener la integridad referencial en las tablas publicadas para la replicación de mezcla, especifique el orden de procesamiento de las tablas para reducir el número de reintentos requeridos por el Agente de mezcla. Para más información, vea [Specify merge replication options](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Especificación de opciones de replicación de mezcla).  
  
-   Limite el uso de tipos de datos de objetos grandes (LOB).  
  
     Los LOB requieren más espacio de almacenamiento y procesamiento que otros tipos de datos de columna. No incluya estas columnas en los artículos a menos que sea necesario para la aplicación. Los tipos de datos **text**, **ntext**y **image** han quedado desusados. Si incluye LOB, se recomienda que utilice los tipos de datos **varchar(max)** , **nvarchar(max)** y **varbinary(max)** , respectivamente.  
  
     Para la replicación transaccional, considere la posibilidad de utilizar el perfil de Agente de distribución denominado **Perfil de distribución para secuencias OLEDB**. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="publication-design"></a>Diseño de la publicación  
  
-   Publique solamente los datos necesarios.  
  
     Puesto que la replicación es fácil de configurar, hay cierta tendencia a publicar más datos de los que son realmente necesarios. Esto puede consumir recursos adicionales en las bases de datos de distribución y en los archivos de instantáneas, y puede reducir el rendimiento de los datos requeridos. Evite publicar tablas innecesarias y considere actualizar las publicaciones con menor frecuencia.  
  
-   Minimice los conflictos a través del diseño de publicaciones y el comportamiento de la aplicación.  
  
     Los siguientes tipos de replicación permiten cambiar los datos en los suscriptores: replicación de mezcla, replicación transaccional con suscripciones actualizables y replicación transaccional punto a punto. La replicación de mezcla y la replicación transaccional con suscripciones actualizables admiten conflictos de datos si se actualiza una fila determinada en varios nodos entre las sincronizaciones. La replicación punto a punto no admite los conflictos de datos; los cambios en los datos deben particionarse. Independientemente del tipo de replicación utilizada, se recomienda realizar particiones de los cambios siempre que sea posible, ya que así se reduce el procesamiento necesario para la detección y resolución de conflictos.  
  
     Para realizar particiones de cambios se pueden publicar subconjuntos de datos en cada suscriptor o hacer que una aplicación dirija los cambios de una fila determinada a un nodo en concreto:  
  
    -   La replicación de mezcla admite la publicación de subconjuntos de datos utilizando filtros con parámetros con una sola publicación. Para obtener más información, consulte [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
    -   La replicación transaccional admite la publicación de subconjuntos de datos utilizando filtros estáticos con varias publicaciones. Para obtener más información, vea [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Utilice los filtros de fila con prudencia.  
  
     Cuando una publicación transaccional incluye uno o varios artículos que utilizan filtros de fila, el Agente de registro del LOG tiene que aplicar el filtro a cada fila afectada por una actualización de la tabla conforme examina el registro de transacciones. Por tanto, el rendimiento del Agente de registro del LOG se verá afectado.  
  
     De igual modo, la replicación de mezcla debe evaluar las filas cambiadas o eliminadas para determinar qué suscriptores deben recibir esas filas. Cuando se emplean filtros de fila para reducir los datos requeridos en el suscriptor, este procesamiento es más complejo y puede ser más lento que cuando publica todas las filas en una tabla. Considere cuidadosamente el compromiso entre la reducción de los requisitos de almacenamiento en cada suscriptor y la necesidad de conseguir el máximo rendimiento. Para obtener más información sobre el filtrado, consulte [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## <a name="subscription-considerations"></a>Consideraciones acerca de las suscripciones  
  
-   Utilice suscripciones de extracción cuando haya un gran número de suscriptores.  
  
     El Agente de distribución y el Agente de mezcla se ejecutan en el distribuidor para las suscripciones de inserción, y en los suscriptores para las suscripciones de extracción. El uso de las suscripciones de extracción puede mejorar el rendimiento desplazando el procesamiento de agentes del distribuidor a los suscriptores. Para obtener más información, vea [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Considere la posibilidad de reinicializar la suscripción si los suscriptores están muy retrasados.  
  
     Cuando sea necesario enviar grandes cantidades de cambios a los suscriptores, reinicializarlos con una nueva instantánea puede ser más rápido que utilizar la replicación para mover los cambios individuales. Para obtener más información, vea [Reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
     En la replicación transaccional, el Monitor de replicación muestra, en la pestaña **Comandos sin distribuir** , información acerca del número de transacciones de la base de datos de distribución que aún no se han distribuido a un suscriptor, así como el tiempo estimado para la distribución de dichas transacciones. Para más información, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="snapshot-considerations"></a>Consideraciones acerca de las instantáneas  
  
-   Ejecute el Agente de instantáneas solamente cuando sea necesario y en horas de poca actividad.  
  
     El Agente de instantáneas copia los datos de forma masiva desde la tabla publicada en el publicador a un archivo de la carpeta de instantáneas del distribuidor. Generar una instantánea puede ser un proceso que consume muchos recursos y es mejor programarla para que se lleve a cabo durante las horas de poca actividad.  
  
-   Utilice una instantánea en modo nativo a menos que sea necesaria una instantánea en modo de carácter.  
  
     Utilice la instantánea en modo nativo predeterminada para todos los suscriptores excepto los suscriptores que no sean de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y los que ejecuten [!INCLUDE[ssEW](../../../includes/ssew-md.md)], que requieren una instantánea en modo de carácter.  
  
-   Utilice una única carpeta de instantáneas para una publicación.  
  
     Al especificar las propiedades de la publicación relacionadas con una ubicación de instantáneas, puede elegir generar archivos de instantáneas en la carpeta de instantáneas predeterminada, en una carpeta de instantáneas alternativa o ambas. La generación de los archivos de instantáneas en las dos ubicaciones requiere espacio adicional en disco y más procesamiento cuando se ejecuta el Agente de instantáneas.  
  
-   Coloque la carpeta de instantáneas en una unidad local del distribuidor que no se utilice para almacenar bases de datos o archivos de registro.  
  
     El Agente de instantáneas realiza una escritura secuencial de los datos en la carpeta de instantáneas. Colocar la carpeta de instantáneas en una unidad independiente de cualquier base de datos o archivo de registro reduce la contención entre los discos y ayuda a que el proceso de las instantáneas se complete más deprisa.  
  
-   Cuando cree la base de datos de suscripciones en el suscriptor, considere la posibilidad de especificar un modelo de recuperación simple o por medio de registros de operaciones masivas. Esto permite un registro mínimo de las inserciones masivas realizadas durante la aplicación de la instantánea en el suscriptor. Una vez que se ha aplicado la instantánea a la base de datos de suscripciones, puede cambiar a otro modelo de recuperación diferente si es necesario (las bases de datos replicadas pueden utilizar cualquiera de los modelos de recuperación). Para obtener más información sobre cómo seleccionar un modelo de recuperación, consulte [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
-   Considere la posibilidad de utilizar la carpeta de instantáneas alternativa y las instantáneas comprimidas en medios extraíbles para las redes de ancho de banda reducido.  
  
     Comprimir archivos de instantáneas en la carpeta de instantáneas alternativa puede reducir los requisitos de almacenamiento en disco y facilitar la transferencia de los archivos de instantáneas en medios extraíbles.  
  
     En algunos casos, las instantáneas comprimidas pueden mejorar el rendimiento de la transferencia de archivos de instantáneas en la red. No obstante, la compresión de instantáneas requiere que el Agente de instantáneas realice un procesamiento adicional al generar los archivos de instantáneas, y otro procesamiento adicional por parte del Agente de distribución o del Agente de mezcla al aplicar los archivos de instantáneas. Esto puede ralentizar, en algunos casos, la generación de instantáneas y aumentar el tiempo de aplicación de una instantánea. Además, las instantáneas comprimidas no se pueden reanudar si se produce un error de red; por tanto, no son adecuadas para redes no confiables. Cuando utilice instantáneas comprimidas en una red, tenga en cuenta estos inconvenientes. Para más información, vea [Modificación de las opciones de la instantánea](../../../relational-databases/replication/snapshot-options.md). 
-   Considere la posibilidad de inicializar una suscripción manualmente.  
  
     En algunos casos, como aquellos en los que intervienen grandes conjuntos de datos iniciales, es preferible inicializar una suscripción mediante otro método distinto a una instantánea. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
## <a name="agent-parameters"></a>Parámetros de los agentes  
  
-   Reduzca el nivel de detalle de los agentes de replicación, excepto durante la prueba inicial, la supervisión o la depuración.  
  
     Reduzca los parámetros **–HistoryVerboseLevel** y **–OutputVerboseLevel** de los agente de distribución o agentes de mezcla. Esto reducirá número de nuevas filas insertadas para realizar el seguimiento de la salida y el historial del agente. En su lugar, los mensajes anteriores del historial con el mismo estado se actualizarán a la nueva información del historial. Aumente los niveles de detalle de la prueba, la supervisión y la depuración para tener toda la información que sea posible sobre la actividad del agente.  
  
-   Use el parámetro **–MaxBCPThreads** del Agente de instantáneas, del Agente de mezcla y del Agente de distribución (el número de subprocesos especificados no debe superar el número de procesadores del equipo). Este parámetro especifica el número de operaciones de copia masiva que se pueden realizar en paralelo cuando se crea y aplica la instantánea.  
  
-   Utilice el parámetro **–UseInprocLoader** del Agente de distribución y del Agente de mezcla (este parámetro no se puede utilizar si las tablas publicadas incluyen columnas XML). Con este parámetro, el agente utiliza el comando BULK INSERT cuando se aplica la instantánea.  
  
 Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para más información, consulte:  
  
-   [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
  
