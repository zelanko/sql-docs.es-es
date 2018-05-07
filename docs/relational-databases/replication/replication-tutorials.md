---
title: Tutoriales de replicación | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3900aae4e96b5490b0b65cbbee004fc66337ff63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="replication-tutorials"></a>Tutoriales de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La replicación es una solución eficaz para migrar datos o subconjuntos de datos entre servidores. Puede replicar datos entre servidores que están conectados de forma continua mediante la replicación transaccional. También puede replicar datos entre servidores y clientes que están conectados de forma intermitente con la replicación de mezcla. A continuación encontrará tutoriales que le ayudan a preparar el servidor para la replicación y, después, le enseñan a configurar la replicación transaccional y de mezcla. 
  
En los tutoriales de replicación, "publicador" hace referencia al servidor que contiene los datos de origen que se replican y "suscriptor" hace referencia al servidor de destino. El publicador y el suscriptor pueden compartir la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque no es necesario. Para obtener más información, vea [Información general del modelo de publicación de replicación](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

Estos tutoriales usan NODE1\SQL2016 como publicador y distribuidor y NODE2\SQL2016 como suscriptor. 
  
> [!NOTE]  
> La mayoría de las tareas que se muestran en estos tutoriales se pueden realizar mediante programación. Para obtener más información, vea [Guía del desarrollador (replicación)](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## <a name="replication-tutorials"></a>Tutoriales de replicación  
[Tutorial: Preparar SQL Server para la replicación: publicador, distribuidor, suscriptor](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Aprenda cómo preparar servidores para poder ejecutar una replicación con privilegios mínimos. Debe finalizar este tutorial antes de realizar otros tutoriales de replicación.  
  
[Tutorial: Configurar la replicación entre dos servidores conectados de forma continua (transaccional)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Aprenda cómo configurar la replicación transaccional para replicar datos entre servidores conectados de forma continua. Este tutorial también incluye metodología de solución de problemas para algunos errores básicos. 

  
[Tutorial: Configurar la replicación entre un servidor y clientes móviles (de mezcla)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Aprenda cómo configurar la replicación de mezcla para intercambiar datos entre un servidor y uno o más clientes que solo se conectan en determinadas ocasiones.  
  
## <a name="see-also"></a>Ver también  
[Seguridad y protección para la replicación](../../relational-databases/replication/security/security-and-protection-replication.md) 

[Información general de la replicación transaccional](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication) 

[Información general sobre la replicación de mezcla](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)

  