---
title: Agente de instantáneas (Asistente para nueva publicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa6f51b354a0843b189e216ef7d690ab1ccc5f19
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699333"
---
# <a name="snapshot-agent-new-publication-wizard"></a>Agente de instantáneas (Asistente para nueva publicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Agente de instantáneas crea archivos que contienen el esquema y los datos de publicación que se utilizan para inicializar nuevas suscripciones. De forma predeterminada, el Agente de instantáneas se ejecuta inmediatamente después de la creación de la publicación en el Asistente para nueva publicación. Posteriormente, el agente se ejecuta de acuerdo con la programación que el usuario haya especificado. Que el agente cree nuevos archivos de instantáneas cada vez que se ejecute depende del tipo de replicación y de las opciones que se hayan elegido. Para obtener más información, consulte [Crear y aplicar una instantánea](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Para las publicaciones de combinación que utilizan filtros con parámetros, debe crear una instantánea para cada partición de datos después de haber finalizado la instantánea de publicación. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="options"></a>Opciones  
 **Crear una instantánea inmediatamente** (replicación de mezcla) o **Crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones** (replicación transaccional)  
 Active esta casilla para crear una instantánea inmediatamente después de que finalice el Asistente para nueva publicación. Desactive esta casilla si tiene previsto cambiar las propiedades de la instantánea en el cuadro de diálogo **Propiedades de la publicación** antes de generar una instantánea o bien si inicializa el suscriptor sin una instantánea. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  El asistente podría solicitar una conexión al distribuidor para iniciar un trabajo adecuado del Agente de distribución o el Agente de mezcla.  
  
 **Programar el Agente de instantáneas para ejecutarse**  
 Acepte el programa predeterminado para la ejecución del Agente de instantáneas o haga clic en **Cambiar** para especificar un programa.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
