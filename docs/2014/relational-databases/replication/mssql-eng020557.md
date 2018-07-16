---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fae14de91b626fdb349f712f0311ccbe97929560
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315645"
---
# <a name="mssqleng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20557|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Cierre del agente. Para obtener más información, vea el trabajo '%s' en el historial de trabajos del Agente SQL Server.|  
  
## <a name="explanation"></a>Explicación  
 El agente de replicación se ha cerrado sin escribir un motivo en la tabla del historial adecuada o el agente se ha cerrado durante un proceso.  
  
## <a name="user-action"></a>Acción del usuario  
  
-   Reinicie el agente para ver si se ejecuta ahora correctamente. Para obtener más información, vea [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [Conceptos de los ejecutables del Agente de replicación](concepts/replication-agent-executables-concepts.md).  
  
-   Compruebe el historial del agente y el historial de trabajos para ver otros errores que se hayan producido aproximadamente a la misma hora. Para obtener información sobre el modo de ver el estado del agente y los detalles del error en el Monitor de replicación, vea los siguientes temas:  
  
    -   Para el Agente de instantáneas, el Agente de registro del LOG y el Agente de lectura de cola, vea [Cómo ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
    -   Para el Agente de distribución y el Agente de mezcla, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
-   Compruebe que la conectividad básica funciona entre los equipos a los que el agente tiene acceso y, a continuación, conéctese a cada equipo con una utilidad como **sqlcmd** . Para conectar, utilice la misma cuenta con la que el agente realiza las conexiones. Para obtener más información acerca de los permisos que necesita cada cuenta de agente, vea [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Si se producen errores al crear o aplicar una instantánea, compruebe los archivos del directorio de la instantánea.  
  
-   Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error y a mensajes de error adicionales. Para obtener más información acerca de la configuración del registro para replicación, vea el artículo [312292](http://support.microsoft.com/kb/312292)de Microsoft Knowledge Base.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
