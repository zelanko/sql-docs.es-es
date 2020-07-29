---
title: Proteger el suscriptor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], security
- Subscribers [SQL Server replication], security
- security [SQL Server replication], Subscribers
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0d2b4567f9f835e0118e882aa8ca85d1465c4b3f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "87110642"
---
# <a name="secure-the-subscriber"></a>Proteger el suscriptor
[!INCLUDE[sql-asdb](../../../includes/applies-to-version/sql-asdb.md)]
  Los agentes de mezcla y de distribución se conectan al suscriptor. Estas conexiones pueden realizarse en el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Windows. Es importante proporcionar un inicio de sesión apropiado para estos agentes, al mismo tiempo que se sigue el principio de conceder los derechos mínimos necesarios y proteger el almacenamiento de todas las contraseñas. Para obtener información acerca de los permisos necesarios para cada agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="distribution-agent"></a>Agente de distribución  
 Hay un Agente de distribución por suscripción (un agente independiente, predeterminado para las publicaciones creadas en el Asistente para nueva publicación), o un Agente de distribución por par de base de datos de publicaciones y base de datos de suscripciones (un agente compartido). T  
  
 Para especificar la información de conexión para suscripciones de inserción, vea [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md) (Crear una suscripción de inserción).  
  
 Para especificar la información de conexión para suscripciones de extracción, vea [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) (Crear una suscripción de extracción).  
  
## <a name="merge-agent"></a>Agente de mezcla  
 Cada suscripción de mezcla tiene su propio Agente de mezcla que conecta y actualiza el publicador y el suscriptor.  
  
 Para especificar la información de conexión para suscripciones de inserción, vea [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md) (Crear una suscripción de inserción).  
  
 Para especificar la información de conexión para suscripciones de extracción, vea [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) (Crear una suscripción de extracción).  
  
## <a name="immediate-updating-subscriptions"></a>Suscripciones de actualización inmediata  
 Al configurar una suscripción de actualización inmediata, se especifica una cuenta en el suscriptor con la que se realizan las conexiones al publicador. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Hay tres opciones disponibles para el tipo de conexión:  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales especificadas durante la configuración.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales del usuario que realiza el cambio en el suscriptor.  
  
-   Un servidor vinculado o un servidor remoto previamente definido.  
  
> [!IMPORTANT]  
>  Para especificar la información de conexión, use el procedimiento almacenado [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). También puede usar la página **Inicio de sesión para suscripciones actualizables** del Asistente para nueva suscripción, que llama a **sp_link_publication**. En ciertas condiciones, este procedimiento almacenado puede producir un error si el suscriptor ejecuta el Service Pack 1 (SP1) de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior y el publicador ejecuta una versión anterior. Si el procedimiento almacenado produce un error en estas circunstancias, actualice el publicador a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 o posterior.  
  
 Para más información, vea [Create an Updatable Subscription to a Transactional Publication](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) (Create an Updatable Subscription to a Transactional Publication) y [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) (Ver y modificar la configuración de seguridad de la replicación).  
  
> [!IMPORTANT]  
>  La cuenta especificada para la conexión solo debe tener permiso para insertar, actualizar y eliminar datos en las vistas que crea la replicación en la base de datos de publicaciones; no debe tener ningún permiso adicional. Conceda permisos para las vistas de la base de datos de publicación designadas con el formato **syncobj_** _\<HexadecimalNumber>_ a la cuenta que ha configurado en cada suscriptor.  
  
## <a name="queued-updating-subscriptions"></a>Suscriptores de actualización en cola  
 Al configurar suscripciones de actualización en cola, hay dos áreas relacionadas con la seguridad que debe tener en cuenta:  
  
-   Solo hay un Agente de lectura de cola para cada distribuidor. Para cada distribuidor, se recomienda configurar como máximo una publicación habilitada para las suscripciones de actualización en cola.  
  
-   El Agente de lectura de cola establece las conexiones con el distribuidor, el publicador y cada suscriptor:  
  
    -   La cuenta con la que se ejecuta el agente y establece conexiones con el distribuidor se especifica al crear el agente (si utiliza el Asistente para nueva publicación, el agente se crea al crear una publicación habilitada para suscripciones de actualización).  
  
    -   La cuenta con la que el agente establece conexiones con el publicador se especifica al configurar la distribución para un publicador. Especifique la cuenta de Windows con la que se ejecuta el agente o una cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   La cuenta con la que el agente establece conexiones con el suscriptor se especifica al crear la suscripción.  
  
    > [!IMPORTANT]  
    >  Utilice la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las conexiones con los suscriptores y especifique una cuenta distinta para la conexión con cada suscriptor. Si utiliza una suscripción de extracción, la replicación establece siempre la conexión para que utilice la autenticación de Windows (en las suscripciones de extracción, la replicación no tiene acceso a los metadatos de un suscriptor que deba usar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ). En este caso, cambie la conexión para que use la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] después de configurar la suscripción.  
  
     Para más información, vea: Cómo: Crear una suscripción de actualización en una publicación transaccional (SQL Server Management Studio) y [Ver y modificar la configuración de seguridad de la replicación](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección &#40;Replicación&#41;](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
