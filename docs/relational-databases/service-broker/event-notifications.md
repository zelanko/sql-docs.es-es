---
title: Notificaciones de eventos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6a1470d8bb606a29df7c7393fbd0c74772ba5d06
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="event-notifications"></a>Notificaciones de eventos
  Las notificaciones de eventos envían información acerca de los eventos a un servicio [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Las notificaciones de eventos se ejecutan como respuesta a una variedad de instrucciones del lenguaje de definición de datos (DDL) [!INCLUDE[tsql](../../includes/tsql-md.md)] y eventos de Seguimiento de SQL enviando información acerca de esos eventos a un servicio de [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
 Las notificaciones de eventos se pueden usar para realizar lo siguiente:  
  
-   Registrar y revisar cambios o actividades que se producen en la base de datos.  
  
-   Realizar una acción en respuesta a un evento de una forma asincrónica en lugar de sincrónica.  
  
 Las notificaciones de eventos pueden ofrecer una alternativa de programación a los desencadenadores DDL y al Seguimiento de SQL.  
  
## <a name="event-notifications-benefits"></a>Ventajas de las notificaciones de eventos  
 Las notificaciones de eventos se ejecutan asincrónicamente, fuera del ámbito de una transacción. Por consiguiente, a diferencia de los desencadenadores DDL, las notificaciones de eventos se pueden usar dentro de una aplicación de bases de datos para responder a eventos sin usar los recursos definidos por la transacción inmediata.  
  
 A diferencia del Seguimiento de SQL, las notificaciones de eventos se pueden usar para realizar una acción en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como respuesta a un evento de Seguimiento de SQL.  
  
 Los datos de eventos pueden ser usados por aplicaciones que se ejecutan junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar un seguimiento del progreso y tomar decisiones. Por ejemplo, la siguiente notificación de eventos envía un aviso a un servicio determinado cada vez que se emite una instrucción `ALTER TABLE` en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>Conceptos de las notificaciones de eventos  
 Cuando se crea una notificación de eventos, se abren una o más conversaciones de [!INCLUDE[ssSB](../../includes/sssb-md.md)] entre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el servicio de destino que se especifica. Normalmente, las conversaciones permanecen abiertas mientras existe la notificación de eventos como objeto de la instancia de servidores. En algunos casos de error, las conversaciones se pueden cerrar antes de que se quite la notificación de eventos. Esas conversaciones nunca se comparten entre notificaciones de eventos. Cada notificación de eventos tiene sus propias conversaciones exclusivas. Al finalizar una conversación explícitamente se impide que el servicio de destino reciba más mensajes y la conversación no se vuelve a abrir la próxima vez que se activa la notificación de eventos.  
  
 La información de eventos se proporciona al servicio [!INCLUDE[ssSB](../../includes/sssb-md.md)] como una variable de tipo **xml** que proporciona información acerca de cuándo se produce un evento, el objeto de la base de datos afectado, la instrucción de lote [!INCLUDE[tsql](../../includes/tsql-md.md)] implicada y otra información. Para obtener más información sobre el esquema XML producido por las notificaciones de eventos, vea [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md).  
  
### <a name="event-notifications-vs-triggers"></a>Notificaciones de eventos y Desencadenadores  
 En la siguiente tabla se comparan y contrastan los desencadenadores y las notificaciones de eventos.  
  
|Desencadenadores|Notificaciones de eventos|  
|--------------|-------------------------|  
|Los desencadenadores DML responden a los eventos deL lenguaje de manipulación de datos (DML). Los desencadenadores DDL responden a los eventos deL lenguaje de definición de datos (DDL).|Las notificaciones de eventos responden a los eventos DDL y a un subconjunto de eventos de Seguimiento de SQL.|  
|Los desencadenadores pueden ejecutar código administrado de Common Language Runtime (CLR) o Transact-SQL.|Las notificaciones de eventos no ejecutan código. En su lugar, envían mensajes **xml** a un servicio de Service Broker.|  
|Los desencadenadores se procesan sincrónicamente, en el ámbito de las transacciones que los activan.|Las notificaciones de eventos pueden procesarse de forma asincrónica y no se ejecutan en el ámbito de las transacciones que las activan.|  
|El consumidor de un desencadenador se une estrechamente al evento que lo activa.|El consumidor de una notificación de eventos se desliga del evento que lo activa.|  
|Los desencadenadores se deben procesar en el servidor local.|Las notificaciones de eventos se pueden procesar en un servidor remoto.|  
|Se pueden revertir los desencadenadores.|No se pueden revertir las notificaciones de eventos.|  
|Los nombres de desencadenador DML se encuentran en el ámbito de esquema. Los nombres de desencadenador DDL se encuentran en el ámbito de la base de datos o del servidor.|Los nombres de notificación de eventos se encuentran en el ámbito de la base de datos o del servidor. Las notificaciones de eventos en un evento QUEUE_ACTIVATION se encuentran en el ámbito de una cola específica.|  
|El mismo propietario posee los desencadenadores DML y las tablas en que se aplican.|El propietario de una notificación de eventos en una cola puede tener un propietario diferente que el objeto en el que se aplica.|  
|Los desencadenadores admiten la cláusula EXECUTE AS.|Las notificaciones de eventos no admiten la cláusula EXECUTE AS.|  
|Se puede capturar la información de eventos del desencadenador DDL mediante la función EVENTDATA, que devuelve un tipo de datos **xml** .|Las notificaciones de eventos envían información de eventos **xml** a un servicio de Service Broker. El formato de la información usa el mismo esquema que la función EVENTDATA.|  
|Los metadatos sobre los desencadenadores se encuentran en las vistas de catálogo **sys.triggers** y **sys.server_triggers** .|Los metadatos sobre las notificaciones de eventos se encuentran en las vistas de catálogo **sys.event_notifications** y **sys.server_event_notifications**.|  
  
### <a name="event-notifications-vs-sql-trace"></a>Notificaciones de eventos y Seguimiento de SQL  
 En la siguiente tabla se compara y contrasta el uso de notificaciones de eventos y de la Seguimiento de SQL para supervisar eventos de servidor.  
  
|Seguimiento de SQL|Notificaciones de eventos|  
|---------------|-------------------------|  
|Seguimiento de SQL no genera carga de rendimiento asociada con transacciones. El empaquetado de los datos es eficaz.|Existe una carga de rendimiento asociada con la creación de datos de eventos con formato XML y con el envío de notificaciones de eventos.|  
|Seguimiento de SQL puede supervisar y realizar un seguimiento de cualquier clase de evento.|Los notificaciones de eventos pueden supervisar un subconjunto de clases de eventos de seguimiento y también todos los eventos del lenguaje de definición de datos (DDL).|  
|Puede personalizar qué columnas de datos se crean en un evento de seguimiento.|El esquema de datos de eventos con formato XML devuelto por las notificaciones de eventos es fijo.|  
|Los eventos de seguimiento generados por DDL siempre se generan, independientemente de si la instrucción DDL se revierte.|Las notificaciones de eventos no se activan si el evento de la instrucción DDL correspondiente se revierte.|  
|La administración del flujo intermedio de los datos de eventos de seguimiento implica llenar y administrar archivos de seguimiento o tablas de seguimiento.|La administración intermedia de los datos de notificación de eventos se consigue automáticamente mediante las colas de Service Broker.|  
|Los seguimientos deben reiniciarse cada vez que se reinicia el servidor.|Después de registrarse, las notificaciones de eventos persisten en ciclos de servidor y participan en transacciones.|  
|Tras reiniciarse, la activación de los seguimientos no se puede controlar. Las horas de detención y filtrado se pueden usar para especificar cuándo se inician. Se obtiene acceso a los seguimientos sondeando el archivo de seguimientos correspondiente.|Las notificaciones de eventos se pueden controlar utilizando la instrucción WAITFOR sobre la cola que recibe el mensaje generado por la notificación de eventos. Se puede obtener acceso a ellas sondeando la cola.|  
|ALTER TRACE es el permiso mínimo necesario para crear un seguimiento. También se requiere el permiso para crear un archivo de seguimiento en el equipo correspondiente.|El permiso mínimo depende del tipo de notificación de eventos que se está creando. El permiso RECEIVE también es necesario en la cola correspondiente.|  
|Los seguimientos se pueden recibir remotamente.|Las notificaciones de eventos se pueden recibir remotamente.|  
|Los eventos de seguimiento se implementan utilizando procedimientos almacenados del sistema.|Las notificaciones de eventos se implementan mediante una combinación de instrucciones [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|Se puede obtener acceso a los datos de eventos de seguimiento mediante programación consultando la tabla de seguimiento correspondiente, analizando el archivo de seguimiento o usando la clase TraceReader de los objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO).|Se obtiene acceso a los datos de eventos mediante programación emitiendo XQuery sobre los datos de eventos con formato XML, o mediante las clases SMO Event.|  
  
## <a name="event-notification-tasks"></a>Tareas de las notificaciones de eventos  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear e implementar notificaciones de eventos.|[Implementar notificaciones de eventos](../../relational-databases/service-broker/implement-event-notifications.md)|  
|Describe cómo configurar la seguridad de diálogo de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para las notificaciones de evento que envían mensajes a un Service Broker en un servidor remoto.|[Configurar la seguridad de diálogo para notificaciones de eventos](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|Describe cómo devolver información acerca de las notificaciones de eventos.|[Obtener información sobre notificaciones de eventos](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Desencadenadores DML](../../relational-databases/triggers/dml-triggers.md)   
 [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
