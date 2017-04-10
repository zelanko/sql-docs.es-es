---
title: "Seguridad del Agente de distribuci&#243;n (replicaci&#243;n punto a punto) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.DA.f1"
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Seguridad del Agente de distribuci&#243;n (replicaci&#243;n punto a punto)
  El **seguridad del agente de distribución** página le permite especificar las cuentas en las que el agente de distribución se ejecuta y realiza conexiones a los equipos en una topología punto a punto. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas de seguridad de replicación, consulte [modelo de seguridad del agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md) y [recomendaciones de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Si el Agente de distribución de una suscripción ya se ha configurado en una ejecución anterior de este asistente, no se pueden cambiar las credenciales que utiliza en este asistente. Si especifica credenciales nuevas, se omitirán. Para cambiar las credenciales, utilice el cuadro de diálogo **Propiedades de suscripción** . Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Opciones  
 Haga clic en el botón de propiedades (**...**) en la fila para cada suscriptor tener acceso a la **seguridad del agente de distribución** cuadro de diálogo. Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de distribución** que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada elemento del mismo nivel.  
  
 **Base de datos del mismo nivel**  
 La base de datos del mismo nivel que servirá tanto de base de datos de publicaciones como de base de datos de suscripciones.  
  
 **Conexión al distribuidor**  
 Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente. Este asistente crea suscripciones de inserción (la conexión local es la conexión al distribuidor), por lo que este campo siempre mostrará: **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'**.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. La conexión se puede realizar utilizando el contexto de una cuenta de Windows con la que se ejecute el agente o en el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión ' \< inicio de sesión>'**, **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## Vea también  
 [Administrar una topología punto a punto & #40; Programación de replicación Transact-SQL & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  