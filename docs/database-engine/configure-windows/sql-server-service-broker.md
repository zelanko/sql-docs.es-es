---
title: SQL Server Service Broker | Microsoft Docs
description: Obtenga información sobre Service Broker. Vea cómo proporciona compatibilidad nativa para la mensajería en el Motor de base de datos de SQL Server y Azure SQL Managed Instance.
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 2841f36d3f9e4498763f6b0862e2fa0cfaa2e4a9
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87863413"
---
# <a name="service-broker"></a>Service Broker
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] proporciona compatibilidad nativa con la mensajería y la puesta en cola de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index). Los desarrolladores pueden crear fácilmente aplicaciones complejas que usan los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para comunicarse entre distintas bases de datos y compilar aplicaciones distribuidas y confiables.  
  
## <a name="when-to-use-service-broker"></a>Cuándo utilizar Service Broker

 Utilice componentes de Service Broker para implementar funcionalidades nativas de procesamiento de mensajes asincrónicos en bases de datos. Los desarrolladores de aplicaciones que usan [!INCLUDE[ssSB](../../includes/sssb-md.md)] pueden distribuir las cargas de trabajo de datos en varias bases de datos sin tener que programar complejas funciones internas de comunicación y mensajería. Service Broker reduce el trabajo de desarrollo y realización de pruebas, ya que [!INCLUDE[ssSB](../../includes/sssb-md.md)] controla las vías de comunicación del contexto de una conversación. También aumenta el rendimiento. Por ejemplo, las bases de datos front-end que admiten sitios web pueden grabar información y enviar tareas con muchos procesos a colas de bases de datos back-end. [!INCLUDE[ssSB](../../includes/sssb-md.md)] asegura que todas las tareas se administran en el contexto de transacciones para garantizar confiabilidad y coherencia técnica.  
  
## <a name="overview"></a>Información general

  Service Broker es un marco de trabajo de entrega de mensajes que le permite crear aplicaciones nativas orientadas a servicios en bases de datos. A diferencia de las funcionalidades clásicas de procesamiento de consultas que leen constantemente los datos de las tablas y los procesan durante el ciclo de vida de la consulta, en las aplicaciones orientadas a servicios se tienen servicios de base de datos que intercambian los mensajes. Cada servicio tiene una cola en la que se colocan los mensajes hasta que se procesan.
  
![Service Broker](media/service-broker.png)
  
  Los mensajes de las colas se pueden capturar con el comando `RECEIVE` de Transact-SQL o mediante el procedimiento de activación que se llamará cada vez que el mensaje llegue a la cola.
  
### <a name="creating-services"></a>Creación de servicios
 
  Los servicios de base de datos se crean mediante la instrucción [CREATE SERVICE](../../t-sql/statements/create-service-transact-sql.md) de Transact-SQL. El servicio puede asociarse a la cola de mensajes creada mediante la instrucción [CREATE QUEUE](../../t-sql/statements/create-queue-transact-sql.md):
  
```sql
CREATE QUEUE dbo.ExpenseQueue;
GO
CREATE SERVICE ExpensesService
    ON QUEUE dbo.ExpenseQueue; 
```

### <a name="sending-messages"></a>Envío de mensajes
  
  Los mensajes se envían en la conversación entre los servicios con la instrucción [SEND](../../t-sql/statements/send-transact-sql.md) de Transact-SQL. Una conversación es un canal de comunicación que se establece entre los servicios con la instrucción `BEGIN DIALOG` de Transact-SQL. 
  
```sql
DECLARE @dialog_handle UNIQUEIDENTIFIER;

BEGIN DIALOG @dialog_handle  
FROM SERVICE ExpensesClient  
TO SERVICE 'ExpensesService';  
  
SEND ON CONVERSATION @dialog_handle (@Message) ;  
```
   El mensaje se enviará a la `ExpenssesService` y se colocará en `dbo.ExpenseQueue`. Dado que no hay ningún procedimiento de activación asociado a esta cola, el mensaje permanecerá en la cola hasta que alguien lo lea.

