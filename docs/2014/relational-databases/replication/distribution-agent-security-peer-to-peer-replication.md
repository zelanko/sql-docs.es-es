---
title: Seguridad del Agente de distribución (replicación punto a punto) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78d8baed7783459db79bb9facb0141cc570c4127
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765517"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>Seguridad del Agente de distribución (replicación punto a punto)
  La página **Seguridad del Agente de distribución** permite especificar las cuentas con las que el Agente de distribución se ejecuta y realiza conexiones con los equipos de una topología punto a punto. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, vea [Replication Agent Security Model](security/replication-agent-security-model.md) (Modelo de seguridad del Agente de replicación) y [Replication Security Best Practices](security/replication-security-best-practices.md) (Procedimientos recomendados de seguridad en la replicación).  
  
> [!NOTE]  
>  Si el Agente de distribución de una suscripción ya se ha configurado en una ejecución anterior de este asistente, no se pueden cambiar las credenciales que utiliza en este asistente. Si especifica credenciales nuevas, se omitirán. Para cambiar las credenciales, utilice el cuadro de diálogo **Propiedades de suscripción** . Para más información, consulte [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>Opciones  
 Haga clic en el botón de propiedades (**...**) de la fila de cada suscriptor para tener acceso al cuadro de diálogo **Seguridad del Agente de distribución** . Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de distribución** que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada elemento del mismo nivel.  
  
 **Base de datos del mismo nivel**  
 La base de datos del mismo nivel que servirá tanto de base de datos de publicaciones como de base de datos de suscripciones.  
  
 **Conexión al distribuidor**  
 Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente. Este asistente crea suscripciones de inserción (la conexión local es la conexión al distribuidor), por lo que este campo muestra siempre: **Suplantar '\<dominio >\\< inicio de sesión\>'** o **suplantar '\<equipo >\\< inicio de sesión\>'**.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. La conexión se puede realizar utilizando el contexto de una cuenta de Windows con la que se ejecute el agente o en el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión '\<inicio de sesión >'**, **suplantar '\<dominio >\\< inicio de sesión\>'** o **suplantar '\<equipo >\\< inicio de sesión\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## <a name="see-also"></a>Vea también  
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
