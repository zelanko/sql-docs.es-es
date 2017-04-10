---
title: "Copias de seguridad y restauraci&#243;n de publicadores de Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperación [replicación de SQL Server], publicación de Oracle"
  - "copia de seguridad [replicación de SQL Server], publicación de Oracle"
  - "publicación de Oracle [replicación de SQL Server], realizar copia de seguridad y restaurar"
  - "restauración [replicación de SQL Server], publicación de Oracle"
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Copias de seguridad y restauraci&#243;n de publicadores de Oracle
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Siga estas instrucciones para hacer copias de seguridad y restaurar:  
  
-   Asegúrese de que el Agente de registro del LOG no se ejecuta y que no se produce ninguna otra actividad de base de datos en las tablas publicadas cuando esté haciendo copias de seguridad del publicador.  
  
-   Haga copias de seguridad del publicador y del distribuidor a la vez.  
  
-   Si es necesario restaurar el publicador o el distribuidor, reinicialice todas las suscripciones.  
  
-   Para restaurar un suscriptor desde una copia de seguridad (sin tener que reinicializar todas las suscripciones), las transacciones entregadas en la base de datos del distribuidor después de haber realizado la copia de seguridad de la base de datos de la última suscripción deben estar todavía disponibles. El período de tiempo que las transacciones están disponibles depende de la configuración de retención de la distribución. Para obtener información sobre estas opciones, consulte [caducidad de la suscripción y la desactivación](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Si el publicador o el distribuidor no están sincronizados como resultado de una restauración de la base de datos, los agentes de replicación registran mensajes de error. En ese caso, debe quitar y volver a crear todas las publicaciones y suscripciones relevantes:  
  
    1.  Genere script para la definición de las publicaciones y las suscripciones. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
         Si la definición de las publicaciones ha cambiado entre las versiones de los estados del publicador y el distribuidor, será necesario que modifique los scripts.  
  
    2.  Quite las publicaciones y las suscripciones.  
  
    3.  Ejecute los scripts creados en el paso 1.  
  
     Si es necesario quitar y volver a configurar el publicador, quite el sinónimo público **MSSQLSERVERDISTRIBUTOR** y el usuario de replicación de Oracle configurado con la opción **CASCADE** para quitar todos los objetos de la replicación del publicador de Oracle.  
  
## Vea también  
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  