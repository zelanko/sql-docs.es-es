---
title: Nuevo perfil de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0fcdca4d57b21855a959a876c0c9c9344487046b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060664"
---
# <a name="new-agent-profile"></a>Nuevo perfil de agente
  Utilice el cuadro de diálogo **Nuevo perfil de agente** para crear un perfil nuevo. Los perfiles nuevos siempre se basan en perfiles existentes, pero pueden modificarse para satisfacer los requisitos de la aplicación. Después de crear el perfil, éste puede aplicarse a trabajos de agente existentes y futuros en el cuadro de diálogo **Perfiles de agente** . Los valores de los parámetros del agente se pueden editar en el \<**AgentProfileName> cuadro de diálogo Propiedades * *.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre para el perfil.  
  
 **Descripción**  
 Escriba una descripción para el perfil.  
  
 **Parámetro**  
 Parámetros de agente incluidos en el perfil. El perfil en el que se basa el nuevo perfil no especifica necesariamente un valor para cada parámetro. Para ver todos los parámetros válidos para un agente determinado, desactive la casilla **Mostrar solo los parámetros utilizados en este perfil** . Para obtener una descripción de cada parámetro, vea:  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [Agente de registro del LOG de replicación](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [Replication Merge Agent](agents/replication-merge-agent.md)  
  
-   [Agente de lectura de cola de replicación](agents/replication-queue-reader-agent.md)  
  
 **Valor predeterminado**  
 Valor predeterminado para cada parámetro de agente.  
  
 **Valor**  
 Valor especificado para el parámetro en el perfil en el que se basa el perfil nuevo. Modifique este campo para todos los parámetros que desee cambiar.  
  
 **Mostrar solo los parámetros utilizados en este perfil**  
 Desactive esta opción si desea mostrar todos los parámetros válidos para un agente determinado.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con perfiles del Agente de replicación](agents/work-with-replication-agent-profiles.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Perfiles del Agente de replicación](agents/replication-agent-profiles.md)  
  
  
