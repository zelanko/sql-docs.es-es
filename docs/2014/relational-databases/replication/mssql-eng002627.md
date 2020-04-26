---
title: MSSQL_ENG002627 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a102991d08085f093e08a068a3d3127c9d7f7fc6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62666701"
---
# <a name="mssql_eng002627"></a>MSSQL_ENG002627
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2627|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico|N/D|  
|Texto del mensaje|Infracción de la restricción '%.*ls'. No se puede insertar una fila de clave duplicada en el objeto '%.\*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Se trata de un error general que puede producirse independientemente de que la base de datos esté replicada o no. En las bases de datos replicadas, el error suele producirse cuando las claves principales no se han administrado adecuadamente en la topología. En un entorno distribuido es fundamental asegurarse de que no se inserta el mismo valor en una columna de clave principal o en otra columna única en más de un nodo. Entre las posibles causas figuran:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo. Tanto la replicación de mezcla como las suscripciones actualizables de la replicación transaccional ofrecen detección y resolución de conflictos, aunque es preferible insertar o actualizar una fila concreta solo en un nodo. La replicación transaccional del mismo nivel no ofrece detección y resolución de conflictos; exige que las inserciones y las actualizaciones estén divididas en particiones.  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura. Los suscriptores de publicaciones de instantáneas deben tratarse como de solo lectura, al igual que los suscriptores de publicaciones transaccionales, a menos que se utilicen suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
## <a name="user-action"></a>Acción del usuario  
 La acción que debe llevarse a cabo depende del motivo por el que se produjo el error:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo.  
  
     Independientemente del tipo de replicación utilizada, se recomienda que, siempre que sea posible, las inserciones y las actualizaciones se dividan en particiones, ya que esto reduce el procesamiento necesario para la detección y resolución de conflictos. En la replicación transaccional del mismo nivel, se exige dividir en particiones las inserciones y las actualizaciones. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md).  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura.  
  
     No inserte ni actualice filas en el suscriptor a menos que esté utilizando replicación de mezcla, replicación transaccional con suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
     En la replicación de mezcla y la replicación transaccional con suscripciones actualizables, las columnas de identidad deben ser administradas automáticamente por la replicación. En la replicación transaccional de punto a punto, es necesario administrarlas manualmente. Para más información, vea [Replicar columnas de identidad](publish/replicate-identity-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)   
 [Replicación de mezcla](merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
