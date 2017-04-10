---
title: "Poner en modo inactivo una topolog&#237;a de replicaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "administrar replicación, poner en modo inactivo"
  - "poner en modo inactivo [replicación de SQL Server]"
  - "replicación transaccional, copia de seguridad y restauración"
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Poner en modo inactivo una topolog&#237;a de replicaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  *Detener* un sistema implica detener la actividad de las tablas publicadas en todos los nodos y asegurarse de que cada nodo ha recibido todos los cambios de los demás nodos. Este tema explica cómo detener una topología de replicación, una operación necesaria para varias tareas administrativas, y cómo asegurarse que un nodo ha recibido todos los cambios de otros nodos.  
  
### Para detener una topología de replicación transaccional con suscripciones de solo lectura  
  
1.  Detenga la actividad en todas las tablas en el publicador.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_posttracertoken & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
4.  Asegúrese de que cada suscriptor ha recibido el token de seguimiento.  
  
### Para detener una topología de replicación transaccional con suscripciones actualizables  
  
1.  Detenga la actividad en todas las tablas en el publicador y todos los suscriptores.  
  
2.  Si algún suscriptor utiliza suscripciones de actualización en cola:  
  
    1.  Si el Agente de lectura de cola no se está ejecutando de forma continua, ejecútelo. Para obtener más información acerca de cómo ejecutar los agentes, consulte [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Para comprobar que la cola está vacía, ejecute [sp_replqueuemonitor](../../../relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql.md) en cada suscriptor.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_posttracertoken](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
5.  Asegúrese de que cada suscriptor ha recibido el token de seguimiento.  
  
### Para detener una topología de replicación transaccional punto a punto  
  
1.  Detenga la actividad en todas las tablas de todos los nodos.  
  
2.  Ejecutar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en cada base de datos de publicación de la topología.  
  
3.  Si el Agente de registro del LOG o el Agente de distribución no se está ejecutando de forma continua, ejecútelo. El Agente de registro del LOG se debe iniciar antes del Agente de distribución. Para obtener más información acerca de cómo ejecutar los agentes, consulte [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Ejecutar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) en cada base de datos de publicación de la topología. Asegúrese de que el conjunto de resultados contiene las respuestas de cada uno de los otros nodos.  
  
### Para asegurarse de que un nodo punto a punto ha recibido todos los cambios anteriores  
  
1.  Ejecutar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) en la base de datos de publicación en el nodo que está comprobando.  
  
2.  Si el Agente de registro del LOG o el Agente de distribución no se está ejecutando de forma continua, ejecútelo. El Agente de registro del LOG se debe iniciar antes del Agente de distribución. Para obtener más información acerca de cómo ejecutar los agentes, consulte [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Ejecutar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) en la base de datos de publicación en el nodo que está comprobando. Asegúrese de que el conjunto de resultados contiene las respuestas de cada uno de los otros nodos.  
  
### Para detener una topología de replicación de mezcla  
  
1.  Detenga la actividad en todas las tablas en el publicador y en todos los suscriptores.  
  
2.  Ejecute el Agente de mezcla para cada suscripción dos veces: sincronice todas las suscripciones una vez y, a continuación, sincronice cada suscripción una segunda vez. Con esto se asegura de que todos los cambios se han replicado en todos los nodos. Para obtener más información acerca de cómo ejecutar los agentes, consulte [conceptos de los ejecutables del agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) o [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Si se producen conflictos durante la sincronización, es posible que los cambios requeridos por la resolución de conflictos no se propaguen a todos los nodos después de ejecutar el Agente de mezcla dos veces.  
  
## Vea también  
 [Administrar una topología punto a punto & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  