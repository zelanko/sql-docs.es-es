---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23bd163d63fa3939e35facc49cb3be7f8f07ff91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63023215"
---
# <a name="mssql_eng021076"></a>MSSQL_ENG021076
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|21076|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La instantánea inicial del artículo '%1!' aún no está disponible.|  
  
## <a name="explanation"></a>Explicación  
 El error MSSQL_ENG021076 puede producirse si el Agente de distribución se inicia antes de que el Agente de instantáneas haya terminado de generar la instantánea. El error se produce solo si la publicación contiene un único artículo. Si la publicación contiene más de un artículo, en su lugar se produce el error MSSQL_ENG021075. Para más información, consulte [MSSQL_ENG021075](mssql-eng021075.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Si el Agente de instantáneas para la publicación no se ha iniciado desde que se creó la suscripción, o si no se ha iniciado desde la última vez que decidió reinicializar la suscripción, inicie el Agente de instantáneas y deje que se complete antes de iniciar el Agente de distribución. Para obtener más información, vea [Crear y aplicar una instantánea](create-and-apply-the-snapshot.md).  
  
 Si no finaliza el Agente de instantáneas, revise el historial del Agente de instantáneas para detectar posibles errores y soluciónelos. Para obtener información sobre la visualización del estado y los errores en Monitor de replicación, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
