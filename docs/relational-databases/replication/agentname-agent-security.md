---
title: Seguridad del agente &lt;NombreAgente&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a66173782ef133b5636b53d545dca698468b9f1b
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37360017"
---
# <a name="ltagentnamegt-agent-security"></a>Seguridad del agente &lt;NombreAgente&gt;
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **Seguridad del Agente \<NombreAgente>** permite especificar las cuentas con las que el Agente de distribución (para replicación transaccional y de instantáneas) o el Agente de mezcla (para replicación de mezcla) ejecuta y realiza conexiones con los equipos de una topología de replicación. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, consulte [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md) y [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Opciones  
 Haga clic en el botón de propiedades (**...**) de la fila de cada suscriptor para obtener acceso al cuadro de diálogo **Seguridad del Agente de distribución** o **Seguridad del Agente de mezcla** . Haga clic en **Ayuda** en el cuadro de diálogo que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada suscriptor.  
  
 **Conexión al distribuidor**  
 Se muestra para la replicación transaccional y de instantáneas. Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el agente:  
  
-   Para suscripciones de inserción, la conexión local es la conexión con el distribuidor, por lo que este campo muestra siempre: **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<Equipo>\\<inicioDeSesión\>'** para suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el campo se muestra una de las siguientes opciones: **Usar inicio de sesión '\<inicioDeSesión>'**, **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<equipo>\\<inicioDeSesión>\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión con el publicador y distribuidor**  
 Se muestra para la replicación de mezcla. Contexto en el que se realizan las conexiones al publicador y al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para suscripciones de inserción, la conexión local es la conexión con el publicador y el distribuidor, por lo que este campo muestra siempre: **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<Equipo>\\<inicioDeSesión\>'** para suscripciones de inserción.  
  
-   Para las suscripciones de extracción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra una de las opciones siguientes: **Usar inicio de sesión '\<inicioDeSesión>'**, **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<Equipo>\\<inicioDeSesión>\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente:  
  
-   Para suscripciones de extracción, la conexión local es la conexión con el suscriptor, por lo que este campo muestra siempre: **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<Equipo>\\<inicioDeSesión\>'** para suscripciones de inserción.  
  
-   Para las suscripciones de inserción, la conexión se puede realizar también bajo el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el campo se muestra una de las siguientes opciones: **Usar inicio de sesión '\<inicioDeSesión>'**, **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<equipo>\\<inicioDeSesión>\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## <a name="see-also"></a>Ver también  
 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Seguridad y protección &#40;Replicación&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
