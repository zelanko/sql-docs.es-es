---
title: "Proteger el publicador | Microsoft Docs"
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
  - "inicios de sesión [replicación de SQL Server], lista de acceso a la publicación"
  - "publicaciones [replicación de SQL Server], listas de acceso a la publicación"
  - "lista de acceso a la publicación (PAL)"
  - "PAL (lista de acceso a la publicación)"
  - "publicadores [replicación de SQL Server], seguridad"
  - "publicaciones [replicación de SQL Server], seguridad"
ms.assetid: 4513a18d-dd6e-407a-b009-49dc9432ec7e
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 48
---
# Proteger el publicador
  Los siguientes agentes de replicación se conectan al publicador:  
  
-   Agente de registro del LOG  
  
-   Agente de instantáneas  
  
-   Agente de lectura de cola  
  
-   Agente de mezcla  
  
 Se recomienda proporcionar un inicio de sesión adecuado para estos agentes, seguir el principio de conceder los derechos mínimos necesarios y proteger el almacenamiento de todas las contraseñas. Para obtener información acerca de los permisos necesarios para cada agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Además de administrar inicios de sesión y contraseñas correctamente, es necesario comprender el rol de la lista de acceso a la publicación (PAL). Esta lista se utiliza para permitir que los inicios de sesión tengan acceso a los datos de la publicación al tiempo que se restringe el acceso ad hoc a la base de datos en el publicador.  
  
## Lista de acceso a la publicación  
 La PAL es el mecanismo principal para proteger las publicaciones en el publicador. La PAL funciona de forma similar a las listas de control de acceso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Al crear una publicación, la replicación crea una PAL para dicha publicación. La PAL puede configurarse para que contenga una lista de los inicios de sesión y los grupos a los que se han concedido permiso de acceso a la publicación. Cuando un agente se conecta al publicador o al distribuidor y solicita acceso a una publicación, la información de autenticación de la PAL se compara con el inicio de sesión del publicador que proporciona el agente. Este proceso proporciona seguridad adicional para el publicador al impedir que una herramienta de cliente utilice el inicio de sesión del publicador y del distribuidor para realizar modificaciones directamente en el publicador.  
  
> [!NOTE]  
>  La replicación crea un rol en el publicador para cada publicación para exigir la pertenencia a la PAL. La función tiene un nombre con el formato **Msmerge_***\< Iddepublicación>* para la replicación de mezcla y **MSReplPAL_***\< Iddebasededatosdepublicaciones>***_***\< Iddepublicación>* para la replicación de instantáneas y transaccional.  
  
 Los inicios de sesión incluidos en la PAL de forma predeterminada son: los miembros del rol fijo de servidor **sysadmin** cuando se crea la publicación y el inicio de sesión utilizado para crear la publicación. De forma predeterminada, todos los inicios de sesión que son miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos en la base de datos de publicación puede suscribirse a una publicación sin agregarse explícitamente a la PAL.  
  
 Cuando utilice la PAL, tenga en cuenta las siguientes directrices:  
  
-   Debe asociar el inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un usuario de la base de datos de publicaciones antes de agregar el inicio de sesión a la PAL.  
  
-   Respete el principio de privilegios mínimos proporcionando a los inicios de sesión de la PAL solo los permisos que necesitan para realizar tareas de replicación. No agregue los inicios de sesión a los roles fijos de base de datos ni a los roles de servidor que no sean necesarios para replicación. Para obtener más información acerca de los permisos necesarios, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
-   Si se utiliza un distribuidor remoto, las cuentas de la lista de acceso de la publicación deben estar disponibles tanto en el publicador como en el distribuidor. La cuenta debe ser una cuenta de dominio o una cuenta local que esté definida en ambos servidores. Las contraseñas asociadas a ambos inicios de sesión deben ser iguales.  
  
-   Si la PAL contiene cuentas de Windows y el dominio utiliza Active Directory, la cuenta con la que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener permisos de lectura en Active Directory. Si tiene problemas con cuentas de Windows, asegúrese de que la cuenta con la que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene permisos suficientes. Para obtener más información, consulte la documentación de Windows.  
  
 Para administrar la PAL, consulte [administrar inicios de sesión en la lista de acceso](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md).  
  
## Agente de instantáneas  
 Existe un Agente de instantáneas para cada publicación. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## Entrega de instantáneas a través de FTP  
 Si especifica que las instantáneas deben estar disponibles a través de un recurso compartido FTP en lugar de un recurso compartido UNC, es preciso indicar un inicio de sesión y una contraseña al configurar el acceso FTP. Para obtener más información, consulte [entregar una instantánea mediante FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## Agente de registro del LOG  
 Existe un Agente de registro del LOG para cada base de datos publicada para la replicación transaccional. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
## Agente de lectura de cola  
 Existe un Agente de lectura de cola para todos los publicadores y publicaciones (que permite las suscripciones de actualización en cola) asociados a un distribuidor determinado. Para obtener más información, consulte [Habilitar suscripciones de actualización para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).  
  
## Vea también  
 [Habilitar conexiones cifradas en el motor de base de datos & #40; Administrador de configuración de SQL Server & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Prácticas recomendadas de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  