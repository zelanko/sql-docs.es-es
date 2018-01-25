---
title: "Información general del modelo de publicación de replicación | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2016
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
- replication [SQL Server], publishing model
- subscriptions [SQL Server replication], about subscriptions
- articles [SQL Server replication]
- publications [SQL Server replication]
- Publishers [SQL Server replication], about Publishers
- Subscribers [SQL Server replication]
- Distributors [SQL Server replication], about Distributors
- Subscribers [SQL Server replication], about Subscribers
- articles [SQL Server replication], about articles
- publications [SQL Server replication], about publications
- Distributors [SQL Server replication]
ms.assetid: b9567832-e6a8-45b2-a3ed-ea12aa002f4b
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 63243f524fa4b94c4dfa535b533dbef87dd3a41c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="replication-publishing-model-overview"></a>Información general del modelo de publicación de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La replicación utiliza una metáfora del sector editorial para representar los componentes de una topología de replicación, como el publicador, el distribuidor, los suscriptores, las publicaciones, los artículos y las suscripciones. Resulta útil pensar en la replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como si fuera una revista:  
  
-   El publicador (editor) de una revista produce una o más publicaciones.  
  
-   Una publicación contiene artículos.  
  
-   El publicador distribuye la revista directamente o a través de un distribuidor.  
  
-   Los suscriptores reciben las publicaciones a las que se han suscrito.  
  
 Aunque la metáfora de la revista es útil para comprender la replicación, es importante señalar que la replicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye funciones que no están representadas en esta metáfora, en particular, la posibilidad de que un suscriptor realice actualizaciones y de que un publicador envíe cambios incrementales a los artículos de una publicación.  
  
 Una *topología de replicación* define la relación entre los servidores y las copias de los datos, y aclara la lógica que determina cómo fluyen los datos entre los servidores. Hay varios procesos de replicación (denominados *agentes*) que son responsables de copiar y mover los datos entre el publicador y los suscriptores. En la siguiente ilustración se muestra información general acerca de los componentes y procesos que participan en la replicación.  
  
 ![Componentes de replicación y flujo de datos](../../../relational-databases/replication/publish/media/replintro1.gif "Componentes de replicación y flujo de datos")  
  
## <a name="publisher"></a>publicador  
 El publicador es una instancia de base de datos que permite que los datos estén disponibles para otras ubicaciones a través de la replicación. El publicador puede tener una o más publicaciones, cada una de las cuales representa un conjunto de objetos y datos relacionados lógicamente para replicar.  
  
## <a name="distributor"></a>Distribuidor  
 El distribuidor es una instancia de base de datos que funciona como almacén para datos específicos de replicación asociados con uno o más publicadores. Cada publicador está asociado con una sola base de datos (conocida como la base de datos de distribución) en el distribuidor. La base de datos de distribución almacena los datos de estado de la replicación, metadatos acerca de la publicación y, en algunos casos, funciona como cola para los datos que se transfieren del publicador a los suscriptores. En muchos casos, una sola instancia de servidor de bases de datos funciona como publicador y como distribuidor Esto se conoce como un *distribuidor local*. Cuando el publicador y el distribuidor se configuran en instancias distintas del servidor de bases de datos, el distribuidor se denomina un *distribuidor remoto*.  
  
## <a name="subscribers"></a>Suscriptores  
 Un suscriptor es una instancia de base de datos que recibe datos replicados. Un suscriptor puede recibir datos de varios publicadores y publicaciones. En función del tipo de replicación elegida, el suscriptor también puede devolver los datos modificados al publicador o volver a publicar los datos en otros suscriptores.  
  
## <a name="article"></a>Artículo  
 Un artículo identifica un objeto de base de datos incluido en una publicación. Una publicación puede contener diferentes tipos de artículos, como tablas, vistas, procedimientos almacenados y otros objetos. Cuando las tablas se publican como artículos, se pueden usar filtros para restringir las columnas y filas de datos que se envían a los suscriptores.  
  
## <a name="publication"></a>Publicación  
 Una publicación es un conjunto de uno o más artículos de una base de datos. La agrupación de varios artículos en una publicación permite especificar más fácilmente un conjunto de objetos y datos de bases de datos relacionados lógicamente, que se replican como una unidad.  
  
## <a name="subscription"></a>Suscripción  
 Una suscripción es una solicitud de una copia de una publicación que se entrega a un suscriptor. La suscripción define qué publicación se recibirá, dónde y cuándo. Hay dos tipos de suscripciones: de inserción y de extracción. Para más información sobre las suscripciones de inserción y de extracción, vea [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md).  
  
## <a name="see-also"></a>Ver también  
 [Información general sobre los agentes de replicación](../../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Tipos de replicación](../../../relational-databases/replication/types-of-replication.md)   
 [Configurar la replicación para grupos de disponibilidad AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)   
 [Mantener una base de datos de publicación AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)  
  
  
