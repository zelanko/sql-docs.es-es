---
title: "Propiedades de la publicaci&#243;n, Opciones de suscripci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.subscriptionoptions.f1"
ms.assetid: 31abd605-b273-419d-86df-d0ecf539a507
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Propiedades de la publicaci&#243;n, Opciones de suscripci&#243;n
  La página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación** permite ver y establecer propiedades a nivel de publicación asociadas con suscripciones. Las propiedades se agrupan en las siguientes categorías:  
  
-   Propiedades que se aplican a todas las publicaciones.  
  
-   Propiedades que se aplican a las publicaciones transaccionales y de instantáneas (incluidas las que permiten suscripciones de actualización).  
  
-   Propiedades que se aplican a las publicaciones de combinación.  
  
> [!NOTE]  
>  Algunas propiedades son de solo lectura; los motivos se tratan en las descripciones de propiedad de este tema. Algunos cambios de propiedad requieren una nueva instancia para la publicación, y otros también requieren la reinicialización de todas las suscripciones. Para obtener más información, consulte [Propiedades de artículo y publicación de cambio](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Opciones para todas las publicaciones  
  
### Creación y sincronización  
 **Permitir suscripciones anónimas**  
 Determina si se permiten suscripciones de extracción anónimas. Se admiten suscripciones anónimas para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEWEd2005](../../includes/ssewed2005-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssMobileEd2005](../../includes/ssmobileed2005-md.md)]y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows CE. Para utilizar esta opción en publicaciones transaccionales y de instantáneas, la opción **Instantánea siempre visible** debe establecerse en **True**.  
  
 **Base de datos de suscripciones adjuntables**  
 Determina si se pueden crear suscripciones adjuntando una copia de una base de datos de suscripciones (requiere que la opción **instantáneas estén siempre disponibles** está establecido en **True** para publicaciones de instantáneas y transaccionales).  
  
> [!IMPORTANT]  
>  Las suscripciones adjuntables no estarán disponibles en futuras versiones. La característica ha quedado desusada.  
  
 **Permitir suscripciones de extracción**  
 Determina si se permite a los suscriptores crear suscripciones de extracción en esta publicación. Para obtener más información, consulte [suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md).  
  
