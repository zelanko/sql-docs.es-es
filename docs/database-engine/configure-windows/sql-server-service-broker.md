---
title: SQL Server Service Broker | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
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
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 757ee407d0831734b7c55b9e1b8b5a20e91d042a
ms.sourcegitcommit: d8e3da95f5a2b7d3997d63c53e722d494b878eec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2018
ms.locfileid: "44171817"
---
# <a name="sql-server-service-broker"></a>SQL Server Service Broker
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] proporciona compatibilidad nativa para las aplicaciones de mensajería y de cola en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. De este modo, resulta más fácil para los desarrolladores crear aplicaciones complejas que usan los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para la comunicación entre bases de datos distintas. Los desarrolladores pueden usar [!INCLUDE[ssSB](../../includes/sssb-md.md)] para crear con facilidad aplicaciones distribuidas y confiables.  
  
 Los desarrolladores de aplicaciones que usan [!INCLUDE[ssSB](../../includes/sssb-md.md)] pueden distribuir las cargas de trabajo de datos en varias bases de datos sin tener que programar complejas funciones internas de comunicación y mensajería. Así se reduce el trabajo de programación y realización de pruebas, ya que [!INCLUDE[ssSB](../../includes/sssb-md.md)] controla las vías de comunicación del contexto de una conversación. También aumenta el rendimiento. Por ejemplo, las bases de datos front-end que admiten sitios web pueden grabar información y enviar tareas con muchos procesos a colas de bases de datos back-end. [!INCLUDE[ssSB](../../includes/sssb-md.md)] asegura que todas las tareas se administran en el contexto de transacciones para garantizar confiabilidad y coherencia técnica.  
  
## <a name="where-is-the-documentation-for-service-broker"></a>¿Dónde está la documentación de Service Broker?  
 La documentación de referencia para [!INCLUDE[ssSB](../../includes/sssb-md.md)] se incluye en la documentación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esta documentación de referencia incluye las secciones siguientes:  
  
-   [Instrucciones de lenguaje de definición de datos &#40;DDL&#41; &#40;Transact-SQL&#41;](~/mdx/mdx-data-definition-statements-mdx.md) para las instrucciones CREATE, ALTER y DROP  
  
-   [Instrucciones de Service Broker](../../t-sql/statements/service-broker-statements.md)  
  
-   [Vistas de catálogo de Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Vistas de administración dinámica relacionadas con Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [Utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 Vea la [documentación publicada previamente](http://go.microsoft.com/fwlink/?LinkId=231312) para conocer los conceptos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] y las tareas de desarrollo y administración. Esta documentación no se reproduce en la documentación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] debido al pequeño número de cambios realizados en [!INCLUDE[ssSB](../../includes/sssb-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="whats-new-in-service-broker"></a>Novedades de Service Broker  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no se introducen cambios significativos.  Los siguientes cambios se incluyeron por primera vez en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

### <a name="service-broker-and-azure-sql-database-managed-instance"></a>Service Broker e Instancia administrada de Azure SQL Database

- No se admite la opción de Service Broker entre instancias 
 - `sys.routes` -Requisito previo: seleccione la dirección desde sys.routes. La dirección debe ser LOCAL en todas las rutas. Consulte [sys.routes](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md).
 - `CREATE ROUTE` -no puede usar `CREATE ROUTE` con `ADDRESS` que no sea `LOCAL`. Consulte [CREATE ROUTE](https://docs.microsoft.com/sql/t-sql/statements/create-route-transact-sql).
 - `ALTER ROUTE` no se puede usar `ALTER ROUTE` con `ADDRESS` que no sea `LOCAL`. Consulte [ALTER ROUTE](../../t-sql/statements/alter-route-transact-sql.md).  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>Se pueden enviar mensajes a varios servicios de destino (multidifusión)  
 La sintaxis de la instrucción de [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) se ha ampliado para habilitar la multidifusión admitiendo varios identificadores de conversación.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>Las colas exponen la hora de puesta en cola del mensaje  
 Las colas tienen una nueva columna, **message_enqueue_time**, que muestra el tiempo que un mensaje ha estado en la cola.  
  
### <a name="poison-message-handling-can-be-disabled"></a>El control de mensajes dudosos se puede deshabilitar  
 Las instrucciones [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) y [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) ahora pueden habilitar o deshabilitar el control de mensajes dudosos agregando la cláusula `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)`. La vista de catálogo **sys.service_queues** tiene ahora la columna **is_poison_message_handling_enabled** para indicar si el control de mensajes dudosos está habilitado o deshabilitado.  
  
### <a name="always-on-support-in-service-broker"></a>Compatibilidad con AlwaysOn de Service Broker  
 Para más información, vea [Service Broker con grupos de disponibilidad AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md).  
  
  

