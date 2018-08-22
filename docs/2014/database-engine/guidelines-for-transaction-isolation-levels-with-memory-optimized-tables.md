---
title: Directrices para los niveles de aislamiento de transacciones con tablas optimizadas para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e365e9ca-c34b-44ae-840c-10e599fa614f
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 456922a60eb0d5544c2cdb7992979fea59c3da66
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394334"
---
# <a name="guidelines-for-transaction-isolation-levels-with-memory-optimized-tables"></a>Instrucciones para los niveles de aislamiento de transacciones con tablas con optimización para memoria
  En muchos casos, debe especificar el nivel de aislamiento de transacción. El aislamiento de transacción para las tablas optimizadas para memoria difiere de las tablas basadas en disco.  
  
 Requisitos para especificar el nivel de aislamiento de transacción:  
  
-   TRANSACTION ISOLATION LEVEL es una opción necesaria para el bloque ATOMIC que comprende el contenido de un procedimiento almacenado compilado de forma nativa.  
  
-   Debido a las restricciones de uso del nivel de aislamiento en las transacciones entre contenedores, el uso de tablas optimizadas para memoria en [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado debe ir acompañado con frecuencia de una sugerencia de tabla que especifique el nivel de aislamiento usado para el acceso a la tabla. Para obtener más información sobre sugerencias de nivel de aislamiento y transacciones entre contenedores, consulte [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md).  
  
-   El nivel de aislamiento de transacción deseado debe declararse explícitamente. No es posible utilizar sugerencias de bloqueo (como XLOCK) para garantizar el aislamiento de algunas filas o tablas de la transacción.  
  
-   La aplicación que tiene acceso a la base de datos debe implementar lógica de reintentos para tratar los errores resultantes de conflictos de invalidación de transacciones, errores de validación y errores de dependencia de confirmación. Tenga en cuenta que pueden producirse errores de dependencia de confirmación incluso con transacciones de solo lectura.  
  
-   Deben evitarse transacciones de ejecución prolongada con tablas optimizadas para memoria. Estas transacciones aumentan la probabilidad de conflictos y la terminación de las siguientes transacciones. Una transacción de larga duración también pospone la recolección de elementos no utilizados. Cuanto más tiempo dure la ejecución de una transacción, más tiempo conserva OLTP en memoria las versiones de filas recién eliminadas, lo que puede reducir el rendimiento de la búsqueda de transacciones nuevas.  
  
 Las tablas basadas en disco se suelen basar en el bloqueo y en el bloqueo del aislamiento de las transacciones. Las tablas con optimización para memoria dependen del control de varias versiones y de la detección de conflictos para garantizar el aislamiento. Para obtener más información, vea la sección sobre la detección de conflictos, validación y comprobaciones de dependencia de confirmación en [transacciones en tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Las tablas basadas en disco permiten el control de varias versiones con los niveles de aislamiento SNAPSHOT y READ_COMMITTED_SNAPSHOT. En el caso de tablas optimizadas para memoria, todos los niveles de aislamiento se basan en el control de varias versiones, incluidos REPEATABLE READ y SERIALIZABLE.  
  
## <a name="types-of-transactions"></a>Tipos de transacciones  
 Todas las consultas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecutan en el contexto de una transacción.  
  
 Hay tres tipos de transacciones en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Transacciones de confirmación automática. Si no hay ningún contexto de transacción activa y las transacciones implícitas no están establecidas en ON en la sesión, cada consulta tiene su propio contexto de transacción. La transacción se inicia cuando comienza la ejecución de la instrucción y se completa cuando finaliza la instrucción.  
  
-   Transacciones explícitas. El usuario inicia la transacción mediante una instrucción BEGIN TRAN o BEGIN ATOMIC explícita. La transacción se completa siguiendo la instrucción COMMITT y ROLLBACK o END correspondiente (en el caso de un bloque atomic).  
  
-   transacciones implícitas. Cuando la opción IMPLICIT_TRANSACTIONS se establece en ON, una transacción se inicia implícitamente siempre que el usuario ejecuta una instrucción y no hay un contexto de transacción activa. La transacción se completa mediante instrucciones COMMIT y ROLLBACK explícitas.  
  
## <a name="baseline-read-committed-isolation"></a>Aislamiento READ COMMITTED de línea base  
 READ COMMITTED es el nivel de aislamiento predeterminado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 El nivel de aislamiento READ COMMITTED garantiza que las transacciones no ven datos no confirmados de los cambios ajenos a la transacción actual. Es decir, la transacción solo lee los datos que se han confirmado en la base de datos o que la transacción actual ha modificado.  
  
 Todos los niveles de aislamiento admitidos para las tablas optimizadas para memoria proporcionan la garantía de lectura confirmada. Por tanto, si la transacción no requiere garantías más sólidas, puede utilizar cualquiera de los niveles de aislamiento admitidos para las tablas optimizadas para memoria. SNAPSHOT utiliza la menor cantidad de recursos del sistema, en comparación con otros niveles de aislamiento.  
  
 La garantía que proporciona el nivel de aislamiento SNAPSHOT (el menor nivel de aislamiento que se admite en las tablas optimizadas para memoria) incluye las garantías de READ COMMITTED. Cada instrucción de la transacción lee la misma versión coherente de la base de datos. No solo todas las filas leídas por la transacción se confirman en la base de datos, sino que todas las operaciones de lectura ven el conjunto de cambios realizados por el mismo conjunto de transacciones.  
  
 **Directriz**: si solo se requiere la garantía de aislamiento READ COMMITTED, use el aislamiento SNAPSHOT con procedimientos almacenados compilados de forma nativa y obtener acceso a tablas optimizadas para memoria mediante interpreta [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
 En las transacciones de confirmación automática, el nivel de aislamiento READ COMMITTED se asigna implícitamente en SNAPSHOT para las tablas optimizadas para memoria. Por tanto, si la configuración de sesión TRANSACTION ISOLATION LEVEL se establece en READ COMMITTED, no es necesario especificar el nivel de aislamiento mediante una sugerencia de tabla al tener acceso a tablas optimizadas para memoria.  
  
 En el siguiente ejemplo de transacción de confirmación automática se muestra una combinación entre una tabla Customers optimizada para memoria y una tabla normal [Order History], como parte de un lote ad hoc:  
  
```tsql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
SELECT *   
FROM dbo.Customers AS c   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id = oh.customer_id;  
```  
  
 El siguiente ejemplo de transacciones implícitas o explícitas muestra la misma combinación, pero esta vez en una transacción de usuario explícita. Se tiene acceso a la tabla optimizada para memoria Customers con aislamiento de instantánea, según indica la sugerencia de tabla WITH (SNAPSHOT), y a la tabla normal [Order History] con aislamiento de lectura confirmada:  
  
```tsql  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
GO  
BEGIN TRAN  
SELECT * FROM dbo.Customers c with (SNAPSHOT)   
LEFT JOIN dbo.[Order History] oh   
    ON c.customer_id=oh.customer_id  
…  
COMMIT  
```  
  
### <a name="operational-differences"></a>Diferencias operativas  
 Además de la garantía de lectura confirmada, también hay dos detalles de implementación de claves que las aplicaciones que usan tablas basadas en disco pueden emplear. Tenga en cuenta lo siguiente al convertir una tabla basada en disco a la que se tiene acceso con el aislamiento READ COMMITTED en una tabla optimizada para memoria a la que se tiene acceso con el aislamiento SNAPSHOT:  
  
-   La implementación del nivel de aislamiento READ COMMITTED para las tablas basadas en disco (suponiendo que READ_COMMITTED_SNAPSHOT es OFF) utiliza bloqueos para evitar conflictos entre los lectores y los escritores. Cuando un escritor comienza a actualizar una fila, adopta un bloqueo y no lo libera hasta que la transacción se confirma. Las operaciones de lectura están bloqueadas y esperarán hasta que las transacciones de escritura se confirmen.  
  
     Algunas aplicaciones pueden suponer que los lectores siempre esperan hasta que los escritores confirmen la operación, especialmente si hay algún tipo de sincronización entre las dos transacciones en el nivel de aplicación.  
  
     **Directriz:** aplicaciones no pueden confiar en comportamiento de bloqueo. Si una aplicación necesita sincronización entre transacciones simultáneas, esa lógica se puede implementar en la capa de aplicación o en el nivel de base de datos a través de [sp_getapplock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getapplock-transact-sql).  
  
-   En las transacciones que utilizan el aislamiento READ COMMITTED, cada instrucción ve la versión más reciente de las filas de la base de datos. Por consiguiente, las instrucciones posteriores ven los cambios en el estado de la base de datos.  
  
     Sondear una tabla con un bucle WHILE hasta que se encuentra una nueva fila es un ejemplo de un patrón de aplicación que utiliza esta suposición. Con cada iteración del bucle, la consulta verá las últimas actualizaciones de la base de datos.  
  
     **Directriz:** si una aplicación debe sondear una tabla optimizada en memoria para obtener las filas más recientes que se escriben en la tabla, mueva el bucle de sondeo fuera del ámbito de la transacción.  
  
     A continuación se muestra un patrón de aplicación de ejemplo que utiliza esta suposición. Sondear una tabla con un bucle WHILE hasta encontrar una nueva fila. En cada iteración del bucle, la consulta tendrá acceso a las últimas actualizaciones de la base de datos.  
  
 El siguiente script de ejemplo sondea la tabla t1 hasta que tiene una fila. Después quita una sola fila de la tabla para su procesamiento posterior.  
  
 Tenga en cuenta que la lógica de sondeo debe estar fuera del ámbito de la transacción, ya que utiliza aislamiento de instantánea para tener acceso a la tabla t1. Si se usa lógica de sondeo en el ámbito de una transacción, se crearía una transacción de ejecución prolongada, que es una práctica incorrecta.  
  
```tsql  
-- poll table  
WHILE NOT EXISTS (SELECT 1 FROM dbo.t1)  
BEGIN   
  -- if empty, wait and poll again  
  WAITFOR DELAY '00:00:01'  
END  
  
BEGIN TRANSACTION  
  DECLARE @id int  
  SELECT TOP 1 @id=id FROM dbo.t1 WITH (SNAPSHOT)  
  DELETE FROM dbo.t1 WITH (SNAPSHOT) WHERE id=@id  
  
  -- insert processing based on @id  
COMMIT  
```  
  
## <a name="locking-table-hints"></a>Sugerencias de bloqueo de tabla  
 Sugerencias de bloqueo ([sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)) como HOLDLOCK y XLOCK se pueden usar con las tablas basadas en disco para tener [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] realice más bloqueos de los necesarios para el nivel de aislamiento especificado.  
  
 Las tablas con optimización para memoria no usan bloqueos. Se pueden usar niveles de aislamiento superiores como REPEATABLE READ y SERIALIZABLE para declarar las garantías deseadas.  
  
 Las sugerencias de bloqueo no se admiten. En su lugar, declare las garantías necesarias a través de los niveles de aislamiento de transacción. (Se admite NOLOCK porque [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no adopta bloqueos en las tablas optimizadas para memoria. Tenga en cuenta que, a diferencia de las tablas basadas en disco, NOLOCK no implica el comportamiento READ UNCOMMITTED para las tablas optimizadas para memoria).  
  
## <a name="see-also"></a>Vea también  
 [Descripción de las transacciones en tablas optimizadas para memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Directrices para la lógica de reintento de transacciones en tablas optimizadas para memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)   
 [Niveles de aislamiento de transacción](../../2014/database-engine/transaction-isolation-levels.md)  
  
  
