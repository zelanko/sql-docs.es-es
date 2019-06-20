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
manager: craigg
ms.openlocfilehash: 12fc3e7e7b67b9f02f2a9744d4af2af175ce0812
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022667"
---
# <a name="new-agent-profile"></a>Nuevo perfil de agente
  Utilice el cuadro de diálogo **Nuevo perfil de agente** para crear un perfil nuevo. Los perfiles nuevos siempre se basan en perfiles existentes, pero pueden modificarse para satisfacer los requisitos de la aplicación. Después de crear el perfil, éste puede aplicarse a trabajos de agente existentes y futuros en el cuadro de diálogo **Perfiles de agente** . Los valores de los parámetros de agente pueden modificarse en el cuadro de diálogo \<**Propiedades de <NombrePerfilAgente>**.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba un nombre para el perfil.  
  
 **Descripción**  
 Escriba una descripción para el perfil.  
  
 **Parámetro**  
 Parámetros de agente incluidos en el perfil. El perfil en el que se basa el nuevo perfil no especifica necesariamente un valor para cada parámetro. Para ver todos los parámetros válidos para un agente determinado, desactive la casilla **Mostrar solo los parámetros utilizados en este perfil** . Para obtener una descripción de cada parámetro, vea:  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [Agente de registro del LOG de replicación](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [Agente de mezcla de replicación](agents/replication-merge-agent.md)  
  
-   [Agente de lectura de cola de replicación](agents/replication-queue-reader-agent.md)  
  
 **Valor predeterminado**  
 Valor predeterminado para cada parámetro de agente.  
  
 **Valor**  
 Valor especificado para el parámetro en el perfil en el que se basa el perfil nuevo. Modifique este campo para todos los parámetros que desee cambiar.  
  
 **Mostrar solo los parámetros utilizados en este perfil**  
 Desactive esta opción si desea mostrar todos los parámetros válidos para un agente determinado.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con perfiles del Agente de replicación](agents/work-with-replication-agent-profiles.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Perfiles del Agente de replicación](agents/replication-agent-profiles.md)  
  
  
