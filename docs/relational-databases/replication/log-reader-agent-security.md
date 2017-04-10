---
title: "Seguridad del Agente de registro del LOG | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.LRA.f1"
helpviewer_keywords: 
  - "Seguridad del Agente de registro del LOG, cuadro de diálogo"
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Seguridad del Agente de registro del LOG
  El cuadro de diálogo **Seguridad del Agente de registro del LOG** permite especificar:  
  
-   La cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el Agente de registro del LOG en el distribuidor. La cuenta de Windows se denomina también *cuenta de proceso*porque el proceso del agente se ejecuta con dicha cuenta.  
  
-   El contexto en el que el Agente de registro del LOG realiza conexiones al publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La conexión se puede realizar suplantando la cuenta de Windows o en el contexto de la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifique.  
  
    > [!NOTE]  
    >  El Agente de registro del LOG realiza conexiones al publicador incluso cuando el publicador y el distribuidor se encuentran en el mismo equipo. El Agente de registro del LOG también realiza conexiones al distribuidor; dichas conexiones se llevan a cabo siempre suplantando la cuenta de Windows con la que se ejecuta el agente.  
  
     Para los publicadores de Oracle, especifique el contexto en el que el agente de lector del registro se conecta al publicador en el **Propiedades del publicador** cuadro de diálogo (disponible en la **Propiedades del distribuidor** cuadro de diálogo). Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## Opciones  
 **Cuenta de proceso**  
 Indique la cuenta de Windows con la que se ejecuta el Agente de registro del LOG en el distribuidor. La cuenta de Windows que especifique debe como mínimo pertenecer el **db_owner** rol fijo de base de datos en la base de datos de distribución.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al publicador**  
 Seleccione si el agente de lector del registro debe realizar conexiones al publicador suplantando la cuenta especificada en la **cuenta de proceso** cuadro de texto o utilizando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta. Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que seleccione para suplantar la cuenta de Windows en lugar de utilizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta.  
  
 La cuenta de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta usada para la conexión debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de publicación.  
  
## Vea también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  