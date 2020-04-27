---
title: Replicación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be03754ea8eeb61d838357667da6e37e1be6bc31
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62626160"
---
# <a name="sql-server-replication"></a>Replicación de SQL Server
  La replicación es un conjunto de tecnologías destinadas a la copia y distribución de datos y objetos de base de datos desde una base de datos a otra, para luego sincronizar ambas bases de datos y mantener su coherencia. La replicación permite distribuir datos entre diferentes ubicaciones y entre usuarios remotos o móviles mediante redes locales y de área extensa, conexiones de acceso telefónico, conexiones inalámbricas e Internet.  
  
 La replicación transaccional se usa normalmente en escenarios servidor a servidor que requieren un alto rendimiento, como por ejemplo, la mejora de la escalabilidad y la disponibilidad, el almacenamiento de datos y la creación de informes, la integración de datos procedentes de varios sitios, la integración de datos heterogéneos, y la descarga del procesamiento por lotes. La replicación de mezcla se ha diseñado principalmente para las aplicaciones móviles o de servidores distribuidos que pueden encontrarse con conflictos de datos. Los escenarios más frecuentes son: el intercambio de datos con usuarios móviles, las aplicaciones de punto de venta (POS) a consumidores, y la integración de datos de varios sitios. La replicación de instantáneas se usa para proporcionar el conjunto de datos inicial para la replicación transaccional y de mezcla; también se puede usar cuando está indicada una actualización completa de los datos. Con estos tres tipos de replicación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un sistema eficaz y flexible para la sincronización de datos en toda la organización. La replicación en SQLCE 3.5 y SQLCE 4.0 se admite tanto en [!INCLUDE[win8srv](../../includes/win8srv-md.md)] como en [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 Como alternativa a la replicación, puede sincronizar bases de datos mediante Microsoft Sync Framework. Sync Framework incluye componentes y una API intuitiva y flexible que facilitan la sincronización entre bases de datos de SQL Server, SQL Server Express, SQL Server Compact y SQL Azure. Sync Framework también incluye clases que se pueden adaptar para sincronizar entre una base de datos de SQL Server y cualquier otra base de datos compatible con ADO.NET. Para obtener documentación detallada de los componentes de sincronización de base de datos de Sync Framework, vea [Sincronizar bases de datos](https://go.microsoft.com/fwlink/?LinkId=209079). Para obtener información general sobre Sync Framework, vea el [Centro para desarrolladores de Microsoft Sync Framework](https://go.microsoft.com/fwlink/?LinkId=209078). Para obtener una comparación entre Sync Framework y la replicación de mezcla, vea [Información general y escenarios](https://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  

## <a name="whats-new"></a>Novedades 
- En SQL Server 2017 no se han presentado nuevas características importantes para la replicación de SQL Server. 
- En SQL Server 2016 no se han presentado nuevas características importantes para la replicación de SQL Server. 

Para obtener información sobre la compatibilidad con versiones anteriores, vea [Compatibilidad con versiones anteriores de replicación](replication-backward-compatibility.md). 


 ## <a name="replication-security"></a>Seguridad de la replicación
  
-   [Ver y modificar la configuración de seguridad de la replicación](security/view-and-modify-replication-security-settings.md)  
-   [Administrar inicios de sesión en la lista de acceso a la publicación](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>Publicación y distribución  
  
-   [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)   
-   [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
-   [Deshabilitar la publicación y la distribución](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>Publicaciones y artículos 
  
-   [Create a Publication](publish/create-a-publication.md) (Creación de una publicación)    
-   [Definir un artículo](publish/define-an-article.md)   
-   [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
-   [er y modificar las propiedades de un artículo](publish/view-and-modify-article-properties.md)    
-   [Eliminar una publicación](publish/delete-a-publication.md)   
-   [Eliminar un artículo](publish/delete-an-article.md)    
-   [Crear una publicación a partir de una base de datos de Oracle](publish/create-a-publication-from-an-oracle-database.md)   
-   [Establecer el período de expiración para las suscripciones](publish/set-the-expiration-period-for-subscriptions.md)  
-   [Especificar opciones de esquema](publish/specify-schema-options.md)  
-   [Replicación de cambios de esquema](publish/replicate-schema-changes.md)    
-   [Administrar columnas de identidad](publish/manage-identity-columns.md)   
-   [Establecer el nivel de compatibilidad para publicaciones de mezcla](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opciones de instantánea  
  
-   [Configurar propiedades de instantáneas](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [Entrega de una instantánea a través de FTP](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>Filtrado de datos  
  
-   [Definir y modificar un filtro de columna](publish/define-and-modify-a-column-filter.md)    
-   [Definir y modificar un filtro de fila estático](publish/define-and-modify-a-static-row-filter.md)    
-   [Definición y modificación de un filtro de fila con parámetros para un artículo de mezcla](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [Optimizar los filtros de fila con parámetros](publish/optimize-parameterized-row-filters.md)    
-   [Definir y modificar un filtro de combinación entre artículos de mezcla](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opciones de la replicación transaccional  
  
-   [Establecer el método de propagación para cambios de datos en artículos transaccionales](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [Habilitar suscripciones actualizables para publicaciones transaccionales](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opciones de la replicación de mezcla  
  
-   [Definir una relación de registros lógicos entre artículos de tabla de mezcla](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [Especificar propiedades de replicación de mezcla](publish/specify-merge-replication-properties.md)    
-   [Especificar un solucionador de artículos de mezcla](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>Administración de suscripciones  
  
-   [Crear una suscripción de extracción](create-a-pull-subscription.md)    
-   [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md) (Ver y modificar las propiedades de una suscripción de extracción)    
-   [Eliminar una suscripción de extracción](delete-a-pull-subscription.md)    
-   [Create a Push Subscription](create-a-push-subscription.md) (Creación de una suscripción de inserción)   
-   [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md)   
-   [Eliminar una suscripción de inserción](delete-a-push-subscription.md)   
-   [Especificar programaciones de sincronización](specify-synchronization-schedules.md)    
-   [Crear una suscripción actualizable en una publicación transaccional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [Crear una suscripción para un suscriptor que no sea de SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>Sincronización de suscripciones  
  
-   [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)   
-   [Crear una instantánea para una publicación de mezcla con filtros con parámetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [Inicializar una suscripción transaccional desde una copia de seguridad](initialize-a-transactional-subscription-from-a-backup.md)    
-   [Inicializar una suscripción manualmente](initialize-a-subscription-manually.md)    
-   [Sincronizar una suscripción de extracción](synchronize-a-pull-subscription.md)    
-   [Sincronizar una suscripción de inserción](synchronize-a-push-subscription.md)   
-   [Reinicializar una suscripción](reinitialize-a-subscription.md)    
-   [Ejecución de scripts durante la sincronización](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [Implementar un controlador de lógica de negocios para un artículo de mezcla](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [Depurar un controlador de lógica de negocios &#40;programación de la replicación&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administeration"></a>Administración de 
  
-   [Trabajar con perfiles del Agente de replicación](agents/work-with-replication-agent-profiles.md)   
-   [Validar datos en el suscriptor](validate-data-at-the-subscriber.md)    
-   [Administrar particiones para una publicación de mezcla mediante filtros con parámetros](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [Carga masiva de datos en tablas en una publicación de mezcla](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [Limpiar metadatos de mezcla](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [Realizar una actualización ficticia de un artículo de mezcla](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [Ver comandos replicados y otra información en la base de datos de distribución](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Habilitar copias de seguridad coordinadas para la replicación transaccional](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [Administrar una topología punto a punto](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [Poner en modo inactivo una topología de replicación](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [Actualizar scripts de replicación](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>Supervisión
  
-   [Permitir el uso del Monitor de replicación a los usuarios que no son administradores](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [Supervisar la replicación mediante programación](monitor/programmatically-monitor-replication.md)    
-   [Ver comandos replicados y otra información en la base de datos de distribución](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Ver información de conflictos para publicaciones de mezcla](view-conflict-information-for-merge-publications.md) 
-   [Medir la latencia y validar las conexiones de la replicación transaccional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  