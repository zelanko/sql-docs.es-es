---
title: "Estrategias para hacer copias de seguridad y restaurar replicaci&#243;n de instant&#225;neas o replicaci&#243;n transaccional | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "copias de seguridad [replicación de SQL Server], replicación de instantáneas"
  - "restauración [replicación de SQL Server], replicación transaccional"
  - "replicación de instantáneas [SQL Server], copia de seguridad y restauración"
  - "restauración [replicación de SQL Server], replicación de instantáneas"
  - "recuperación [replicación de SQL Server], replicación transaccional"
  - "replicación transaccional, copia de seguridad y restauración"
  - "recuperación [replicación de SQL Server], replicación de instantáneas"
  - "sincronización con copia de seguridad [replicación de SQL Server]"
  - "copias de seguridad [replicación de SQL Server], replicación transaccional"
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# Estrategias para hacer copias de seguridad y restaurar replicaci&#243;n de instant&#225;neas o replicaci&#243;n transaccional
  Hay tres áreas que hay que considerar al diseñar una estrategia de copias de seguridad y restauración para la replicación de instantáneas o transaccional:  
  
-   Qué bases de datos se incluirán en la copia de seguridad.  
  
-   Configuración de la copia de seguridad para la replicación transaccional  
  
-   Los pasos necesarios para restaurar una base de datos. Éstos dependen del tipo de replicación y de las opciones elegidas.  
  
 En este tema se tratan cada una de estas áreas en las tres secciones siguientes. Para obtener información acerca de la copia de seguridad y restauración para la publicación de Oracle, vea [de copia de seguridad y restauración para los publicadores de Oracle](../../../relational-databases/replication/non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## Realizar copias de seguridad de bases de datos  
 Para la replicación de instantáneas y la replicación transaccional, debe crear de forma periódica una copia de seguridad de las siguientes bases de datos:  
  
-   La base de datos de publicaciones en el publicador.  
  
-   La base de datos de distribución en el distribuidor.  
  
-   La base de datos de suscripciones en el suscriptor.  
  
-   Las bases de datos del sistema **maestra** y **msdb** en el publicador, el distribuidor y todos los suscriptores. La copia de seguridad de cada una de estas bases de datos debe realizarse al mismo tiempo que la de las otras y la base de datos de replicación correspondiente. Por ejemplo, cree la copia de seguridad de las bases de datos **master** y **msdb** en el publicador al mismo tiempo que crea la copia de seguridad de la base de datos de publicación. Al restaurar la base de datos de publicación, asegúrese de que las bases de datos **maestra** y **msdb** sean coherentes con la base de datos de publicación en términos de configuración general y configuración de la replicación.  
  
 Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no se realizan copias de seguridad de registros, debe realizarse una copia de seguridad siempre que se cambie un valor importante en la replicación. Para más información, vea [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Configuración de la copia de seguridad para la replicación transaccional  
 La replicación transaccional incluye el uso de la opción **sync with backup** , que se puede establecer en las bases de datos de distribución y de publicación:  
  
-   Se recomienda establecer siempre esta opción en la base de datos de distribución.  
  
     Establecer esta opción en la base de datos de distribución garantiza que las transacciones en el registro de la base de datos de publicaciones no se trunquen hasta que se hayan incluido en una copia de seguridad en la base de datos de distribución. La base de datos de distribución se puede restaurar hasta la última copia de seguridad y todas las transacciones que falten se entregan de la base de datos de publicación a la base de datos de distribución. La replicación continúa sin ninguna variación.  
  
     Establecer esta opción en la base de datos de distribución no afecta a la latencia de replicación. Sin embargo, la opción retrasará el truncamiento del registro en la base de datos de publicación hasta que se haya hecho copia de seguridad de las transacciones correspondientes en la base de datos de distribución. Esto puede crear un registro de transacciones mayor en la base de datos de publicación.  
  
-   Se recomienda establecer esta opción en la base de datos de publicación si su aplicación tolera latencia adicional.  
  
     Establecer esta opción en la base de datos de publicaciones garantiza que las transacciones no se enviarán a la base de datos de distribución hasta que se hayan incluido en la copia de seguridad en la base de datos de publicaciones. Se puede restaurar la última copia de seguridad de la base de datos de publicación en el publicador, sin que exista ninguna posibilidad de que la base de datos de distribución contenga transacciones que la base de datos de publicación restaurada no tenga.  
  
     La latencia y el rendimiento se ven afectados, ya que las transacciones no se pueden enviar a la base de datos de publicaciones hasta que no se hayan incluido en la copia de seguridad del publicador. Por ejemplo, si se crea una copia de seguridad del registro de transacciones cada cinco minutos, habrá cinco minutos más de latencia entre que una transacción se confirma en el publicador y el momento en que la transacción enviada a la base de datos de distribución y posteriormente al suscriptor.  
  
    > [!NOTE]  
    >  La opción **sync with backup** garantiza la coherencia entre la base de datos de publicación y la base de datos de distribución, pero la opción no garantiza que no se pierdan datos. Por ejemplo, si se pierde el registro de transacciones, las transacciones confirmadas desde la última copia de seguridad del registro de transacciones no estarán disponibles en la base de datos de publicación ni en la base de datos de distribución. Éste es el mismo comportamiento que tiene una base de datos no replicada.  
  
 **Para establecer la opción sync with backup**  
  
-   Replicación [!INCLUDE[tsql](../../../includes/tsql-md.md)] programming: [Habilitar copias de seguridad coordinadas para la replicación transaccional & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md)  
  
## Restaurar bases de datos que participan en la replicación  
 Puede restaurar todas las bases de datos de una topología de replicación si hay copias de seguridad recientes disponibles y se siguen los pasos correctos. Los pasos de restauración de la base de datos de publicación dependen del tipo de replicación y de las opciones utilizadas. No obstante, los pasos de restauración de todas las demás bases de datos son independientes del tipo y de las opciones.  
  
 La replicación permite restaurar las bases de datos replicadas en el mismo servidor y base de datos de los que se creó la copia de seguridad. Si restaura una copia de seguridad de una base de datos replicada en otro servidor o base de datos, no se conservará la configuración de la replicación. En este caso, deberá volver a crear todas las publicaciones y suscripciones después de restaurar las copias de seguridad.  
  
### publicador  
 Se proporcionan los pasos de restauración para los siguientes tipos de replicación:  
  
-   Replicación de instantáneas  
  
-   Replicación transaccional de solo lectura  
  
-   Replicación transaccional con suscripciones de actualización  
  
-   Replicación transaccional punto a punto  
  
 La restauración de las bases de datos **msdb** y **maestra** , que también se tratan en esta sección, es igual para los cuatro tipos.  
  
#### Base de datos de publicaciones: replicación de instantáneas  
  
1.  Restaure la última copia de seguridad de la base de datos de publicaciones. Vaya al paso 2.  
  
2.  ¿La base de datos de publicaciones contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, la restauración se ha completado. En caso contrario, continúe en el paso 3.  
  
3.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. La restauración se ha completado.  
  
     Para obtener más información acerca de cómo quitar la replicación, consulte [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
#### Base de datos de publicaciones: replicación transaccional de solo lectura  
  
1.  Restaure la última copia de seguridad de la base de datos de publicaciones. Vaya al paso 2.  
  
2.  ¿Estaba habilitada la opción **sync with backup** en la base de datos de publicación antes del error? En caso afirmativo, vaya al paso 3; de lo contrario, continúe en el paso 5.  
  
     Si la opción está habilitada, la consulta `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` devuelve '1'.  
  
3.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, la restauración se ha completado. De lo contrario, continúe en el paso 4.  
  
4.  La información de configuración de la base de datos de publicación restaurada no es actualizada. Por consiguiente, debe asegurarse de que los suscriptores tienen todos los comandos pendientes en la base de datos de distribución, y, a continuación, quitar y volver a crear la configuración de replicación.  
  
    1.  Ejecute el Agente de distribución hasta que todos los suscriptores estén sincronizados con los comandos pendientes de la base de datos de distribución. Compruebe que todos los comandos se entregan a los suscriptores utilizando la **comandos sin distribuir** ficha Monitor de replicación o consultando el [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) vista en la base de datos de distribución. Continúe en el paso b.  
  
         Para obtener más información sobre cómo ejecutar el agente de distribución, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obtener más información acerca de cómo comprobar comandos, consulte [comandos replicados de vista y otra información en la base de datos de distribución & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) y [Ver información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. La restauración se ha completado.  
  
         Para obtener más información acerca de cómo quitar la replicación, consulte [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
5.  La opción **sync with backup** no estaba activada en la base de datos de publicación. Por consiguiente, las transacciones que no se incluyeron en la copia de seguridad restaurada se podrían haber entregado al distribuidor y suscriptores. Ahora, debe asegurarse de que los suscriptores tengan todos los comandos pendientes de la base de datos de distribución y, después, debe aplicar manualmente a la base de datos de publicación todas las transacciones no incluidas en la copia de seguridad restaurada.  
  
    > [!IMPORTANT]  
    >  Este proceso puede dar lugar a que se restauren las tablas publicadas hasta un momento más reciente que el de otras tablas no publicadas restauradas a partir de la copia de seguridad.  
  
    1.  Ejecute el Agente de distribución hasta que todos los suscriptores estén sincronizados con los comandos pendientes de la base de datos de distribución. Compruebe que todos los comandos se entregan a los suscriptores utilizando la **comandos sin distribuir** ficha Monitor de replicación o consultando el [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) vista en la base de datos de distribución. Continúe en el paso b.  
  
         Para obtener más información sobre cómo ejecutar el agente de distribución, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
         Para obtener más información acerca de cómo comprobar comandos, consulte [comandos replicados de vista y otra información en la base de datos de distribución & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) y [Ver información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
    2.  Utilice la [tablediff utility](../../../tools/tablediff-utility.md) u otra herramienta para sincronizar manualmente el publicador con el suscriptor. Esto le permite recuperar los datos de la base de datos de suscripciones que no estaban incluidos en la copia de seguridad de base de datos de publicación. Continúe en el paso c.  
  
         Para obtener más información acerca de la **tablediff** utilidad, vea [comparar tablas replicadas para diferencias & #40; Programación de la replicación y nº 41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, ejecute el [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) procedimiento almacenado para sincronizar los metadatos del publicador con el distribuidor de metadatos. La restauración se ha completado. En caso contrario, continúe en el paso d.  
  
    4.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. La restauración se ha completado.  
  
         Para obtener más información acerca de cómo quitar la replicación, consulte [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Base de datos de publicaciones: replicación transaccional con suscripciones de actualización  
  
1.  Restaure la última copia de seguridad de la base de datos de publicaciones. Vaya al paso 2.  
  
2.  Ejecute el Agente de distribución hasta que todos los suscriptores estén sincronizados con los comandos pendientes de la base de datos de distribución. Compruebe que todos los comandos se entregan a los suscriptores utilizando la **comandos sin distribuir** ficha Monitor de replicación o consultando el [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) vista en la base de datos de distribución. Vaya al paso 3.  
  
     Para obtener más información sobre cómo ejecutar el agente de distribución, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
     Para obtener más información acerca de cómo comprobar comandos, consulte [comandos replicados de vista y otra información en la base de datos de distribución & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) y [Ver información y realizar tareas de los agentes asociados con una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
3.  Si utiliza suscripciones de actualización en cola, conéctese a cada suscriptor y eliminar todas las filas de la [MSreplication_queue & #40; Transact-SQL & #41;](../../../relational-databases/system-tables/msreplication-queue-transact-sql.md) tabla en la base de datos de suscripción. Vaya al paso 4.  
  
    > [!NOTE]  
    >  Si está utilizando suscripciones de actualización en cola y hay tablas que contienen columnas de identidad, debe asegurarse de que se asignen los intervalos de identidad correctos después de la restauración. Para obtener más información, consulte [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
4.  Ahora, debe asegurarse de que los suscriptores tengan todos los comandos pendientes de la base de datos de distribución y, después, debe aplicar manualmente a la base de datos de publicación todas las transacciones no incluidas en la copia de seguridad restaurada.  
  
    > [!IMPORTANT]  
    >  Este proceso puede dar lugar a que se restauren las tablas publicadas hasta un momento más reciente que el de otras tablas no publicadas restauradas a partir de la copia de seguridad.  
  
    1.  Ejecute el Agente de distribución hasta que todos los suscriptores estén sincronizados con los comandos pendientes de la base de datos de distribución. Compruebe que todos los comandos se entregan a los suscriptores mediante el Monitor de replicación o consultando el [MSdistribution_status](../../../relational-databases/system-views/msdistribution-status-transact-sql.md) vista en la base de datos de distribución. Continúe en el paso b.  
  
    2.  Utilice la [tablediff Utility](../../../tools/tablediff-utility.md) u otra herramienta para sincronizar manualmente el publicador con el suscriptor. Esto le permite recuperar los datos de la base de datos de suscripciones que no estaban incluidos en la copia de seguridad de base de datos de publicación. Continúe en el paso c.  
  
         Para obtener más información acerca de la **tablediff** utilidad, vea [comparar tablas replicadas para diferencias & #40; Programación de la replicación y nº 41;](../../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, ejecute el [sp_replrestart](../../../relational-databases/system-stored-procedures/sp-replrestart-transact-sql.md) procedimiento almacenado para sincronizar los metadatos del publicador con el distribuidor de metadatos. La restauración se ha completado. En caso contrario, continúe en el paso d.  
  
    4.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. La restauración se ha completado.  
  
         Para obtener más información acerca de cómo quitar la replicación, vea y [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Base de datos de publicaciones: replicación transaccional punto a punto  
 En los pasos siguientes, las bases de datos de publicación **A**, **B**, y **C** están en una topología de replicación transaccional punto a punto. Las bases de datos **A** y **C** están en línea y funcionan correctamente; la base de datos **B** es la que se desea restaurar. El proceso descrito aquí, sobre todo los pasos 7, 10 y 11, son muy similares al proceso que se requiere para agregar un nodo a una topología punto a punto. La forma más directa de llevar a cabo estos pasos es mediante el Asistente de configuración de la topología punto a punto, pero también puede usar procedimientos almacenados.  
  
1.  Ejecute los agentes de distribución para sincronizar las bases de datos de suscripciones **A** y **C**. Vaya al paso 2.  
  
     Para obtener más información sobre cómo ejecutar el agente de distribución, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Si la distribución de base de datos que **B** utiliza sigue estando disponible, ejecutar agentes de distribución para sincronizar las suscripciones entre las bases de datos **B** y **A** y bases de datos y B y **C**. Vaya al paso 3.  
  
3.  Quite los metadatos de la distribución de la base de datos que **B** utiliza ejecutando [sp_removedistpublisherdbreplication](../../../relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql.md) en la base de datos de distribución para **B**. Vaya al paso 4.  
  
4.  Las bases de datos **A** y **C**, quite las suscripciones a la publicación en la base de datos **B**. Vaya al paso 5.  
  
     Para obtener más información acerca de cómo quitar suscripciones, vea [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
5.  Realizar una copia de seguridad del registro o la copia de seguridad completa de base de datos **A**. Vaya al paso 6.  
  
6.  Restaurar la copia de seguridad de base de datos **A** en la base de datos **B**. Base de datos **B** tiene ahora los datos de la base de datos **A**, pero no la configuración de replicación. Al restaurar una copia de seguridad en otro servidor, se quita la replicación; por lo tanto, se ha quitado la replicación de base de datos **B**. Vaya al paso 7.  
  
7.  Volver a crear la publicación en la base de datos **B**, y, a continuación, volver a crear las suscripciones entre las bases de datos **A** y **B**. (Las suscripciones que implican la base de datos **C** se controlan en una etapa posterior.).  
  
    1.  Volver a crear la publicación en la base de datos **B**. Continúe en el paso b.  
  
    2.  Volver a crear la suscripción en la base de datos **B** a la publicación de la base de datos **A**, especificando que la suscripción debe inicializarse con una copia de seguridad (un valor de **inicializar con copia de seguridad** para el **@sync_type** parámetro de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Continúe en el paso c.  
  
    3.  Volver a crear la suscripción en la base de datos **A** a la publicación de la base de datos **B**, especificando que el suscriptor ya tiene los datos (un valor de **sólo compatibilidad con réplica** para el **@sync_type** parámetro de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Vaya al paso 8.  
  
8.  Ejecute los agentes de distribución para sincronizar las bases de datos de suscripciones **A** y **B**. Si hay columnas de identidad en las tablas publicadas, vaya al paso 9. En caso contrario, continúe en el paso 10.  
  
9. Después de la restauración, el intervalo de identidad asignada para cada tabla de base de datos **A** también se utilizará en la base de datos **B**. Asegúrese de que la base de datos restaurada **B** ha recibido todos los cambios de la base de datos con errores **B** que se han propagado a la base de datos **A** y base de datos **C**; y regenere el intervalo de identidad para cada tabla.  
  
    1.  Ejecutar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en la base de datos **B** y recuperar el parámetro de salida **@request_id**. Continúe en el paso b.  
  
    2.  De forma predeterminada, el Agente de distribución está configurado para ejecutarse de forma continua, por lo que los tokens deben enviarse automáticamente a todos los nodos. Si el Agente de distribución no se está ejecutando de forma continua, ejecútelo. Para obtener más información, consulte [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Continúe en el paso c.  
  
    3.  Ejecutar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), proporcionando la **@request_id** valor recuperado en el paso b. Espere hasta que todos los nodos indiquen que han recibido la solicitud del mismo nivel. Continúe en el paso d.  
  
    4.  Use [DBCC CHECKIDENT](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) para reinicializar cada tabla de la base de datos **B** con el fin de asegurarse de que se utiliza un intervalo apropiado. Vaya al paso 10.  
  
     Para obtener más información acerca de cómo administrar intervalos de identidad, vea la sección "Asignar intervalos para la administración de intervalos de identidad manual" de [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
10. En este punto, la base de datos **B** y base de datos **C** no están conectados directamente, pero reciben los cambios a través de la base de datos **A**. Si la topología contiene cualquier nodo que está ejecutando [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], continúe en el paso 11; en caso contrario, continúe en el paso 12.  
  
11. Detenga el sistema y, a continuación, volver a crear la suscripción entre bases de datos **B** y **C**. Para detener el sistema, hay que detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo haya recibido todos los cambios de los demás nodos.  
  
    1.  Detenga toda la actividad en las tablas publicadas de la topología punto a punto. Continúe en el paso b.  
  
    2.  Ejecutar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en la base de datos **B** y recuperar el parámetro de salida **@request_id**. Continúe en el paso c.  
  
    3.  De forma predeterminada, el Agente de distribución está configurado para ejecutarse de forma continua, por lo que los tokens deben enviarse automáticamente a todos los nodos. Si el Agente de distribución no se está ejecutando de forma continua, ejecútelo. Continúe en el paso d.  
  
    4.  Ejecutar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md), proporcionando la **@request_id** valor recuperado en el paso b. Espere hasta que todos los nodos indiquen que han recibido la solicitud del mismo nivel. Continúe en el paso e.  
  
    5.  Volver a crear la suscripción en la base de datos **B** a la publicación de la base de datos **C**, especificando que el suscriptor ya tiene los datos. Continúe en el paso b.  
  
    6.  Volver a crear la suscripción en la base de datos **C** a la publicación de la base de datos **B**, especificando que el suscriptor ya tiene los datos. Vaya al paso 13.  
  
12. Volver a crear la suscripción entre bases de datos **B** y **C**:  
  
    1.  En la base de datos **B**, consulta el [MSpeer_lsns](../../../relational-databases/system-tables/mspeer-lsns-transact-sql.md) tabla para recuperar el número de secuencia de registro (LSN) de la transacción más reciente de esa base de datos **B** ha recibido de la base de datos **C**.  
  
    2.  Volver a crear la suscripción en la base de datos **B** a la publicación de la base de datos **C**, especificando que la suscripción debe inicializarse basándose en LSN (un valor de **inicializar desde lsn** para el **@sync_type** parámetro de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)). Continúe en el paso b.  
  
    3.  Volver a crear la suscripción en la base de datos **C** a la publicación de la base de datos **B**, especificando que el suscriptor ya tiene los datos. Vaya al paso 13.  
  
13. Ejecute los agentes de distribución para sincronizar las bases de datos de suscripciones **B** y **C**. La restauración se ha completado.  
  
#### Base de datos msdb (publicador)  
  
1.  Restaure la última copia de seguridad de la base de datos **msdb** .  
  
2.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, la recuperación se ha completado. En caso contrario, continúe en el paso 3.  
  
3.  Vuelva a crear el trabajo de limpieza de suscripción a partir de los scripts de replicación. La recuperación se ha completado.  
  
#### Base de datos maestra (publicador)  
  
1.  Restaure la última copia de seguridad de la base de datos **master** .  
  
2.  Asegúrese de que la base de datos sea coherente con la base de datos de publicación en términos de configuración general y configuración de la replicación.  
  
### Bases de datos del distribuidor  
  
#### Base de datos de distribución  
  
1.  Restaure la última copia de seguridad de la base de datos de distribución.  
  
2.  ¿Estaba habilitada la opción **sync with backup** en la base de datos de distribución antes del error? En caso afirmativo, vaya al paso 3; de lo contrario, continúe en el paso 4.  
  
     Si la opción está habilitada, la consulta `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` devuelve '1'.  
  
3.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, la recuperación se ha completado. De lo contrario, continúe en el paso 4.  
  
4.  La información de configuración en la base de datos de distribución restaurada no está actualizada, o la **sincronización con copia de seguridad** opción no se estableció en la base de datos de distribución. (Después de la restauración, a la base de datos de distribución le podrían faltar transacciones que se confirmaron en el publicador pero no se entregaron todavía a suscriptores.) Quite y vuelva a crear la replicación y después, ejecute la validación.  
  
    1.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. Continúe en el paso b.  
  
         Para obtener más información acerca de cómo quitar la replicación, consulte [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
         Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
    2.  Marque todas las publicaciones para validación. Reinicialice todas las suscripciones que no superen la validación. La recuperación se ha completado.  
  
         Para obtener más información acerca de la validación, consulte [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Para obtener más información acerca de la reinicialización, vea [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Base de datos msdb (distribuidor)  
  
1.  Restaure la última copia de seguridad de la base de datos **msdb** .  
  
2.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las publicaciones y suscripciones? En caso afirmativo, la recuperación se ha completado. En caso contrario, continúe en el paso 3.  
  
3.  Quite la configuración de replicación del publicador, el distribuidor y los suscriptores, y vuelva a crear la configuración. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. Vaya al paso 4.  
  
     Para obtener más información acerca de cómo quitar la replicación, consulte [sp_removedbreplication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
     Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
4.  Marque todas las publicaciones para validación. Reinicialice todas las suscripciones que no superen la validación. La recuperación se ha completado.  
  
     Para obtener más información acerca de la validación, consulte [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md). Para obtener más información acerca de la reinicialización, vea [reinicializar suscripciones](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Base de datos maestra (distribuidor)  
  
1.  Restaure la última copia de seguridad de la base de datos **master** .  
  
2.  Asegúrese de que la base de datos sea coherente con la base de datos de publicación en términos de configuración general y configuración de la replicación.  
  
### Bases de datos del suscriptor  
  
#### Base de datos de suscripciones  
  
1.  ¿La última copia de seguridad de la base de datos de suscripciones es más reciente que el período mínimo de retención de distribución en la base de datos de distribución? (Esto determina si el distribuidor sigue teniendo todos los comandos que se exigen para actualizar el suscriptor). En caso afirmativo, continúe en el paso 2. En caso contrario, reinicialice la suscripción. La recuperación se ha completado.  
  
     Para determinar la configuración de retención de distribución máximo, ejecute [sp_helpdistributiondb](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) y recuperar el valor de la **max_distretention** columna (este valor en horas).  
  
     Para obtener más información acerca de cómo reinicializar una suscripción, vea [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
2.  Restaure la última copia de seguridad de la base de datos de suscripciones. Vaya al paso 3.  
  
3.  Si la base de datos de suscripciones solo contiene las suscripciones de inserción, vaya al paso 4. Si la base de datos de suscripciones contiene cualquier suscripción de extracción, hágase las preguntas siguientes: ¿está actualizada la información de suscripción? ¿La base de datos incluye todas las tablas y opciones que se establecieron en el momento del error? En caso afirmativo, continúe en el paso 4. En caso contrario, reinicialice la suscripción. La recuperación se ha completado.  
  
4.  Para sincronizar el suscriptor, ejecute el Agente de distribución. La recuperación se ha completado.  
  
     Para obtener más información sobre cómo ejecutar el agente de distribución, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
#### Base de datos msdb (suscriptor)  
  
1.  Restaure la última copia de seguridad de la base de datos **msdb** . ¿Se utilizan suscripciones de extracción en este suscriptor? Si no es así, la restauración se ha completado. En caso afirmativo, continúe en el paso 2.  
  
2.  ¿Está completa y actualizada la copia de seguridad restaurada? ¿Contiene la configuración más reciente de todas las suscripciones de extracción? En caso afirmativo, la recuperación se ha completado. En caso contrario, continúe en el paso 3.  
  
3.  Quite y vuelva a crear todas las suscripciones de extracción. Al volver a crear las suscripciones, especifique que el suscriptor ya tiene los datos. La restauración se ha completado.  
  
     Para obtener más información acerca de cómo quitar suscripciones, vea [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md).  
  
     Para obtener más información acerca de cómo especificar que el suscriptor ya tiene los datos, vea [Initialize a Subscription Manually](../../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
#### Base de datos maestra (suscriptor)  
  
1.  Restaure la última copia de seguridad de la base de datos **master** .  
  
2.  Asegúrese de que la base de datos sea coherente con la base de datos de publicación en términos de configuración general y configuración de la replicación.  
  
## Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar la distribución](../../../relational-databases/replication/configure-distribution.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md)   
 [Inicializar una suscripción](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Sincronizar datos](../../../relational-databases/replication/synchronize-data.md)  
  
  