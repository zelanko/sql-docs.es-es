---
title: Copias de seguridad y restauración de publicadores de Oracle| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55270122c19f014f16ef62dcdc5efa52395d3ec1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238835"
---
# <a name="backup-and-restore-for-oracle-publishers"></a>Copias de seguridad y restauración de publicadores de Oracle
  Siga estas instrucciones para hacer copias de seguridad y restaurar:  
  
-   Asegúrese de que el Agente de registro del LOG no se ejecuta y que no se produce ninguna otra actividad de base de datos en las tablas publicadas cuando esté haciendo copias de seguridad del publicador.  
  
-   Haga copias de seguridad del publicador y del distribuidor a la vez.  
  
-   Si es necesario restaurar el publicador o el distribuidor, reinicialice todas las suscripciones.  
  
-   Para restaurar un suscriptor desde una copia de seguridad (sin tener que reinicializar todas las suscripciones), las transacciones entregadas en la base de datos del distribuidor después de haber realizado la copia de seguridad de la base de datos de la última suscripción deben estar todavía disponibles. El período de tiempo que las transacciones están disponibles depende de la configuración de retención de la distribución. Para más información, vea [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md) (Desactivación y expiración de las suscripciones).  
  
-   Si el publicador o el distribuidor no están sincronizados como resultado de una restauración de la base de datos, los agentes de replicación registran mensajes de error. En ese caso, debe quitar y volver a crear todas las publicaciones y suscripciones relevantes:  
  
    1.  Genere script para la definición de las publicaciones y las suscripciones. Para más información, consulte [Scripting Replication](../scripting-replication.md).  
  
         Si la definición de las publicaciones ha cambiado entre las versiones de los estados del publicador y el distribuidor, será necesario que modifique los scripts.  
  
    2.  Quite las publicaciones y las suscripciones.  
  
    3.  Ejecute los scripts creados en el paso 1.  
  
     Si es necesario quitar y volver a configurar el publicador, quite el sinónimo público **MSSQLSERVERDISTRIBUTOR** y el usuario de replicación de Oracle configurado con la opción **CASCADE** para quitar todos los objetos de la replicación del publicador de Oracle.  
  
## <a name="see-also"></a>Vea también  
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../administration/back-up-and-restore-replicated-databases.md)   
 [Configurar un publicador de Oracle](configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](oracle-publishing-overview.md)  
  
  
