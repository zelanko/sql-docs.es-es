---
title: "Instantáneas para publicaciones de combinación con filtros con parámetros | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83e1c3bcb6cc4a435f3db4b3e96812a0c308c8b9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>Instantáneas para publicaciones de combinación con filtros con parámetros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Cuando se utilizan filtros de fila con parámetros en las publicaciones de combinación, la replicación inicializa cada suscripción con una instantánea en dos partes. Primero, se crea una instantánea de esquema que contiene todos los objetos necesarios para la replicación y el esquema de los objetos publicados, pero no los datos. Después, se inicializa cada suscripción con una instantánea que incluye los objetos y el esquema de la instantánea de esquema, y los datos que pertenecen a la partición de la suscripción. Si hay más de una suscripción que recibe una partición determinada (es decir, que reciben el mismo esquema y los mismos datos), la instantánea de esa partición se creará una sola vez; se inicializarán varias suscripciones con la misma instantánea. Para obtener más información acerca de los filtros de fila con parámetros, vea [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Puede crear instantáneas para publicaciones con filtros con parámetros de las tres formas siguientes:  
  
-   Genere previamente las instantáneas para cada partición. Esta opción le permite controlar cuándo se generan las instantáneas.  
  
     También puede elegir que las instantáneas se actualicen de acuerdo con una programación. Los suscriptores nuevos que se suscriban a una partición para la que se ha creado una instantánea recibirán una instantánea actualizada.  
  
-   Permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronicen. Esta opción permite a los nuevos suscriptores sincronizarse sin la intervención de un administrador (el Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe estar ejecutando en el publicador para que se pueda generar la instantánea).  
  
    > [!NOTE]  
    >  Si el filtrado de uno o más artículos de la publicación produce particiones no superpuestas y únicas para cada suscripción, los metadatos se limpian cada vez que se ejecuta el Agente de mezcla. Esto significa que la instantánea con particiones expira antes. Cuando utilice esta opción, puede ser conveniente permitir a los suscriptores que inicien la generación y entrega de instantáneas. Para obtener más información acerca de las opciones de filtro, vea [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Genere manualmente una instantánea para cada suscriptor con el Agente de instantáneas. A continuación, el suscriptor deberá proporcionar la ubicación de la instantánea al Agente de mezcla para que pueda recuperar y aplicar la instantánea correcta.  
  
    > [!NOTE]  
    >  Esta opción se admite para la compatibilidad con versiones anteriores y no permite los recursos compartidos de instantáneas en FTP.  
  
 El enfoque más flexible es utilizar una combinación de opciones de instantáneas generadas previamente y solicitadas por el suscriptor: las instantáneas se generan previamente y se actualizan según una programación (por lo general, durante los períodos de menor actividad), pero un suscriptor puede generar su propia instantánea si se crea una suscripción que necesita una partición nueva.  
  
 Considere [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], que tiene un personal móvil que proporciona inventarios a las tiendas. Cada vendedor recibe una suscripción según su inicio de sesión, que recupera los datos de las tiendas a las que prestan servicio. El administrador genera previamente las instantáneas y las actualiza cada domingo. Ocasionalmente, se agrega al sistema un usuario nuevo que necesita datos para una partición que no tiene una instantánea disponible. El administrador también permite las instantáneas iniciadas por el suscriptor, con el fin de evitar situaciones en las que un suscriptor no puede suscribirse a la publicación porque la instantánea aún no está disponible. Cuando el nuevo suscriptor se conecta por primera vez, se genera la instantánea para la partición especificada y se aplica al suscriptor (debe ejecutarse el Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el publicador para que se pueda generar la instantánea).  
  
 Para crear una instantánea para una publicación con filtros con parámetros, vea [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="security-settings-for-the-snapshot-agent"></a>Configuración de seguridad para el Agente de instantáneas  
 El Agente de instantáneas crea instantáneas para cada partición. Para las instantáneas generadas previamente y las solicitadas por un suscriptor, el agente se ejecuta y establece conexiones con las credenciales especificadas cuando se creó el trabajo del Agente de instantáneas para la publicación (el trabajo lo crea el Asistente para nueva publicación o **sp_addpublication_snapshot**). Para cambiar las credenciales, utilice **sp_changedynamicsnapshot_job**. Para obtener más información, consulte [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
