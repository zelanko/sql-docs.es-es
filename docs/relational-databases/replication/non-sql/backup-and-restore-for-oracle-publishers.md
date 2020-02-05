---
title: Copias de seguridad y restauración de publicadores de Oracle| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ea6539e0d004f573281d54f7bb4a4c055c7b3e73
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67901112"
---
# <a name="backup-and-restore-for-oracle-publishers"></a>Copias de seguridad y restauración de publicadores de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Siga estas instrucciones para hacer copias de seguridad y restaurar:  
  
-   Asegúrese de que el Agente de registro del LOG no se ejecuta y que no se produce ninguna otra actividad de base de datos en las tablas publicadas cuando esté haciendo copias de seguridad del publicador.  
  
-   Haga copias de seguridad del publicador y del distribuidor a la vez.  
  
-   Si es necesario restaurar el publicador o el distribuidor, reinicialice todas las suscripciones.  
  
-   Para restaurar un suscriptor desde una copia de seguridad (sin tener que reinicializar todas las suscripciones), las transacciones entregadas en la base de datos del distribuidor después de haber realizado la copia de seguridad de la base de datos de la última suscripción deben estar todavía disponibles. El período de tiempo que las transacciones están disponibles depende de la configuración de retención de la distribución. Para más información, vea [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md) (Desactivación y expiración de las suscripciones).  
  
-   Si el publicador o el distribuidor no están sincronizados como resultado de una restauración de la base de datos, los agentes de replicación registran mensajes de error. En ese caso, debe quitar y volver a crear todas las publicaciones y suscripciones relevantes:  
  
    1.  Genere script para la definición de las publicaciones y las suscripciones. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
         Si la definición de las publicaciones ha cambiado entre las versiones de los estados del publicador y el distribuidor, será necesario que modifique los scripts.  
  
    2.  Quite las publicaciones y las suscripciones.  
  
    3.  Ejecute los scripts creados en el paso 1.  
  
     Si es necesario quitar y volver a configurar el publicador, quite el sinónimo público **MSSQLSERVERDISTRIBUTOR** y el usuario de replicación de Oracle configurado con la opción **CASCADE** para quitar todos los objetos de la replicación del publicador de Oracle.  
  
## <a name="see-also"></a>Consulte también  
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
