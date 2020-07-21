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
ms.openlocfilehash: 3b95cb43b9321a33be520ee480e3baf203aa4432
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010816"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>Seguridad del Agente de distribución (replicación punto a punto)
  La página **Seguridad del Agente de distribución** permite especificar las cuentas con las que el Agente de distribución se ejecuta y realiza conexiones con los equipos de una topología punto a punto. Para obtener información sobre los permisos requeridos por los agentes y las prácticas recomendadas que se aplican a la seguridad de replicación, vea [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md) y [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Si el Agente de distribución de una suscripción ya se ha configurado en una ejecución anterior de este asistente, no se pueden cambiar las credenciales que utiliza en este asistente. Si especifica credenciales nuevas, se omitirán. Para cambiar las credenciales, utilice el cuadro de diálogo **Propiedades de suscripción** . Para obtener más información, vea [ver y modificar la configuración de seguridad](security/view-and-modify-replication-security-settings.md)de la replicación.  
  
## <a name="options"></a>Opciones  
 Haga clic en el botón de propiedades (**...**) de la fila de cada suscriptor para tener acceso al cuadro de diálogo **Seguridad del Agente de distribución** . Haga clic en **Ayuda** en el cuadro de diálogo **Seguridad del Agente de distribución** que se muestra para obtener más información sobre los permisos requeridos para las cuentas utilizadas por los agentes.  
  
 Una vez especificadas las opciones en uno de los cuadros de diálogo, la información de conexión del suscriptor aparece en la cuadrícula.  
  
 **Agente para el suscriptor**  
 El nombre de cada elemento del mismo nivel.  
  
 **Base de datos del mismo nivel**  
 La base de datos del mismo nivel que servirá tanto de base de datos de publicaciones como de base de datos de suscripciones.  
  
 **Conexión al distribuidor**  
 Contexto en el que se realiza la conexión al distribuidor. Las conexiones locales se realizan siempre utilizando el contexto de la cuenta de Windows con la que se ejecuta el agente. Este asistente crea suscripciones de extracción (la conexión local es la conexión al distribuidor), por lo que este campo muestra siempre: **Suplantar ' \<Domain> \\<inicio de sesión \> '** o **Suplantar ' \<Computer> \\<inicio de sesión \> '**.  
  
 **Conexión al suscriptor**  
 Contexto en el que se realiza la conexión al suscriptor. La conexión se puede realizar utilizando el contexto de una cuenta de Windows con la que se ejecute el agente o en el contexto de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El campo muestra uno de los siguientes: **Usar inicio de sesión ' \<Login> '**, **Suplantar ' \<Domain> \\<inicio de sesión \> '** o **Suplantar ' \<Computer> \\<inicio de sesión \> '**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que todas las conexiones se realicen utilizando el contexto de la cuenta de Windows.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar una topología punto a punto &#40;la programación de la replicación con Transact-SQL&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
