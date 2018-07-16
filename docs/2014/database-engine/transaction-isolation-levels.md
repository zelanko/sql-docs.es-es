---
title: Niveles de aislamiento de transacción | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7fb341cb36e97fbd06f38363c84d87f975d23eed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329965"
---
# <a name="transaction-isolation-levels"></a>Niveles de aislamiento de transacción
  Los niveles de aislamiento siguientes se admiten en las transacciones que tienen acceso a las tablas optimizadas para memoria.  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 El nivel de aislamiento de transacción se puede especificar como parte del bloque ATOMIC de un procedimiento almacenado compilado de forma nativa. Para obtener más información, vea [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql). Cuando se tiene acceso a tablas optimizadas para memoria desde [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado, el nivel de aislamiento se puede especificar mediante sugerencias de nivel de tabla.  
  
 Debe especificar el nivel de aislamiento de transacción cuando defina un procedimiento almacenado compilado de forma nativa. Debe especificar el nivel de aislamiento en las sugerencias de tabla cuando tenga acceso a las tablas optimizadas para memoria desde las transacciones de usuario en [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado. Para obtener más información, consulte [directrices para los niveles de aislamiento de transacciones con tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 El nivel de aislamiento READ COMMITTED se admite para las tablas optimizadas para memoria con transacciones de confirmación automática. READ COMMITTED no es válido en transacciones de usuario o en un bloque atómico. READ COMMITTED no se admite con las transacciones de usuario explícitas o implícitas. El nivel de aislamiento READ_COMMITTED_SNAPSHOT se admite para las tablas optimizadas para memoria que tienen confirmación automática de la transacción y solo si la consulta no tiene acceso a ninguna tabla basada en disco. Además, las transacciones que se inician con [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado con aislamiento SNAPSHOT no pueden tener acceso a las tablas optimizadas para memoria. Las transacciones que usan [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado con el aislamiento REPEATABLE READ o SERIALIZABLE deben tener acceso a las tablas optimizadas para memoria que utilicen el aislamiento SNAPSHOT. Para obtener más información acerca de este escenario, consulte [transacciones entre contenedores](cross-container-transactions.md).  
  
 READ COMMITTED es el nivel de aislamiento predeterminado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Cuando el nivel de aislamiento de la sesión sea READ COMMITTED (o inferior), puede hacer lo siguiente:  
  
-   Usar explícitamente una sugerencia de nivel de aislamiento mayor para tener acceso a la tabla optimizada para memoria (por ejemplo, WITH (SNAPSHOT)).  
  
-   Especificar la opción `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`, que establecerá el nivel de aislamiento de las tablas optimizadas para memoria en SNAPSHOT (como si incluyera sugerencias WITH(SNAPSHOT) en cada tabla optimizada para memoria). Para obtener más información acerca de `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`, consulte [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 O bien, si el nivel de aislamiento de la sesión es READ COMMITTED, puede utilizar transacciones de confirmación automática.  
  
 Las transacciones SNAPSHOPT que se inician en [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado no pueden tener acceso a las tablas optimizadas para memoria.  
  
 Los niveles de aislamiento de transacción admitidos para las tablas optimizadas para memoria proporcionan las mismas garantías lógicas que las tablas basadas en disco. El mecanismo utilizado para ofrecer garantías del nivel de aislamiento es diferente.  
  
 En el caso de las tablas basadas en disco, la mayor parte de las garantías del nivel de aislamiento se implementan utilizando el bloqueo, lo que evita conflictos durante el mismo. En las tablas optimizadas para memoria, las garantías se aplican a través de un mecanismo de detección de conflictos, que evita la necesidad de usar bloqueos. La excepción es el aislamiento SNAPSHOT en tablas basadas en disco. Esto se implementa de forma similar al aislamiento SNAPSHOT en las tablas optimizadas para memoria usando un mecanismo de detección de conflictos.  
  
 SNAPSHOT  
 Este nivel de aislamiento especifica que los datos leídos por cualquier instrucción de una transacción serán la versión coherente, desde el punto de vista transaccional, de los datos existentes al comienzo de la transacción. La transacción únicamente puede reconocer las modificaciones de datos confirmadas antes del comienzo de la misma. Las instrucciones que se ejecuten en la transacción actual no verán las modificaciones de datos efectuadas por otras transacciones después del inicio de la transacción actual. Las instrucciones de una transacción obtienen una instantánea de los datos confirmados tal como se encontraban al comienzo de la transacción.  
  
 Las operaciones de escritura (actualizaciones, inserciones y eliminaciones) siempre se aíslan completamente de otras transacciones. Por tanto, las operaciones de escritura en una transacción SNAPSHOT pueden entrar en conflicto con las operaciones de escritura realizadas por otras transacciones. Cuando la transacción actual intenta actualizar o eliminar una fila que ha sido actualizada o eliminada por otra transacción que se confirmó tras iniciarse la transacción actual, la transacción finaliza con el siguiente mensaje de error.  
  
 Error 41302. La transacción actual intentó actualizar un registro en la tabla X que se ha actualizado desde que esta transacción se inició. Se anuló la transacción.  
  
 Cuando la transacción actual intenta insertar una fila con el mismo valor de clave principal que una fila que fue insertada por otra transacción que se confirmó antes que la transacción actual, habrá un error en la confirmación y el siguiente mensaje de error.  
  
 Error 41325. La transacción actual no pudo confirmarse debido a un error serializable de validación.  
  
 Si una transacción escribe en una tabla que se quita antes de que la transacción se confirme, la transacción termina con el mensaje de error siguiente:  
  
 Error 41305. La transacción actual no pudo confirmarse debido a un error repetible de validación de lectura.  
  
 REPEATABLE READ  
 Este nivel de aislamiento incluye las garantías proporcionadas por el nivel de aislamiento SNAPSHOT. Además, REPEATABLE READ garantiza que, para cualquier fila leída por la transacción, en el momento en que la transacción se confirma, la fila no ha sido cambiada por otra transacción. Cada operación de lectura en la transacción es repetible hasta el final de la misma.  
  
 Si la transacción actual ha leído alguna fila que haya sido actualizada por otra transacción que se ha confirmado antes que la transacción actual, se produce un error en la confirmación y se genera el mensaje de error siguiente.  
  
 Error 41305. La transacción actual no pudo confirmarse debido a un error repetible de validación de lectura.  
  
 SERIALIZABLE  
 Este nivel de aislamiento incluye las garantías que proporciona REPEATABLE READ. No han aparecido filas fantasma entre la instantánea y el final de la transacción. Las filas fantasma cumplen la condición de filtro de una selección, una actualización o una eliminación.  
  
 Se ejecuta la transacción como si no hubiera transacciones simultáneas. Todas las acciones que prácticamente se producen en un solo punto de serialización (tiempo de confirmación).  
  
 Si se infringe alguna de estas garantías, la transacción no puede confirmarse y genera el mensaje de error siguiente:  
  
 Error 41325. La transacción actual no pudo confirmarse debido a un error serializable de validación.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de las transacciones en tablas optimizadas para memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Directrices para los niveles de aislamiento de transacciones con tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Instrucciones para la lógica de reintento de transacciones en tablas optimizadas para memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
