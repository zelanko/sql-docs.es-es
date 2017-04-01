---
title: "Proteger el distribuidor | Microsoft Docs"
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
  - "seguridad [replicación de SQL Server], distribuidores"
  - "distribuidores [replicación de SQL Server], seguridad"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Proteger el distribuidor
  Al distribuidor se conectan los siguientes agentes de replicación: el Agente de registro del LOG, el Agente de instantáneas, el Agente de lectura de cola, el Agente de distribución y el Agente de mezcla. Es importante proporcionar un inicio de sesión adecuado para cada uno de estos agentes respetando el principio de conceder los derechos mínimos necesarios y proteger el almacenamiento de todas las contraseñas:  
  
-   Para obtener información acerca de cómo administrar inicios de sesión y contraseñas, consulte [administrar inicios de sesión y contraseñas en la replicación](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Para obtener información detallada acerca de los permisos exigidos para cada agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Además de administrar inicios de sesión y contraseñas de forma adecuada, es importante comprender la función de la **repl_distributor** vínculo con un servidor remoto y el **distributor_admin** cuenta.  
  
## Proteger la conexión del publicador al distribuidor  
 Para admitir la comunicación necesaria cuando los procedimientos almacenados administrativos se ejecutan en el publicador y actualizar la información en el distribuidor, la replicación configura automáticamente el servidor remoto **repl_distributor**. El **repl_distributor** entrada del servidor remoto se utiliza para la comunicación con la base de datos de distribución, independientemente de la base de datos de distribución está dentro de la instancia del publicador (distribuidor local) o reside en un equipo remoto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia (un distribuidor remoto).  
  
 Cuando la base de datos de distribución está incluida en una instancia local, se genera una contraseña aleatoria y se configura automáticamente. Cuando la base de datos de distribución se encuentra en una instancia remota, el administrador configura una contraseña compartida durante la instalación del publicador y del distribuidor; Esta contraseña, a continuación, se utiliza para proporcionar autenticación de tráfico que atraviesa el **repl_distributor** vínculo.  
  
 El distribuidor utiliza la **repl_distributor** entrada del servidor remoto para comprobar que el servidor que realiza la llamada está configurado como publicador en el distribuidor, valida la contraseña proporcionada por el publicador y valida que el procedimiento almacenado es una réplica de procedimiento almacenado durante la ejecución.  
  
 La contraseña configurada para la **repl_distributor** está asociado a la entrada del servidor remoto durante la instalación de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Inicio de sesión, **distributor_admin**, que se agrega a la **sysadmin** rol fijo de servidor en el distribuidor. El **distributor_admin** Inicio de sesión utiliza procedimientos almacenados de replicación al conectarse al distribuidor.  
  
> [!NOTE]  
>  No cambie la contraseña de la **distributor_admin** manualmente. Utilice siempre la **sp_changedistributor_password** procedimiento almacenado, o la **Propiedades del distribuidor** o **Actualizar contraseñas de replicación** cuadros de diálogo de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], porque los cambios de contraseña son publicaciones aplicadas a local automáticamente.  
  
## Seguridad de la carpeta de instantáneas  
 Asegúrese de que el recurso compartido de instantáneas tiene acceso de lectura a la cuenta con la que se ejecutan el Agente de mezcla (para la replicación de mezcla) o el Agente de distribución (para la replicación transaccional o de instantáneas), así como acceso de escritura a la cuenta con la que se ejecuta el Agente de instantáneas. Para obtener más información acerca de la carpeta de instantáneas, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## Vea también  
 [Ver y modificar la configuración de seguridad de la replicación](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Habilitar conexiones cifradas en el motor de base de datos & #40; Administrador de configuración de SQL Server & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [Prácticas recomendadas de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  