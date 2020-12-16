---
description: Reinicializar suscripciones
title: Reinicialización de suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 739d977502331d245b78fcd22776a25590c66bc8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479816"
---
# <a name="reinitialize-subscriptions"></a>Reinicializar suscripciones
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Reinicializar una suscripción implica aplicar una nueva instantánea de uno o más artículos a uno o más suscriptores: las replicaciones transaccionales y de instantáneas permiten la reinicialización de los artículos individuales. La replicación de mezcla requiere que todos los artículos se reinicialicen. Los nodos de una topología de replicación transaccional punto a punto no se pueden reinicializar. Si necesita asegurarse de que un nodo tiene una copia nueva de los datos, restaure una copia de seguridad en el nodo. La reinicialización se produce por dos motivos:  
  
-   Se marca una suscripción explícitamente para reinicializarla.  
  
-   Se realiza una acción, por ejemplo un cambio de propiedad, que requiere la reinicialización. Para obtener más información sobre las acciones que requieren reinicialización, vea [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 En ambos casos, la instantánea más reciente se aplica al suscriptor la próxima vez que se ejecuten el Agente de distribución o el Agente de mezcla. En la replicación transaccional y de instantáneas, cuando se produce la reinicialización, cualquier cambio realizado en el suscriptor, pero que todavía no esté sincronizado con el publicador, lo sobrescribirá la aplicación de la nueva instantánea.  
  
 En la replicación de mezcla, puede elegir cargar todos los cambios de datos desde el suscriptor antes de que se aplique la instantánea. Los cambios de esquema pendientes del publicador se aplican en el suscriptor y, después, las actualizaciones que se hayan realizado en el suscriptor desde la última sincronización se propagan al publicador antes de volver a aplicar la instantánea. Este comportamiento lo controlan las propiedades **upload_first** y **automatic_reinitialization_policy** . Para obtener más información, vea [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md). Si marca una suscripción para reinicialización utilizando SQL Server Management Studio o el Monitor de replicación, en el cuadro de diálogo **Reinicializar suscripciones** puede elegir una opción para cargar primero los cambios.  
  
> [!IMPORTANT]  
>  Si agrega, quita o cambia un filtro con parámetros en una publicación de combinación, los cambios pendientes en el suscriptor no se pueden volver a cargar en el publicador durante la reinicialización. Si desea cargar los cambios pendientes, sincronice todas las suscripciones antes de cambiar el filtro.  
  
 Si se especificó que no se aplicara ninguna instantánea inicial en el suscriptor al crear la suscripción, y después se marca la suscripción para reinicializarla, no se aplicará ninguna instantánea. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Para reinicializar una suscripción**  
  
 Para reinicializar todos los artículos de una suscripción, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimientos almacenados o Replication Management Objects (RMO). Debe utilizar procedimientos almacenados para reinicializar artículos individuales en publicaciones transaccionales y de instantáneas. Para más información, consulte [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md).  
  
## <a name="see-also"></a>Consulte también  
 [Initialize a Subscription](../../relational-databases/replication/initialize-a-subscription.md)  (Inicializar una suscripción)  
 [Desactivación y expiración de la suscripción](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
