---
title: Nuevo perfil de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8549be8d4c8a40aaaa35c171e0d2183c7b490768
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104486"
---
# <a name="new-agent-profile"></a>Nuevo perfil de agente
  Utilice el cuadro de diálogo **Nuevo perfil de agente** para crear un perfil nuevo. Los perfiles nuevos siempre se basan en perfiles existentes, pero pueden modificarse para satisfacer los requisitos de la aplicación. Después de crear el perfil, éste puede aplicarse a trabajos de agente existentes y futuros en el cuadro de diálogo **Perfiles de agente** . Los valores de los parámetros de agente pueden modificarse en el cuadro de diálogo \<**Propiedades de <NombrePerfilAgente>**.  
  
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
  
  