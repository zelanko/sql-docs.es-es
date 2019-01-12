---
title: Creación y aplicación de la instantánea | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], applying
- snapshots [SQL Server replication], creating
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4c69b22af2a4e5a087c21b34fc719f971c3844b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128585"
---
# <a name="create-and-apply-the-snapshot"></a>Crear y aplicar una instantánea
  El Agente de instantáneas genera instantáneas una vez creada la publicación. Se pueden generar de la siguiente manera:  
  
-   Inmediatamente. De manera predeterminada, se genera una instantánea para una publicación de combinación inmediatamente después de haberse creado la publicación en el Asistente para nueva publicación.  
  
-   A la hora programada. Especifique una programación en la página **Agente de instantáneas** del Asistente para nueva publicación o al utilizar procedimientos almacenados o Replication Management Objects (RMO).  
  
-   Manualmente. Ejecute el Agente de instantáneas desde el símbolo del sistema o desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Conceptos de los ejecutables del Agente de replicación](concepts/replication-agent-executables-concepts.md) e [Iniciar y detener un Agente de replicación &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
 Para la replicación de mezcla se genera una instantánea cada vez que se ejecuta el Agente de instantáneas. Para la replicación transaccional, la generación de instantáneas depende de la configuración de la propiedad de publicación **immediate_sync**. Si la propiedad se define como TRUE (la opción predeterminada cuando se utiliza el Asistente para nueva publicación), se genera una instantánea cada vez que se ejecuta el Agente de instantáneas, y puede aplicarse a un suscriptor en cualquier momento. Si la propiedad se define como FALSE (la opción predeterminada cuando se utiliza **sp_addpublication**), la instantánea se genera solo si se ha agregado una nueva suscripción desde la última ejecución del Agente de instantáneas; los suscriptores deberán esperar a que el Agente de instantáneas finalice para poder sincronizarse.  
  
 De manera predeterminada, cuando se generan instantáneas, éstas se guardan en la carpeta predeterminada de instantáneas situada en el distribuidor. También puede guardar archivos de instantáneas en medios extraíbles, como discos extraíbles o CD-ROM, o en otras ubicaciones distintas de la carpeta de instantáneas predeterminada. Además, puede comprimir los archivos para que sean más fáciles de almacenar y transferir, así como ejecutar scripts antes o después de aplicar la instantánea al suscriptor. Para obtener más información acerca de estas opciones, consulte [Snapshot Options](snapshot-options.md).  
  
 Si la instantánea es para una publicación de combinación que utiliza filtros con parámetros, se crea mediante un proceso de dos partes. En primer lugar se crea una instantánea del esquema que contiene los scripts y el esquema de replicación de los objetos publicados, pero no los datos. A continuación, cada suscripción se inicializa con una instantánea que incluye los scripts y el esquema copiados de la instantánea de esquema y los datos que pertenecen a la partición de la suscripción. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Una vez creada la instantánea en el publicador y almacenada en una ubicación de instantáneas predeterminada o alternativa, la misma puede transferirse al suscriptor y aplicarse. El Agente de distribución (para replicación transaccional o de instantáneas) o el Agente de mezcla (para la replicación de mezcla) transfiere la instantánea y aplica el esquema y los archivos de datos a la base de datos de suscripciones del suscriptor durante la sincronización inicial. De manera predeterminada, la sincronización inicial se produce inmediatamente después de creada la suscripción si se utiliza el Asistente para nueva publicación. Este comportamiento se controla mediante la opción **Inicializar cuando** de la página **Inicializar suscripciones** del asistente. Cuando se generan instantáneas después de inicializada una suscripción, éstas no se aplican al suscriptor a menos que se marque una suscripción para reinicialización. Para obtener más información, vea [Reinicializar suscripciones](reinitialize-subscriptions.md).  
  
 Una vez que el Agente de distribución o el Agente de mezcla aplican la instantánea inicial, el agente propaga las actualizaciones posteriores y otras modificaciones de datos. Cuando se distribuyen y se aplican instantáneas a los suscriptores, solo se ven afectados los suscriptores que estén esperando instantáneas iniciales o nuevas. Los demás suscriptores de esa publicación (aquellos que ya están recibiendo inserciones, actualizaciones, eliminaciones u otras modificaciones de los datos publicados) no se ven afectados.  
  
 Para crear y aplicar la instantánea inicial, [Create and Apply the Initial Snapshot](create-and-apply-the-initial-snapshot.md).  
  
 Para ver o modificar la ubicación de la carpeta de instantáneas predeterminada, vea  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especifique la ubicación predeterminada de instantáneas](snapshot-options.md#snapshot-folder-locations)
-   Programación de la replicación y programación con RMO: [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)  
  
  
