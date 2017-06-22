---
title: MSSQL_ENG020598 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020598 error
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 46ca28952a628032fc98fe0fb78f603c4101f726
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng020598"></a>MSSQL_ENG020598
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20598|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se encontró la fila en el suscriptor al aplicar el comando replicado.|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce en la replicación transaccional si el Agente de distribución intenta actualizar una fila en el suscriptor, pero la fila se ha eliminado o se ha cambiado su clave principal. De forma predeterminada, los suscriptores de publicaciones transaccionales deben tratarse como de solo lectura, porque los cambios no se propagan de vuelta al publicador. En la replicación transaccional, los cambios de usuario deben realizarse solo en el suscriptor si se utilizan suscripciones actualizables o replicación del mismo nivel. Para obtener información acerca de estas opciones, vea [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) y [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
## <a name="user-action"></a>Acción del usuario  
 **Para resolver este problema:**  
  
1.  Si la replicación debe continuar mientras identifica el origen del error, especifique el parámetro **SkipErrors 20598** para el agente de distribución. Esto permite al agente omitir los cambios que provocan el error 20598, a la vez que permite que se repliquen otros cambios.  
  
2.  Identifique qué filas del suscriptor se han eliminado o tienen una clave principal distinta que las filas correspondientes en el publicador. Puede utilizar la [tablediff Utility](../../tools/tablediff-utility.md) para determinar qué filas de las bases de datos de publicaciones y suscripciones son diferentes. Para obtener información sobre el uso de esta utilidad con bases de datos replicadas, vea [Comparar tablas replicadas para buscar diferencias &#40;programación de la replicación&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
3.  Corrija las filas del suscriptor con la utilidad **tablediff** u otro método.  
  
4.  (Opcional) Quite el parámetro **- SkipErrors** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
