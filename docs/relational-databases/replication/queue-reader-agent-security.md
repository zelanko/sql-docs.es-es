---
title: "Seguridad del Agente de lectura de cola | Microsoft Docs"
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
  - "sql13.rep.security.QRA.f1"
helpviewer_keywords: 
  - "Seguridad del Agente de lectura de cola, cuadro de diálogo"
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Seguridad del Agente de lectura de cola
  El cuadro de diálogo **Seguridad del Agente de lectura de cola** le permitirá especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutará el Agente de lectura de cola y establecerá las conexiones locales al distribuidor. El agente se conecta al publicador con la cuenta especificada en la **Propiedades del publicador** cuadro de diálogo (disponible en la **Propiedades del distribuidor** cuadro de diálogo); el agente se conecta al suscriptor con el mismo contexto que el agente de distribución para la suscripción. Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 La cuenta deberá ser válida y deberá especificarse la contraseña correcta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## Opciones  
 **Cuenta de proceso**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de lectura de cola en el distribuidor. La cuenta de Windows que especifique debe como mínimo pertenecer el **db_owner** rol fijo de base de datos en la base de datos de distribución.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
## Vea también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Información general sobre los agentes de replicación](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  