### <a name="processing-messages"></a>Procesar mensajes

   Los mensajes que están colocados en la cola se pueden seleccionar mediante una consulta `SELECT` estándar. La instrucción `SELECT` no modificará la cola y quitará los mensajes. Para leer y extraer los mensajes de la cola, puede usar la instrucción [RECEIVE](../../t-sql/statements/receive-transact-sql.md) de Transact-SQL.

```sql
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue; 
```

  Una vez que procesa todos los mensajes de la cola, debe cerrar la conversación con la instrucción [END CONVERSATION](../../t-sql/statements/end-conversation-transact-sql.md) de Transact-SQL.

## <a name="where-is-the-documentation-for-service-broker"></a>¿Dónde está la documentación de Service Broker?  
 La documentación de referencia para [!INCLUDE[ssSB](../../includes/sssb-md.md)] se incluye en la documentación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esta documentación de referencia incluye las secciones siguientes:  
  
-   [Instrucciones de lenguaje de definición de datos &#40;DDL&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/statements.md) para las instrucciones CREATE, ALTER y DROP  
  
-   [Instrucciones de Service Broker](../../t-sql/statements/service-broker-statements.md)  
  
-   [Vistas de catálogo de Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Vistas de administración dinámica relacionadas con Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [Utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 Vea la [documentación publicada previamente](https://go.microsoft.com/fwlink/?LinkId=231312) para conocer los conceptos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] y las tareas de desarrollo y administración. Esta documentación no se reproduce en la documentación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] debido al pequeño número de cambios realizados en [!INCLUDE[ssSB](../../includes/sssb-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="whats-new-in-service-broker"></a>Novedades de Service Broker  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no se introducen cambios significativos.  Los siguientes cambios se incluyeron por primera vez en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

### <a name="service-broker-and-azure-sql-managed-instance"></a>Service Broker y Azure SQL Managed Instance

- No se admite la opción de Service Broker entre instancias 
 - `sys.routes` -Requisito previo: seleccione la dirección desde sys.routes. La dirección debe ser LOCAL en todas las rutas. Consulte [sys.routes](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md).
 - `CREATE ROUTE`: no se puede usar `CREATE ROUTE` con un valor de `ADDRESS` distinto de `LOCAL`. Consulte [CREATE ROUTE](https://docs.microsoft.com/sql/t-sql/statements/create-route-transact-sql).
 - `ALTER ROUTE` no se puede usar `ALTER ROUTE` con `ADDRESS` que no sea `LOCAL`. Consulte [ALTER ROUTE](../../t-sql/statements/alter-route-transact-sql.md).  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>Se pueden enviar mensajes a varios servicios de destino (multidifusión)  
 La sintaxis de la instrucción de [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) se ha ampliado para habilitar la multidifusión admitiendo varios identificadores de conversación.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>Las colas exponen la hora de puesta en cola del mensaje  
 Las colas tienen una nueva columna, **message_enqueue_time**, que muestra el tiempo que un mensaje ha estado en la cola.  
  
### <a name="poison-message-handling-can-be-disabled"></a>El control de mensajes dudosos se puede deshabilitar  
 Las instrucciones [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) y [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) ahora pueden habilitar o deshabilitar el control de mensajes dudosos agregando la cláusula `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)`. La vista de catálogo **sys.service_queues** tiene ahora la columna **is_poison_message_handling_enabled** para indicar si el control de mensajes dudosos está habilitado o deshabilitado.  
  
### <a name="always-on-support-in-service-broker"></a>Compatibilidad con AlwaysOn de Service Broker  
 Para más información, vea [Service Broker con grupos de disponibilidad AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md).  
  
  
## <a name="next-steps"></a>Pasos siguientes

El uso más común de Service Broker es para [las notificaciones de eventos](../../relational-databases/service-broker/event-notifications.md). Aprenda a [implementar notificaciones de eventos](../../relational-databases/service-broker/implement-event-notifications.md) o [configurar seguridad de diálogo](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md), o bien [obtenga más información](../../relational-databases/service-broker/get-information-about-event-notifications.md). 


