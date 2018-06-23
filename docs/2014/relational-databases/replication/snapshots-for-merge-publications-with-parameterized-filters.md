---
title: Instantáneas para publicaciones de combinación con filtros con parámetros | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7aaa2f17f78fafb6f361b164807f37032e59cfd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200870"
---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>Instantáneas para publicaciones de combinación con filtros con parámetros
  Cuando se utilizan filtros de fila con parámetros en las publicaciones de combinación, la replicación inicializa cada suscripción con una instantánea en dos partes. Primero, se crea una instantánea de esquema que contiene todos los objetos necesarios para la replicación y el esquema de los objetos publicados, pero no los datos. Después, se inicializa cada suscripción con una instantánea que incluye los objetos y el esquema de la instantánea de esquema, y los datos que pertenecen a la partición de la suscripción. Si hay más de una suscripción que recibe una partición determinada (es decir, que reciben el mismo esquema y los mismos datos), la instantánea de esa partición se creará una sola vez; se inicializarán varias suscripciones con la misma instantánea. Para obtener más información acerca de los filtros de fila con parámetros, vea [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 Puede crear instantáneas para publicaciones con filtros con parámetros de las tres formas siguientes:  
  
-   Genere previamente las instantáneas para cada partición. Esta opción le permite controlar cuándo se generan las instantáneas.  
  
     También puede elegir que las instantáneas se actualicen de acuerdo con una programación. Los suscriptores nuevos que se suscriban a una partición para la que se ha creado una instantánea recibirán una instantánea actualizada.  
  
-   Permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronicen. Esta opción permite a los nuevos suscriptores sincronizarse sin la intervención de un administrador (el Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe estar ejecutando en el publicador para que se pueda generar la instantánea).  
  
    > [!NOTE]  
    >  Si el filtrado de uno o más artículos de la publicación produce particiones no superpuestas y únicas para cada suscripción, los metadatos se limpian cada vez que se ejecuta el Agente de mezcla. Esto significa que la instantánea con particiones expira antes. Cuando utilice esta opción, puede ser conveniente permitir a los suscriptores que inicien la generación y entrega de instantáneas. Para obtener más información acerca de las opciones de filtro, vea [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Genere manualmente una instantánea para cada suscriptor con el Agente de instantáneas. A continuación, el suscriptor deberá proporcionar la ubicación de la instantánea al Agente de mezcla para que pueda recuperar y aplicar la instantánea correcta.  
  
    > [!NOTE]  
    >  Esta opción se admite para la compatibilidad con versiones anteriores y no permite los recursos compartidos de instantáneas en FTP.  
  
 El enfoque más flexible es utilizar una combinación de opciones de instantáneas generadas previamente y solicitadas por el suscriptor: las instantáneas se generan previamente y se actualizan según una programación (por lo general, durante los períodos de menor actividad), pero un suscriptor puede generar su propia instantánea si se crea una suscripción que necesita una partición nueva.  
  
 Considere [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], que tiene un personal móvil que proporciona inventarios a las tiendas. Cada vendedor recibe una suscripción según su inicio de sesión, que recupera los datos de las tiendas a las que prestan servicio. El administrador genera previamente las instantáneas y las actualiza cada domingo. Ocasionalmente, se agrega al sistema un usuario nuevo que necesita datos para una partición que no tiene una instantánea disponible. El administrador también permite las instantáneas iniciadas por el suscriptor, con el fin de evitar situaciones en las que un suscriptor no puede suscribirse a la publicación porque la instantánea aún no está disponible. Cuando el nuevo suscriptor se conecta por primera vez, se genera la instantánea para la partición especificada y se aplica al suscriptor (debe ejecutarse el Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el publicador para que se pueda generar la instantánea).  
  
 Para crear una instantánea para una publicación con filtros con parámetros, vea [Crear una instantánea para una publicación de mezcla con filtros con parámetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="security-settings-for-the-snapshot-agent"></a>Configuración de seguridad para el Agente de instantáneas  
 El Agente de instantáneas crea instantáneas para cada partición. Para las instantáneas generadas previamente y las solicitadas por un suscriptor, el agente se ejecuta y establece conexiones con las credenciales especificadas cuando se creó el trabajo del Agente de instantáneas para la publicación (el trabajo lo crea el Asistente para nueva publicación o **sp_addpublication_snapshot**). Para cambiar las credenciales, utilice **sp_changedynamicsnapshot_job**. Para obtener más información, consulte [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md)  
  
  
