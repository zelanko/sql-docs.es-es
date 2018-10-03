---
title: Seguridad del Agente de lectura de cola | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b0780016cce58223ebe2e5b14726e535a440f41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160335"
---
# <a name="queue-reader-agent-security"></a>Seguridad del Agente de lectura de cola
  El cuadro de diálogo **Seguridad del Agente de lectura de cola** le permitirá especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutará el Agente de lectura de cola y establecerá las conexiones locales al distribuidor. El agente se conecta al publicador a través de la cuenta especificada en el cuadro de diálogo **Propiedades del publicador** (disponible en el cuadro de diálogo **Propiedades del distribuidor** ); el agente se conectará al suscriptor a través del mismo contexto que el Agente de distribución para la suscripción. Para más información, consulte [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md).  
  
 La cuenta deberá ser válida y deberá especificarse la contraseña correcta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Cuenta de proceso**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de lectura de cola en el distribuidor. La cuenta de Windows que especifique debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** de la base de datos de distribución.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
## <a name="see-also"></a>Vea también  
 [Administrar inicios de sesión y contraseñas en la replicación](security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
