---
title: Proteger el publicador | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- Publishers [SQL Server replication], security
- publications [SQL Server replication], security
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fe54bbb15a1a7480c1f3718cdc85e0fdc630efcc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004753"
---
# <a name="secure-the-publisher"></a>Proteger el publicador
  Los siguientes agentes de replicación se conectan al publicador:  
  
-   Agente de registro del LOG  
  
-   Agente de instantáneas  
  
-   Agente de lectura de cola  
  
-   Agente de mezcla  
  
 Se recomienda proporcionar un inicio de sesión adecuado para estos agentes, seguir el principio de conceder los derechos mínimos necesarios y proteger el almacenamiento de todas las contraseñas. Para obtener información acerca de los permisos necesarios para cada agente, vea [Replication Agent Security Model](replication-agent-security-model.md).  
  
 Además de administrar inicios de sesión y contraseñas correctamente, es necesario comprender el rol de la lista de acceso a la publicación (PAL). Esta lista se utiliza para permitir que los inicios de sesión tengan acceso a los datos de la publicación al tiempo que se restringe el acceso ad hoc a la base de datos en el publicador.  
  
## <a name="publication-access-list"></a>Lista de acceso a la publicación  
 La PAL es el mecanismo principal para proteger las publicaciones en el publicador. La PAL funciona de forma similar a las listas de control de acceso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Al crear una publicación, la replicación crea una PAL para dicha publicación. La PAL puede configurarse para que contenga una lista de los inicios de sesión y los grupos a los que se han concedido permiso de acceso a la publicación. Cuando un agente se conecta al publicador o al distribuidor y solicita acceso a una publicación, la información de autenticación de la PAL se compara con el inicio de sesión del publicador que proporciona el agente. Este proceso proporciona seguridad adicional para el publicador al impedir que una herramienta de cliente utilice el inicio de sesión del publicador y del distribuidor para realizar modificaciones directamente en el publicador.  
  
> [!NOTE]  
>  La replicación crea un rol en el publicador para cada publicación para exigir la pertenencia a la PAL. El rol tiene un nombre con el formato **Msmerge_** _\<PublicationID>_ para la replicación de mezcla y **MSReplPAL_** _\<PublicationDatabaseID>_ **_** _\<PublicationID>_ para la replicación transaccional y de instantáneas.  
  
 Los inicios de sesión incluidos en la PAL de forma predeterminada son: los miembros del rol fijo de servidor **sysadmin** cuando se crea la publicación y el inicio de sesión utilizado para crear la publicación. De forma predeterminada, todos los inicios de sesión miembros del rol fijo de servidor **sysadmin** o el rol fijo de base de datos **db_owner** en la base de datos de publicaciones pueden suscribirse a una publicación sin agregarse explícitamente a la PAL.  
  
 Cuando utilice la PAL, tenga en cuenta las siguientes directrices:  
  
-   Debe asociar el inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un usuario de la base de datos de publicaciones antes de agregar el inicio de sesión a la PAL.  
  
-   Respete el principio de privilegios mínimos proporcionando a los inicios de sesión de la PAL solo los permisos que necesitan para realizar tareas de replicación. No agregue los inicios de sesión a los roles fijos de base de datos ni a los roles de servidor que no sean necesarios para replicación. Para obtener más información acerca de los permisos necesarios, vea [Replication Agent Security Model](replication-agent-security-model.md) y [Replication Security Best Practices](replication-security-best-practices.md).  
  
-   Si se utiliza un distribuidor remoto, las cuentas de la lista de acceso de la publicación deben estar disponibles tanto en el publicador como en el distribuidor. La cuenta debe ser una cuenta de dominio o una cuenta local que esté definida en ambos servidores. Las contraseñas asociadas a ambos inicios de sesión deben ser iguales.  
  
-   Si la PAL contiene cuentas de Windows y el dominio utiliza Active Directory, la cuenta con la que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener permisos de lectura en Active Directory. Si tiene problemas con cuentas de Windows, asegúrese de que la cuenta con la que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene permisos suficientes. Para obtener más información, consulte la documentación de Windows.  
  
 Para administrar la PAL, vea [Manage Logins in the Publication Access List](manage-logins-in-the-publication-access-list.md) (Administrar inicios de sesión en la lista de acceso a la publicación).  
  
## <a name="snapshot-agent"></a>Agente de instantáneas  
 Existe un Agente de instantáneas para cada publicación. Para obtener más información, vea [Crear una suscripción](../publish/create-a-publication.md).  
  
## <a name="ftp-snapshot-delivery"></a>Entrega de instantáneas a través de FTP  
 Si especifica que las instantáneas deben estar disponibles a través de un recurso compartido FTP en lugar de un recurso compartido UNC, es preciso indicar un inicio de sesión y una contraseña al configurar el acceso FTP. Para obtener más información, vea [Entregar una instantánea mediante FTP](../publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="log-reader-agent"></a>Agente de registro del LOG  
 Existe un Agente de registro del LOG para cada base de datos publicada para la replicación transaccional. Para obtener más información, vea [Crear una suscripción](../publish/create-a-publication.md).  
  
## <a name="queue-reader-agent"></a>Agente de lectura de cola  
 Existe un Agente de lectura de cola para todos los publicadores y publicaciones (que permite las suscripciones de actualización en cola) asociados a un distribuidor determinado. Para más información, vea [Enable Updating Subscriptions for Transactional Publications](../publish/enable-updating-subscriptions-for-transactional-publications.md) (Habilitar suscripciones actualizables para publicaciones transaccionales).  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Seguridad de Replicación de SQL Server](view-and-modify-replication-security-settings.md)  
  
  
