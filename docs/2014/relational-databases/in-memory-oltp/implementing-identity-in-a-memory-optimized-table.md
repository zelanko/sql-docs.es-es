---
title: Implementar IDENTITY en una tabla con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 591d86011ee769d054c069db98a40e2765b1ec27
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63157818"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>Implementar IDENTITY en una tabla con optimización para memoria
  IDENTITY(1, 1) se admite en una tabla optimizada para memoria. Sin embargo, las columnas de identidad con la definición de IDENTITY(x, y) donde x != 1 o y != 1 no se admiten en las tablas optimizadas para memoria. La solución para los valores de IDENTITY utiliza el objeto SEQUENCE ([Sequence Numbers](../sequence-numbers/sequence-numbers.md)).  
  
 Quite primero la propiedad IDENTITY de la tabla que está convirtiendo a OLTP en memoria. A continuación, defina un nuevo objeto SEQUENCE para la columna en la tabla. Los objetos SEQUENCE como las columnas de identidad se basan en la capacidad de crear valores DEFAULT para las columnas que utilizan la sintaxis NEXT VALUE FOR para obtener un nuevo valor de identidad. Puesto que los valores DEFAULT no se admiten en OLTP en memoria, es necesario pasar el valor SEQUENCE recién generado a la instrucción INSERT o a un procedimiento almacenado compilado de forma nativa que lleve a cabo la inserción. El ejemplo siguiente demuestra este patrón.  
  
```sql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 Después de realizar la inserción varias veces, verá valores que aumentan con una progresión continua en la columna [c1]. Este conjunto de resultados se genera utilizando un recorrido de tabla y un índice hash sin `ORDER BY`, por lo que las filas no están ordenadas.  
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
