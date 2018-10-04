---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6804aac0a6212bf8c80762f44e88fdf9de2d28d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075577"
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21076|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La instantánea inicial del artículo '%1!' aún no está disponible.|  
  
## <a name="explanation"></a>Explicación  
 El error MSSQL_ENG021076 puede producirse si el Agente de distribución se inicia antes de que el Agente de instantáneas haya terminado de generar la instantánea. El error se produce solo si la publicación contiene un único artículo. Si la publicación contiene más de un artículo, en su lugar se produce el error MSSQL_ENG021075. Para más información, consulte [MSSQL_ENG021075](mssql-eng021075.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Si el Agente de instantáneas para la publicación no se ha iniciado desde que se creó la suscripción, o si no se ha iniciado desde la última vez que decidió reinicializar la suscripción, inicie el Agente de instantáneas y deje que se complete antes de iniciar el Agente de distribución. Para obtener más información, vea [Crear y aplicar una instantánea](create-and-apply-the-snapshot.md).  
  
 Si no finaliza el Agente de instantáneas, revise el historial del Agente de instantáneas para detectar posibles errores y soluciónelos. Para obtener información sobre la visualización del estado y los errores del agente del Monitor de replicación, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
