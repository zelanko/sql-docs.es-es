---
title: "Seguridad del Agente de mezcla | Microsoft Docs"
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
  - "sql13.rep.security.MA.f1"
helpviewer_keywords: 
  - "Seguridad del Agente de mezcla, cuadro de diálogo"
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Seguridad del Agente de mezcla
  El cuadro de diálogo **Seguridad del Agente de mezcla** permite especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el Agente de mezcla. El Agente de mezcla se ejecuta en el distribuidor para las suscripciones de inserción y en el suscriptor para las suscripciones de extracción. La cuenta de Windows se denomina también *cuenta de proceso*porque el proceso del agente se ejecuta con dicha cuenta. Las opciones adicionales disponibles en el cuadro de diálogo dependen de cómo se tenga acceso al mismo:  
  
-   Si se tiene acceso al cuadro de diálogo desde el Asistente para nueva suscripción, también permite especificar el contexto para el que el Agente de mezcla realiza las conexiones con el suscriptor (para suscripciones de inserción) o con el publicador y el distribuidor (para las suscripciones de extracción). La conexión puede realizarse con la cuenta de Windows o en el contexto de una cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especifique.  
  
-   Si el cuadro de diálogo se tiene acceso desde el **Propiedades de suscripción** cuadro de diálogo, especifique el contexto en el que el agente de mezcla realiza conexiones haciendo clic en el botón de propiedades (**...**) en el **conexión de suscriptor** o **conexión de publicador** fila de ese cuadro de diálogo. Para obtener más información acerca del acceso a la **Propiedades de suscripción** cuadro de diálogo, vea [Ver y modificar propiedades de suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y cómo: [Ver y modificar propiedades de suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## Opciones  
 **Cuenta de proceso**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de mezcla.  
  
-   Para las suscripciones de inserción, la cuenta debe:  
  
    -   Ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de distribución.  
  
    -   Ser miembro de la PAL.  
  
    -   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
    -   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
-   Para las suscripciones de extracción, la cuenta debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción.  
  
 Si se suplanta la cuenta de proceso al realizar las conexiones serán necesarios permisos adicionales. Vea las secciones **Conectar al publicador y distribuidor** y **Conectar al suscriptor** a continuación.  
  
 La**Cuenta de proceso** no se puede especificar para suscripciones de extracción en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], ya que el Agente de mezcla no se ejecuta en instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al publicador y distribuidor**  
 Para las suscripciones de inserción, siempre se realizan las conexiones al publicador y distribuidor suplantando la cuenta especificada en la **cuenta de proceso** cuadro de texto.  
  
 Para las suscripciones de extracción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o bien usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que seleccione para suplantar la cuenta de Windows en lugar de utilizar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta.  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión debe:  
  
-   Ser miembro de la PAL.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de distribución (el usuario puede ser el usuario Guest).  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
 **Conectar al suscriptor**  
 Para las suscripciones de extracción, siempre se realizan las conexiones al suscriptor suplantando la cuenta especificada en la **cuenta de proceso** cuadro de texto.  
  
 Para las suscripciones de inserción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o mediante una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La cuenta de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta usada para la conexión al suscriptor debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción.  
  
## Vea también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  