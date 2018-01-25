---
title: Perfiles de agente (un solo agente) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.profiles.perfprofileagentname.f1
helpviewer_keywords: Agent Profile dialog box
ms.assetid: 22713555-c496-4ce1-8ec7-4ae75cfadca8
caps.latest.revision: "18"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6984179c2dacffa2d6c2ebcb816114e1fcfdcfd0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="agent-profiles-single-agent"></a>Perfiles de agente (un solo agente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use el cuadro de diálogo **Perfiles de agente** para administrar los perfiles de un agente. Los perfiles de agente proporcionan una manera cómoda de administrar los parámetros en tiempo de ejecución para cada agente. Cada agente tiene un perfil predeterminado y algunos tienen perfiles adicionales predefinidos. Por ejemplo, el Agente de mezcla tiene un perfil de "vínculo lento" diseñado para conexiones de banda ancha lentas. Los perfiles predefinidos son suficientes para la mayoría de las aplicaciones, pero también pueden crearse perfiles definidos por el usuario, que permiten personalizar el comportamiento del agente.  
  
## <a name="options"></a>.  
 **Predeterminado para nuevos**  
 Seleccione el perfil que se utilizará al crear los trabajos de un determinado tipo de agente. Por ejemplo, si crea varias suscripciones para una publicación de combinación, el trabajo del Agente de mezcla de cada suscripción utilizará el perfil seleccionado. Si desea cambiar el perfil de los trabajos existentes, seleccione un perfil y, a continuación, haga clic en **Cambiar agentes existentes**.  
  
 **Nombre**  
 El nombre del perfil.  
  
 **Tipo**  
 Indica el tipo de perfil: **Usuario** (definido por el usuario) o **Sistema** (predefinido).  
  
 **Propiedades (...)**  
 Haga clic para ver los valores utilizados por cada parámetro en el perfil del agente.  
  
 **Nueva**  
 Haga clic para crear un perfil nuevo.  
  
 **Eliminar**  
 Seleccione un perfil definido por el usuario y, a continuación, haga clic en **Eliminar** para eliminar ese perfil. Los perfiles predefinidos no se pueden eliminar.  
  
 **Cambiar agentes existentes**  
 Seleccione un perfil y, a continuación, haga clic en **Cambiar agentes existentes** para especificar que todos los trabajos existentes de un determinado tipo de agente deben utilizar el perfil seleccionado. Por ejemplo, si ha creado varias suscripciones para una publicación de combinación y desea cambiar el perfil para especificar que el trabajo del Agente de mezcla de cada una de esas suscripciones debe utilizar el **Perfil de agente de conexión lenta**, seleccione ese perfil y, a continuación, haga clic en **Cambiar agentes existentes**.  
  
## <a name="see-also"></a>Ver también  
 [Trabajar con perfiles del Agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Perfiles del Agente de replicación](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
