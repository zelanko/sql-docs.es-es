---
title: Tutoriales de replicación | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3e6b91d754c477efe14ee0d47192beff5c735138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784423"
---
# <a name="replication-tutorials"></a>Tutoriales de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La replicación es una solución eficaz para migrar datos o subconjuntos de datos entre servidores. Puede replicar datos entre servidores que están conectados completamente mediante la replicación transaccional. También puede replicar datos entre servidores y clientes que están conectados de forma intermitente mediante la replicación de mezcla. En este artículo encontrará tutoriales con los que podrá preparar el servidor para la replicación y con los que aprenderá a configurar la replicación transaccional y de mezcla. 
  
En los tutoriales de replicación, "publicador" hace referencia al servidor que contiene los datos de origen que se va a replicar. "Suscriptor" hace referencia al servidor de destino. El publicador y el suscriptor pueden compartir la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque no es necesario. Para más información, vea [Información general del modelo de publicación de replicación](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

Estos tutoriales usan NODE1\SQL2016 como publicador y distribuidor. Usan NODE2\SQL2016 como suscriptor. 
  
> [!NOTE]  
> La mayoría de las tareas que se muestran en estos tutoriales se pueden realizar mediante programación. Para más información, vea la [Documentación para desarrolladores de replicación](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## <a name="replication-tutorials"></a>Tutoriales de replicación  
[Tutorial: Preparar el servidor para la replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Aprenda cómo preparar servidores para poder ejecutar una replicación con privilegios mínimos. Debe finalizar este tutorial antes de realizar otros tutoriales de replicación.  
  
[Tutorial: Replicar datos entre servidores conectados completamente (transaccional)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Aprenda a configurar la replicación transaccional para replicar datos entre servidores conectados completamente. Este tutorial también incluye metodología de solución de problemas para algunos errores básicos. 

  
[Tutorial: Configurar la replicación (de mezcla) entre un servidor y clientes móviles](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Aprenda a configurar la replicación de mezcla para intercambiar datos entre un servidor y uno o más clientes que solo se conectan en determinadas ocasiones.  
  
## <a name="see-also"></a>Vea también  
[Seguridad y protección (replicación)](../../relational-databases/replication/security/security-and-protection-replication.md) 

[Replicación transaccional](https://docs.microsoft.com/sql/relational-databases/replication/transactional/transactional-replication) 

[Replicación de mezcla](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication)

  
