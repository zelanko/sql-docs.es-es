---
description: Seguridad del agente (Asistente para nueva publicación)
title: Seguridad del agente (Asistente para nueva publicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 8a33a8a17aea4bddadb1c2ed99a4e5b1bcf1966b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460318"
---
# <a name="agent-security-new-publication-wizard"></a>Seguridad del agente (Asistente para nueva publicación)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La página **Seguridad del agente** permite especificar las cuentas en las que se ejecutarán los siguientes agentes y a partir de las cuales establecerán conexiones con los equipos que conforman una topología de replicación:  
  
-   Agente de instantáneas para todas las publicaciones.  
  
-   Agente de registro del LOG para todas las publicaciones transaccionales.  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones actualizables. Se crea el trabajo de Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente a este agente si se ha especificado **Publicación transaccional con suscripciones actualizables** en la página **Tipo de publicación**, independientemente del tipo de suscripciones actualizables que se use. Para obtener más información sobre las suscripciones actualizables, vea [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opciones  
 **Agente de instantáneas**  
 Se muestra en todas las publicaciones. Haga clic en **Configuración de seguridad** para especificar la configuración de seguridad en el cuadro de diálogo **Seguridad del Agente de instantáneas** .  
  
 Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de instantáneas** para obtener más información sobre los permisos requeridos para las cuentas utilizadas por el Agente de instantáneas.  
  
 **Agente de lector del registro**  
 Se muestra en todas las publicaciones transaccionales. Haga clic en **Configuración de seguridad** para especificar la configuración de seguridad en el cuadro de diálogo **Seguridad del Agente de registro del LOG** .  
  
 Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de registro del LOG** para obtener más información sobre los permisos requeridos para las cuentas utilizadas por el Agente de registro del LOG.  
  
> [!NOTE]  
>  Existe un Agente de registro del LOG para cada base de datos que se publica utilizando la replicación transaccional. Si ya existe una publicación transaccional en la base de datos, la configuración de seguridad será de solo lectura. Es posible modificar la configuración del cuadro de diálogo **Propiedades de la publicación** , aunque los cambios afectarán a todas las publicaciones transaccionales de la base de datos.  
  
 **Agente de lectura de cola**  
 Se muestra para las publicaciones transaccionales que admiten suscripciones actualizables Haga clic en **Configuración de seguridad** para especificar la configuración de seguridad en el cuadro de diálogo **Seguridad del Agente de lectura de cola** . Se crea un trabajo de Agente de lectura de cola cuando finaliza este asistente. Esto no depende de que se hayan creado suscripciones de actualización en cola. Si no tiene previsto crear una suscripción de actualización en cola, puede deshabilitar el trabajo. Haga clic con el botón derecho en el trabajo (con el formato de nombre *[\<Publisher>].\<integer>* .) en la carpeta **Trabajos** del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, después, haga clic en **Deshabilitar**.  
  
 Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de lectura de cola** para obtener más información sobre los permisos requeridos para las cuentas utilizadas por el Agente de lectura de cola.  
  
> [!NOTE]  
>  Hay un Agente de lectura de cola para cada base de datos de distribución (y para todos los publicadores que sirve). Si ya existe una publicación transaccional que permite suscripciones de actualización en cola en cualquiera de los publicadores que usa una determinada base de datos de distribución, la configuración de seguridad será de solo lectura. Se pueden realizar cambios en la cuenta en la que el Agente de lectura de cola se ejecuta y establece conexiones en el cuadro de diálogo **Propiedades del distribuidor** , aunque los cambios afectarán a todos los publicadores que usen la base de datos de distribución.  
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Identidad y control de acceso (replicación)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