### Replicación de esquemas  
 **Replicar cambios de esquema**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Determina si se replican cambios de esquema (como agregar una columna a una tabla o cambiar el tipo de datos de una columna) en objetos publicados. Para obtener más información, consulte [hacer cambios de esquema en bases de datos de publicación](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Opciones de publicaciones transaccionales y de instantáneas  
  
### Creación y sincronización  
 **Agente de distribución independiente**  
 Determina si se utiliza un agente que es independiente de otras publicaciones desde esta base de datos. Esta opción es de solo lectura; se establece en **True** de forma predeterminada para las publicaciones crean con el Asistente para nueva publicación y no se puede cambiar después de crear la publicación. Para obtener más información, consulte [administración del agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 **Instantánea siempre visible**  
 Determina si los archivos de instantáneas se crean cada vez que se ejecuta el agente de instantáneas (requiere **agente de distribución independiente**). Esta opción es de solo lectura; se establece en **True** Si selecciona **crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones** en la **agente de instantáneas** página del Asistente de publicación nuevo (predeterminado). Para obtener más información, consulte [crear y aplicar la instantánea](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 **Permitir inicialización desde archivos de copia de seguridad**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Determina si se permite utilizar archivos de copia de seguridad para inicializar suscripciones. Para obtener más información, consulte [inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Permitir suscriptores que no sean de SQL**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Determina si la publicación admite suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Establecer esta opción en **True** establece otras propiedades de publicación para admitir no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores. Esta opción es de sólo lectura si existen suscripciones; no se puede establecer **True** Si **Permitir suscripciones de actualización inmediata**, **Permitir de actualización en cola**, o **Permitir suscripciones punto a punto** se establece en **True**. Para obtener más información, consulte [suscriptores no SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
### Transformación de datos  
 **Permitir transformaciones de datos**  
 Determina si se deben utilizar los Servicios de transformación de datos (DTS) para transformar los datos antes de distribuirlos a un suscriptor. Esta opción es de solo lectura; las transformaciones de datos solo se pueden habilitar si una publicación se crea utilizando procedimientos almacenados.  
  
> [!IMPORTANT]  
>  Las suscripciones de transformación no estarán disponibles en futuras versiones. La característica ha quedado desusada.  
  
### Replicación punto a punto  
 **Permitir suscripciones punto a punto**  
 Se aplica solamente a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Determina si la publicación admite la replicación punto a punto. Establecer esta opción en **True** establece otras propiedades de publicación para admitir la replicación punto a punto. Esta opción es de solo lectura si existen suscripciones. Esta opción no puede establecerse en **True** Si **Permitir suscripciones de actualización inmediata** o **en cola de permitir suscripciones de actualización**, o **Permitir suscriptores que no sean de SQL Server** está establecido en **True**. Para obtener más información, consulte [replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 **Permitir detección de conflictos de replicación punto a punto**  
 Se aplica solamente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. Especifica si la detección de conflictos está habilitada para esta publicación. Para utilizar la detección de conflictos, todos los nodos deben estar ejecutando [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o una versión posterior, y debe haberse habilitado la detección para todos los ellos. Para utilizar la detección de conflictos también debe especificar un valor para **Identificador del autor del mismo nivel**. Para obtener más información, consulte [la detección de conflictos de replicación punto a punto](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md).  
  
 **Identificador del autor del mismo nivel**  
 Se aplica solamente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. Especifica un Id. para un nodo en una topología punto a punto. Este identificador se utiliza para la detección de conflictos si **Permitir detección de conflictos de peer-to-peer** está establecido en **True**. Especifique un id. positivo distinto de cero que no se haya utilizado jamás en la topología. Para obtener una lista de identificadores que ya se han utilizado, consulte la [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) tabla del sistema.  
  
### Suscripciones actualizables  
 **Permitir suscripciones de actualización inmediata**  
 Determina si los cambios de datos del suscriptor se pueden replicar inmediatamente en el publicador. Esta opción es de solo lectura; las suscripciones de actualización solo se pueden habilitar cuando se crea la publicación. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Permitir suscripciones de actualización en cola**  
 Determina si los cambios de datos del suscriptor se pueden poner en cola y replicar más tarde en el publicador. Esta opción es de solo lectura; las suscripciones de actualización solo se pueden habilitar cuando se crea la publicación. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 **Informar de conflictos centralmente**  
 Determina si se debe notificar los cambios de datos conflictivos sólo en el publicador o en el publicador y el suscriptor (requiere la opción **Permitir de actualización en cola**). Esta opción es de solo lectura; se establece en **True** de forma predeterminada para las publicaciones crean con el Asistente para nueva publicación y no se puede cambiar después de crear la publicación. El valor **True** significa que los conflictos se notifican solo al publicador. Los conflictos solo pueden verse donde se notifican.  
  
 **Directiva de resolución de conflictos**  
 Especifica la acción que se realizará cuando un cambio del suscriptor entra en conflicto con un cambio del publicador (requiere la opción **Permitir de actualización en cola**). Para más información, consulte [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md).  
  
 **Tipo de cola**  
 Determina si se utiliza un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cola o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) para poner en cola los cambios en el suscriptor hasta que se pueden aplicar al publicador (requiere la opción **Permitir de actualización en cola**). Esta opción solo es relevante para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]; las versiones posteriores siempre utilizan tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las colas.  
  
## Opciones para publicaciones de combinación  
  
### Informes de conflictos  
 **Informar de conflictos centralmente**  
 Determina si se notifican los cambios de datos conflictivos solo en el publicador o en el publicador y el suscriptor. Esta opción es de solo lectura; se establece en **True** de forma predeterminada para las publicaciones crean con el Asistente para nueva publicación y no se puede cambiar después de crear la publicación. El valor **True** significa que los conflictos se notifican solo al publicador. Los conflictos solo pueden verse donde se notifican. Para obtener más información, vea la sección "Ver conflictos" de [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### Filtrar  
 **Permitir filtros con parámetros**  
 Se establece en función de si una publicación utiliza filtros con parámetros. Esta opción siempre es de solo lectura. Para más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Validar suscriptores**  
 Determina qué funciones se utilizan al validar si un suscriptor tiene la partición correcta de datos. Debe utilizarse una coma para separar múltiples valores. Para obtener más información, consulte [validar la información de partición para un suscriptor de mezcla](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Calcular particiones previamente**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Determina si se debe optimizar la sincronización calculando previamente las filas de datos que pertenecen a cada partición. Tiene como valor predeterminado **True** si la publicación cumple los criterios de las particiones calculadas previamente. Para obtener más información, consulte [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
 **Optimizar sincronización**  
 Determina si se optimiza el proceso de mezcla almacenando metadatos adicionales en cada suscriptor. Esta optimización se ha sustituido con las particiones calculadas previamente; la opción **Optimizar sincronización** solo es relevante si la opción **Calcular particiones previamente** está establecida en **False**. Para más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
### Procesos de mezcla  
 **Limitar procesos simultáneos**  
 Determina si se limita el número de Agentes de mezcla que se pueden ejecutar al mismo tiempo. Normalmente se utiliza si una publicación tiene un gran número de suscripciones de inserción que pueden sincronizarse simultáneamente.  
  
 **Máximo de procesos simultáneos**  
 El número máximo de agentes de mezcla que se pueden ejecutar al mismo tiempo (requiere **Limitar procesos simultáneos**). Si el número de agentes que se están sincronizando supera el máximo, los agentes se ponen en cola hasta que el número es inferior al máximo.  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  