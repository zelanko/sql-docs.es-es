---
title: "Seguridad del Agente de registro del LOG (replicación punto a punto) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b670e48c6859dfaad38b9383fb3e2056fa47994
ms.lasthandoff: 04/11/2017

---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Seguridad del Agente de registro del LOG (replicación punto a punto)
  La página **Seguridad del Agente de registro del LOG** permite especificar las cuentas bajo las cuales el Agente de registro del LOG de cada nodo del mismo nivel se ejecuta y establece conexiones. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, vea [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md) y [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Existe un Agente de registro del LOG para cada base de datos que se publica utilizando la replicación transaccional. Si el Agente de registro del LOG para una base de datos ya ha sido configurado (ya sea para una publicación en una ejecución anterior de este asistente o para otra publicación transaccional en la misma base de datos), no se pueden cambiar las credenciales que el agente utiliza en este asistente. Si especifica credenciales nuevas, se omitirán. Para cambiar las credenciales, utilice el cuadro de diálogo **Propiedades de la publicación** . Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opciones  
 Haga clic en el botón de propiedades (**...**) en la fila de cada nodo del mismo nivel para obtener acceso al cuadro de diálogo **Seguridad del Agente de registro del LOG** . Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de registro del LOG** que se inicia para obtener más información acerca de los permisos requeridos para las cuentas que utilizan los agentes.  
  
 Una vez que se ha especificado la configuración en el cuadro de diálogo, se muestra la información de conexión para el suscriptor en la cuadrícula.  
  
 **Agentes para el publicador**  
 Nombre de cada instancia de servidor del mismo nivel.  
  
 **Base de datos del mismo nivel**  
 Base de datos que actúa como base de datos de publicaciones y base de datos de suscripciones en cada nodo del mismo nivel.  
  
 **Conexión al distribuidor**  
 Contexto en el que se realiza la conexión al distribuidor. La conexión local con el distribuidor siempre se establece usando el contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente, de modo que este campo siempre mostrará **Suplantar '\<dominio>\\<inicioDeSesión\>'** o **Suplantar '\<equipo>\\<inicioDeSesión\>'**.  
  
 **Conexión al publicador**  
 Contexto bajo el cual se establece la conexión al publicador. La conexión al publicador se puede establecer utilizando un inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utilizando el contexto de la cuenta de Windows bajo la que se ejecuta el agente. En el campo se muestra una de las siguientes opciones: **Usar inicio de sesión '\<inicioDeSesión>'**, **Suplantar '\<Dominio>\\<inicioDeSesión\>'** o **Suplantar '\<equipo>\\<inicioDeSesión>\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## <a name="see-also"></a>Vea también  
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
