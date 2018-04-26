---
title: Inicializar una suscripción | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 13640536d818dfff9b28bd78c7fbdd43c7800269
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="initialize-a-subscription"></a>Inicializar una suscripción
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Los suscriptores de una topología de replicación se deben inicializar con el fin de que tengan una copia del esquema de cada artículo de la publicación a la que están suscritos y de los objetos de replicación que se requieran, como procedimientos almacenados, desencadenadores y tablas de metadatos. Además, el suscriptor normalmente recibe un conjunto de datos inicial. El método de inicialización predeterminado usa una instantánea completa que incluye el esquema, objetos de replicación y datos, aunque las publicaciones también se pueden inicializar sin una instantánea completa.  
  
 Para obtener más información, consulte [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) y [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
