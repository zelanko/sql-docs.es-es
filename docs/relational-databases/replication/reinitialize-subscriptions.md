---
title: "Reinicializar suscripciones | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicializar suscripciones [replicación de SQL Server], reinicializar"
  - "suscripciones [replicación de SQL Server], reinicializar"
  - "reinicializar suscripciones"
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# Reinicializar suscripciones
  Reinicializar una suscripción implica aplicar una nueva instantánea de uno o más artículos a uno o más suscriptores: las replicaciones transaccionales y de instantáneas permiten la reinicialización de los artículos individuales. La replicación de mezcla requiere que todos los artículos se reinicialicen. Los nodos de una topología de replicación transaccional punto a punto no se pueden reinicializar. Si necesita asegurarse de que un nodo tiene una copia nueva de los datos, restaure una copia de seguridad en el nodo. La reinicialización se produce por dos motivos:  
  
-   Se marca una suscripción explícitamente para reinicializarla.  
  
-   Se realiza una acción, por ejemplo un cambio de propiedad, que requiere la reinicialización. Para obtener más información acerca de las acciones que requieren la reinicialización, vea [Propiedades de artículo y publicación de cambio](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 En ambos casos, la instantánea más reciente se aplica al suscriptor la próxima vez que se ejecuten el Agente de distribución o el Agente de mezcla. En la replicación transaccional y de instantáneas, cuando se produce la reinicialización, cualquier cambio realizado en el suscriptor, pero que todavía no esté sincronizado con el publicador, lo sobrescribirá la aplicación de la nueva instantánea.  
  
 En la replicación de mezcla, puede elegir cargar todos los cambios de datos desde el suscriptor antes de que se aplique la instantánea. Los cambios de esquema pendientes del publicador se aplican en el suscriptor y, después, las actualizaciones que se hayan realizado en el suscriptor desde la última sincronización se propagan al publicador antes de volver a aplicar la instantánea. Este comportamiento se controla mediante la **upload_first** y **automatic_reinitialization_policy** Propiedades; para obtener más información, consulte [reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md). Si marca una suscripción para reinicialización utilizando SQL Server Management Studio o el Monitor de replicación, se ofrece una opción el **reinicializar suscripciones** cuadro de diálogo para cargar primero los cambios.  
  
> [!IMPORTANT]  
>  Si agrega, quita o cambia un filtro con parámetros en una publicación de combinación, los cambios pendientes en el suscriptor no se pueden volver a cargar en el publicador durante la reinicialización. Si desea cargar los cambios pendientes, sincronice todas las suscripciones antes de cambiar el filtro.  
  
 Si se especificó que no se aplicara ninguna instantánea inicial en el suscriptor al crear la suscripción, y después se marca la suscripción para reinicializarla, no se aplicará ninguna instantánea. Para obtener más información, consulte [inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 **Para reinicializar una suscripción**  
  
 Para reinicializar todos los artículos de una suscripción, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimientos almacenados o Replication Management Objects (RMO). Debe utilizar procedimientos almacenados para reinicializar artículos individuales en publicaciones transaccionales y de instantáneas. Para más información, consulte [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md).  
  
## Vea también  
 [Inicializar una suscripción](../../relational-databases/replication/initialize-a-subscription.md)   
 [Desactivación y expiración de las suscripciones](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  