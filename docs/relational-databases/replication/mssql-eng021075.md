---
title: "MSSQL_ENG021075 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG021075"
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021075
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21075|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La instantánea inicial de la publicación '%1!' aún no está disponible.|  
  
## Explicación  
 El error MSSQL_ENG021075 aparece cuando se inicia el Agente de distribución o de mezcla antes de que el Agente de instantáneas termine de generar la instantánea.  
  
## Acción del usuario  
 Si no se ha iniciado el Agente de instantáneas para la publicación desde que se creó la suscripción o desde la última vez que eligió reinicializar la suscripción, inícielo y espere a que termine antes de iniciar el Agente de distribución o de mezcla. Para obtener más información, consulte [crear y aplicar la instantánea](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Si no finaliza el Agente de instantáneas, revise el historial del Agente de instantáneas para detectar posibles errores y soluciónelos. Para obtener información acerca de cómo ver los detalles de error y de estado del agente en el Monitor de replicación, consulte [Ver información y realizar tareas para los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
 Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  