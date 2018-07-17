---
title: MSSQL_ENG021385 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e93c9dc9f1374d6215f441f5430d0968870502f6
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353117"
---
# <a name="mssqleng021385"></a>MSSQL_ENG021385
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21385|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La instantánea no pudo procesar la publicación '%1!'. Puede deberse a un cambio de actividad de esquema activo o a la adición de nuevos artículos.|  
  
## <a name="explanation"></a>Explicación  
 Este error aparece si comienza a ejecutarse el Agente de instantáneas cuando hay cambios en curso en la base de datos de publicaciones, como adiciones o eliminaciones de artículos, y cambios de esquema en objetos publicados.  
  
## <a name="user-action"></a>Acción del usuario  
 Reinicie el Agente de instantáneas cuando finalicen los cambios en la base de datos de publicaciones. Para obtener más información, vea [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [Conceptos de los ejecutables del Agente de replicación](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Ver también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
