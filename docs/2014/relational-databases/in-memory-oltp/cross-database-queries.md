---
title: Consultas entre bases de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6e829bc3bc7216532bd76f083335f126166347f4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706518"
---
# <a name="cross-database-queries"></a>Consultas entre bases de datos
  En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], las tablas optimizadas para memoria no admiten las transacciones entre bases de datos. No puede tener acceso a otra base de datos desde la misma transacción o desde la misma consulta que tiene acceso también a una tabla optimizada para memoria. No puede copiar fácilmente los datos de una tabla de una base de datos en una tabla optimizada para memoria de otra base de datos.  
  
 Las variables de tabla no son transaccionales. Por tanto, se pueden utilizar las variables de tabla optimizada para memoria en consultas entre bases de datos y pueden así facilitar la migración de datos de una base de datos a tablas optimizadas para memoria de otra. Puede utilizar dos transacciones. En la primera transacción, inserte los datos de la tabla remota en la variable. En la segunda transacción, inserte los datos en la tabla optimizada para memoria local desde la variable.  
  
 Por ejemplo, para copiar la fila de la tabla T1 de la base de datos db1 en la tabla T2 de DB2, utilizando la variable @v1 de tipo DBO. TT1, puede usar algo parecido a lo siguiente:  
  
```sql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
