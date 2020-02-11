---
title: Agente de instantáneas (Asistente para nueva publicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 20e4e015064dcf0e472c2f3c56ecabf4100e6fe7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62676578"
---
# <a name="snapshot-agent-new-publication-wizard"></a>Agente de instantáneas (Asistente para nueva publicación)
  El Agente de instantáneas crea archivos que contienen el esquema y los datos de publicación que se utilizan para inicializar nuevas suscripciones. De forma predeterminada, el Agente de instantáneas se ejecuta inmediatamente después de la creación de la publicación en el Asistente para nueva publicación. Posteriormente, el agente se ejecuta de acuerdo con la programación que el usuario haya especificado. Que el agente cree nuevos archivos de instantáneas cada vez que se ejecute depende del tipo de replicación y de las opciones que se hayan elegido. Para obtener más información, vea [Crear y aplicar una instantánea](create-and-apply-the-snapshot.md).  
  
 Para las publicaciones de combinación que utilizan filtros con parámetros, debe crear una instantánea para cada partición de datos después de haber finalizado la instantánea de publicación. Para más información, consulte [Instantáneas para publicaciones de combinación con filtros con parámetros](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="options"></a>Opciones  
 **Crear una instantánea inmediatamente** (replicación de mezcla) o **Crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones** (replicación transaccional)  
 Active esta casilla para crear una instantánea inmediatamente después de que finalice el Asistente para nueva publicación. Desactive esta casilla si tiene previsto cambiar las propiedades de la instantánea en el cuadro de diálogo **Propiedades de la publicación** antes de generar una instantánea o bien si inicializa el suscriptor sin una instantánea. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  El asistente podría solicitar una conexión al distribuidor para iniciar un trabajo adecuado del Agente de distribución o el Agente de mezcla.  
  
 **Programar el Agente de instantáneas para ejecutarse**  
 Acepte el programa predeterminado para la ejecución del Agente de instantáneas o haga clic en **Cambiar** para especificar un programa.  
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](publish/create-a-publication.md)   
 [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)   
 [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Información general sobre los agentes de replicación](agents/replication-agents-overview.md)  
  
  
