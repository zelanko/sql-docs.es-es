---
title: "Seguridad del agente &lt;NombreAgente&gt; | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Seguridad del agente &lt;NombreAgente&gt;
  El **\< Nombreagente> seguridad del agente** página le permite especificar las cuentas en que el agente de distribución (para la replicación de instantáneas y transaccional) o el agente de mezcla (para la replicación de mezcla) ejecutan y realizan conexiones a los equipos en una topología de replicación. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas de seguridad de replicación, consulte [modelo de seguridad del agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md) y [recomendaciones de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Opciones  
 Haga clic en el botón de propiedades (**...**) en la fila para cada suscriptor tener acceso a la **seguridad del agente de distribución** o **seguridad del agente de mezcla** cuadro de diálogo. Haga clic en **Ayuda** en el cuadro de diálogo que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada suscriptor.  
  
 **Conexión al distribuidor**  
 Se muestra para la replicación transaccional y de instantáneas. Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de inserción, la conexión local es la conexión al distribuidor, por lo que este campo siempre mostrará: **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'** las suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión ' \< inicio de sesión>'**, **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión con el publicador y distribuidor**  
 Se muestra para la replicación de mezcla. Contexto en el que se realizan las conexiones al publicador y al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de inserción, la conexión local es la conexión al publicador y distribuidor, por lo que este campo siempre mostrará: **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'** las suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión ' \< inicio de sesión>'**, **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para las suscripciones de extracción, la conexión local es la conexión al suscriptor, por lo que este campo siempre mostrará: **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'** las suscripciones de inserción.  
  
-   Para las suscripciones de inserción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión ' \< inicio de sesión>'**, **suplantar ' \< dominio>\\< inicio de sesión\>'** o **suplantar ' \< equipo>\\< inicio de sesión\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## Vea también  
 [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  