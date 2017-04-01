---
title: "MSSQL_ENG002627 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG002627"
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG002627
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2627|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico|N/A|  
|Texto del mensaje|Infracción de la restricción '%.*ls'. No se puede insertar una clave duplicada en el objeto ' %.\*ls'.|  
  
## Explicación  
 Se trata de un error general que puede producirse independientemente de que la base de datos esté replicada o no. En las bases de datos replicadas, el error suele producirse cuando las claves principales no se han administrado adecuadamente en la topología. En un entorno distribuido es fundamental asegurarse de que no se inserta el mismo valor en una columna de clave principal o en otra columna única en más de un nodo. Entre las posibles causas figuran:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo. Tanto la replicación de mezcla como las suscripciones actualizables de la replicación transaccional ofrecen detección y resolución de conflictos, aunque es preferible insertar o actualizar una fila concreta solo en un nodo. La replicación transaccional del mismo nivel no ofrece detección y resolución de conflictos; exige que las inserciones y las actualizaciones estén divididas en particiones.  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura. Los suscriptores de publicaciones de instantáneas deben tratarse como de solo lectura, al igual que los suscriptores de publicaciones transaccionales, a menos que se utilicen suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
## Acción del usuario  
 La acción que debe llevarse a cabo depende del motivo por el que se produjo el error:  
  
-   Se están llevando a cabo inserciones y actualizaciones en una fila en más de un nodo.  
  
     Independientemente del tipo de replicación utilizada, se recomienda que, siempre que sea posible, las inserciones y las actualizaciones se dividan en particiones, ya que esto reduce el procesamiento necesario para la detección y resolución de conflictos. En la replicación transaccional del mismo nivel, se exige dividir en particiones las inserciones y las actualizaciones. Para obtener más información, consulte [replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
-   Se ha insertado una fila en un suscriptor que debería ser de solo lectura.  
  
     No inserte ni actualice filas en el suscriptor a menos que esté utilizando replicación de mezcla, replicación transaccional con suscripciones actualizables o replicación transaccional del mismo nivel.  
  
-   Se está utilizando una tabla con una columna de identidad, pero la columna no está correctamente administrada.  
  
     En la replicación de mezcla y la replicación transaccional con suscripciones actualizables, las columnas de identidad deben ser administradas automáticamente por la replicación. En la replicación transaccional de punto a punto, es necesario administrarlas manualmente. Para obtener más información, consulte [replicar las columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replicación de mezcla](../../relational-databases/replication/merge/merge-replication.md)   
 [Replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  