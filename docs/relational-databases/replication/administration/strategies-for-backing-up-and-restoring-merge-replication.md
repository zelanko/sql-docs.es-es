---
title: Estrategias para hacer copias de seguridad y restaurar la replicación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16f7701ab70e3edab1194732dca70e5c10f98a65
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707913"
---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>Estrategias para hacer copias de seguridad y restaurar la replicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para la replicación de mezcla, cree periódicamente una copia de seguridad de las siguientes bases de datos:  
  
-   Base de datos de publicaciones en el publicador  
  
-   Base de datos de distribución en el distribuidor  
  
-   Base de datos de suscripciones en el suscriptor  
  
-   Las bases de datos del sistema **maestra** y **msdb** en el publicador, el distribuidor y todos los suscriptores. La copia de seguridad de cada una de estas bases de datos debe realizarse al mismo tiempo que la de las otras y la base de datos de replicación correspondiente. Por ejemplo, cree la copia de seguridad de las bases de datos **master** y **msdb** en el publicador al mismo tiempo que crea la copia de seguridad de la base de datos de publicaciones. Al restaurar la base de datos de publicaciones, asegúrese de que las bases de datos **master** y **msdb** sean coherentes con la base de datos de publicaciones en términos de configuración general y configuración de la replicación.  
  
 Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no se realizan copias de seguridad de registros, debe realizarse una copia de seguridad siempre que se cambie un valor importante en la replicación. Para más información, vea [Acciones comunes que requieren una copia de seguridad actualizada](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
 Elija uno de los siguientes métodos para crear copias de seguridad y restaurar la base de datos de publicaciones; después, siga las recomendaciones para la base de datos de distribución y las bases de datos de suscripciones.  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>Realizar copias de seguridad y restaurar la base de datos de publicaciones  
 Hay dos métodos para restaurar una base de datos de publicaciones de combinación. Después de restaurar la base de datos de publicaciones a partir de una copia de seguridad, debe:  
  
-   Sincronizar la base de datos de publicaciones con una base de datos de suscripciones.  
  
-   Reinicializar todas las suscripciones a las publicaciones en la base de datos de publicaciones.  
  
 Cualquiera de estos métodos garantiza la sincronización del publicador y de todos los suscriptores después de la restauración.  
  
> [!NOTE]  
>  Si alguna tabla contiene columnas de identidad, debe asegurarse de asignar los intervalos de identidad correctos después de una restauración. Para más información, vea [Replicar columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### <a name="synchronizing-the-publication-database"></a>Sincronizar la base de datos de publicaciones  
 La sincronización de una base de datos de publicaciones con una base de datos de suscripciones permite cargar desde una o más bases de datos de suscripciones los cambios realizados previamente en la base de datos de publicaciones que no están representados en la copia de seguridad restaurada. Los datos que se pueden cargar dependen de la forma en que se filtra una publicación:  
  
-   Si la publicación no está filtrada, debe poder actualizar la base de datos de publicaciones sincronizándola con el suscriptor más actualizado.  
  
-   Si la publicación está filtrada, es posible que no pueda actualizar la base de datos de publicaciones. Considere una tabla dividida de forma que cada suscripción reciba únicamente datos de clientes de una región: norte, este, sur y oeste. Si hay al menos un suscriptor para cada partición de datos, al sincronizar cada partición con un suscriptor se debería actualizar la base de datos de publicaciones. Sin embargo, si los datos de la partición oeste, por ejemplo, no se han replicado en ningún suscriptor, no se podrán actualizar estos datos en el publicador.  
  
> [!IMPORTANT]  
>  La sincronización de una base de datos de publicaciones con una base de datos de suscripciones puede dar como resultado la restauración de las tablas publicadas hasta un momento más reciente que el de las otras tablas no publicadas restauradas de la copia de seguridad.  
  
 Si se sincroniza con un suscriptor que esté ejecutando una versión de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], la suscripción no podrá ser anónima; deberá ser una suscripción de cliente o de servidor (denominadas suscripciones locales y globales en versiones anteriores).  
  
 Para sincronizar una suscripción de inserción, vea [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) y [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
### <a name="reinitializing-all-subscriptions"></a>Reinicializar todas las suscripciones  
 La reinicialización de todas las suscripciones garantiza que el estado de todos los suscriptores sea coherente con la base de datos de publicaciones restaurada. Este enfoque debe utilizarse si desea restaurar una topología completa a su estado anterior, representado por la copia de seguridad de una base de datos de publicaciones determinada. Por ejemplo, puede reinicializar todas las suscripciones si desea restaurar una base de datos a un momento anterior como un mecanismo para recuperarse de una operación por lotes realizada incorrectamente.  
  
 Si elige esta opción, genere una nueva instantánea para entregar a los suscriptores reinicializados inmediatamente después de restaurar la base de datos de publicaciones.  
  
 Para reinicializar una suscripción, vea [Reinitialize a Subscription](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
 Para crear y aplicar una instantánea, vea [Crear y aplicar la instantánea inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) y [Crear una instantánea para una publicación de mezcla con filtros con parámetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>Realizar copias de seguridad y restaurar la base de datos de distribución  
 Con la replicación de mezcla, se deben crear periódicamente copias de seguridad de la base de datos de distribución, que se pueden restaurar sin ningún tipo de consideraciones especiales, siempre que la copia de seguridad utilizada no sea más antigua que el menor período de retención de todas las publicaciones que utilizan el distribuidor. Por ejemplo, si hay tres publicaciones con períodos de retención de 10, 20 y 30 días respectivamente, la copia de seguridad que deberá utilizarse para restaurar la base de datos no debe tener más de 10 días. La base de datos de distribución tiene un rol limitado en la replicación de mezcla: no almacena ningún dato utilizado en el seguimiento de cambios y no almacena temporalmente los cambios de la replicación de mezcla que se enviarán a las bases de datos de suscripciones (como ocurre con la replicación transaccional).  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>Realizar copias de seguridad y restaurar la base de datos de suscripciones  
 Para garantizar la recuperación correcta de una base de datos de suscripciones, los suscriptores deben sincronizarse con el publicador antes de crear la copia de seguridad de la base de datos de suscripciones y después de restaurar la base de datos de suscripciones:  
  
-   La sincronización con el publicador antes de crear la copia de seguridad de la base de datos de suscripciones ayuda a garantizar que si se restaura un suscriptor a partir de la copia de seguridad, la suscripción seguirá estando dentro del período de retención de la publicación. Por ejemplo, imagine una publicación con un período de retención de 10 días. Suponga que la última sincronización se realizó hace 8 días y que ahora se efectúa la copia de seguridad. Si la copia de seguridad se restaura 4 días más tarde, ya habrán transcurrido 12 días desde la última sincronización, un período superior al de retención. En este caso, será necesario reinicializar el suscriptor. Si el suscriptor se hubiera sincronizado antes de realizar la copia de seguridad, la base de datos de suscripciones todavía estaría dentro del período de retención.  
  
     La copia de seguridad no debe ser anterior al menor período de retención de todas las publicaciones a las que se suscribe el suscriptor. Por ejemplo, si un suscriptor se suscribe a tres publicaciones cuyos períodos de retención son 12, 20 y 30 días respectivamente, la copia de seguridad que deberá utilizarse para restaurar la base de datos no debería tener más de 10 días.  
  
-   Sincronizar la base de datos de suscripciones con cada una de sus publicaciones después de una restauración garantiza que el suscriptor se actualice con todos los cambios presentes en el publicador.  
  
 Para establecer el período de retención de publicación, vea [Set the Expiration Period for Subscriptions](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md) (Establecer el período de expiración para las suscripciones).  
  
 Para sincronizar una suscripción de inserción, vea [Sincronizar una suscripción de inserción](../../../relational-databases/replication/synchronize-a-push-subscription.md) y [Sincronizar una suscripción de extracción](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>Realizar copias de seguridad y restaurar una base de datos de republicaciones  
 Cuando una base de datos se suscribe a datos de un publicador y, a su vez, publica esos mismos datos en otras bases de datos de suscripciones se denomina base de datos de republicaciones. Al restaurar una base de datos de republicaciones, siga las directrices descritas en las secciones "Realizar copias de seguridad y restaurar la base de datos de publicaciones" y "Realizar copias de seguridad y restaurar la base de datos de suscripciones" de este tema.  
  
## <a name="see-also"></a>Ver también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
