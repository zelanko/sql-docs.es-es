---
title: Transacciones entre contenedores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5d84b51a-ec17-4c5c-b80e-9e994fc8ae80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290aff0bfcb01e098ae87b48cf582cdf999314c4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62807429"
---
# <a name="cross-container-transactions"></a>Transacciones entre contenedores
  Las transacciones entre contenedores son transacciones de usuario implícitas o explícitas que incluyen llamadas a procedimientos almacenados compilados de forma nativa u operaciones en tablas optimizadas para memoria.  
  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], las llamadas a procedimientos almacenados no inician una transacción. Las ejecuciones de procedimientos compilados de forma nativa en modo de confirmación automática (no en el contexto de una transacción de usuario) no se consideran transacciones entre contenedores.  
  
 Cualquier consulta interpretada que hace referencia a tablas optimizadas para memoria se considera parte de una transacción entre contenedores, tanto si se ejecuta desde una transacción explícita o implícita como si se ejecuta en modo de confirmación automática.  
  
##  <a name="isolation-of-individual-operations"></a><a name="isolation"></a>Aislamiento de operaciones individuales  
 Cada transacción de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un nivel de aislamiento. El nivel de aislamiento predeterminado es Lectura confirmada. Para usar un nivel de aislamiento diferente, puede establecer el nivel de aislamiento mediante [SET TRANSACTION ISOlation level &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 Suele ser necesario realizar operaciones en tablas optimizadas para memoria en otro nivel de aislamiento diferente al de las operaciones en tablas basadas en disco. En una transacción, es posible establecer otro nivel de aislamiento diferente para una colección de instrucciones o para una operación de lectura individual.  
  
### <a name="specifying-the-isolation-level-of-individual-operations"></a>Especificar el nivel de aislamiento de operaciones individuales  
 Para establecer otro nivel de aislamiento para un conjunto de instrucciones de una transacción, puede utilizar `SET TRANSACTION ISOLATION LEVEL`. En el siguiente ejemplo de una transacción se utiliza el nivel de aislamiento serializable como predeterminado. Las operaciones de inserción y selección en t3, t2 y t1 se ejecutan con aislamiento de lectura repetible.  
  
```sql  
set transaction isolation level serializable  
go  
  
begin transaction  
 ......  
  set transaction isolation level repeatable read  
  
  insert t3 select * from t1 join t2 on t1.id=t2.id  
  
  set transaction isolation level serializable  
 ......  
commit  
```  
  
 Para establecer un nivel de aislamiento para las operaciones de lectura individuales distinto del predeterminado de la transacción, puede usar una sugerencia de tabla (por ejemplo, serializable). Cada selección corresponde a una operación de lectura y cada actualización y eliminación corresponde a una lectura, ya que la fila siempre tiene que leerse para que se pueda actualizar o eliminar. Las operaciones de inserción no tienen un nivel de aislamiento porque las lecturas se aíslan siempre en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. En el ejemplo siguiente, el nivel de aislamiento predeterminado para la transacción es de lectura confirmada pero se tiene acceso a la tabla t1 con un aislamiento serializable y a t2 con aislamiento de instantánea.  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
 ......  
  
  insert t3 select * from t1 (serializable) join t2 (snapshot) on t1.id=t2.id  
  
  ......  
commit  
```  
  
### <a name="isolation-semantics-for-individual-operations"></a>Semántica de aislamiento para operaciones individuales  
 Una transacción T serializable se ejecuta en aislamiento completo. Es como si otra transacción se ha confirmado antes de que se iniciara T o se ha iniciado después confirmarse T. Se vuelve más compleja cuando operaciones diferentes en una transacción tienen niveles de aislamiento distintos.  
  
 La semántica general de los niveles de aislamiento de transacción [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]en, junto con las implicaciones en el bloqueo, se explica en [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 En el caso de transacciones entre contenedores en las que diferentes operaciones pueden tener niveles de aislamiento distintos, debe comprender la semántica del aislamiento de las operaciones de lectura individuales. Las operaciones de escritura se aíslan siempre. Las escrituras de transacciones diferentes no pueden verse afectadas entre sí.  
  
 Una operación de lectura de datos devuelve varias filas que satisfacen una condición de filtro.  
  
 Las lecturas se realizan como parte de una transacción T. los niveles de aislamiento para las operaciones de lectura se pueden entender en términos de,  
  
 Estado de confirmación  
 El estado de confirmación se refiere a si se garantiza que la lectura de los datos se va a confirmar.  
  
 Coherencia (Transaccional)  
 La coherencia transaccional para un conjunto de lecturas se refiere a si se garantiza que todas las lecturas de versiones de fila incluirán actualizaciones del mismo conjunto de transacciones.  
  
 La estabilidad garantiza que el sistema informa a la transacción T acerca de la lectura de los datos.  
 La estabilidad hace referencia a si las lecturas de la transacción son repetibles. Es decir, si las lecturas se repitieran, ¿devolverían las mismas filas y versiones de fila?  
  
 Algunas garantías hacen referencia a la hora de finalización lógica de la transacción. En general, la hora de finalización lógica es aquella en que la transacción se confirma en la base de datos. Si la transacción tiene acceso a tablas optimizadas para memoria, la hora de finalización lógica es técnicamente el principio de la fase de validación. (Para obtener más información, vea la descripción de la duración de las transacciones en las [transacciones en tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Independientemente del nivel de aislamiento, una transacción (T) siempre ve sus propias actualizaciones:  
  
 READ UNCOMMITTED  
 La lectura de datos no se puede confirmar, no es coherente ni es estable. Sin embargo, incluirá las operaciones de escritura anteriores realizadas por T.  
  
 READ COMMITTED  
 La lectura de datos se confirmará.  
  
 SNAPSHOT  
 Todas las operaciones de lectura realizadas por T con aislamiento de instantánea tienen la misma hora de lectura lógica, que es el inicio de la transacción. Se garantiza que la lectura de los datos se confirma y es coherente en la hora de lectura lógica. Se garantiza que si se repite una lectura tal y como está en la hora de lectura original, se devuelve el mismo resultado.  
  
 REPEATABLE READ  
 Se garantiza que la lectura de datos se confirma y es estable hasta la hora de finalización lógica de la transacción.  
  
 SERIALIZABLE  
 Todas las garantías de la prevención y la coherencia de las transacciones de lectura REPETIble y la coherencia transaccional con respecto a todas las operaciones de lectura serializable realizadas por T. la prevención ficticia significa que la operación de examen solo puede devolver filas adicionales escritas por T, pero no filas escritas por otras transacciones.  
  
 Considere la transacción siguiente,  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  -- remove all rows from t3; the related read operation is performed under read committed   
  -- isolation, as this is the default for the transaction  
  delete from t3  
  
  -- copy the contents from t1 to t3; the read on t1 is performed under the serializable   
  -- isolation level  
  insert t3 select * from t1 (serializable)  
  
  -- compare t3 and t1; note: the result set may not be empty, as rows may have been added   
  -- by other transaction before this select, due to the read committed isolation level  
  select * from t3 except t1  
  
  -- compare t1 and t3; note: the result set is empty, as no rows have been added to t1   
  -- since its contents were copied to t1, due to the serializable isolation level  
  select * from t1 except t3  
commit  
```  
  
 Esta transacción elimina todas las filas de la tabla t3 con aislamiento de lectura confirmada, copia todas las filas de t1 a t3 con aislamiento serializable y, a continuación, compara t1 y t3. Se pueden haber agregado a t3 algunas filas (no de t1) porque la tabla se vació. No se agregaron filas a t1 ya que la copia era serializable.  
  
 Aunque la lectura desde t1 al final de la transacción sea una lectura sintácticamente confirmada, es en efecto serializable, porque la misma lectura se realizó antes en la transacción bajo aislamiento serializable: la seriabilidad garantiza que, si la lectura se realiza en algún punto posterior de la transacción, se devuelven las mismas filas.  
  
## <a name="cross-container-transactions-and-isolation-levels"></a>Niveles de aislamiento y transacciones entre contenedores  
 Se puede considerar que una transacción entre contenedores tiene dos caras: una cara basada en disco (para las operaciones con tablas basadas en disco) y una cara optimizada para memoria (para las operaciones en tablas optimizadas para memoria). Estas dos caras pueden tener niveles de aislamiento diferentes. De hecho, las operaciones de lectura individuales en cada cara pueden tener distintos niveles de aislamiento.  
  
 La cara basada en disco de una transacción T determinada alcanza un cierto nivel de aislamiento X si se cumple una de las condiciones siguientes:  
  
-   Se inicia en X. Es decir, el valor predeterminado de la sesión era X, ya `SET TRANSACTION ISOLATION LEVEL`sea porque se ejecutó [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o es el valor predeterminado.  
  
-   Durante la transacción, el nivel de aislamiento predeterminado se cambia a X con `SET TRANSACTION ISOLATION LEVEL`.  
  
-   Una operación de lectura en una tabla basada en disco se ejecuta en el nivel de aislamiento X, utilizando la sintaxis `WITH (X)`.  
  
 La cara optimizada para memoria de T alcanza un nivel de aislamiento Y si durante la ejecución de T cualquier operación de lectura en una tabla optimizada para memoria o cualquier procedimiento almacenado compilado de forma nativa se ejecuta bajo el nivel de aislamiento Y.  
  
 Considere, por ejemplo, la siguiente transacción. Aquí, t1 y t2 son tablas basadas en disco y t3 y t4 son tablas optimizadas para memoria.  
  
 La cara basada en disco de la transacción alcanza el nivel de aislamiento de lectura confirmada, ya que se inició en ese nivel. La cara basada en disco también alcanza el nivel de lectura repetible, ya que la primera operación de lectura se ejecuta en ese nivel de aislamiento. La eliminación al final de la transacción se ejecuta en el nivel de aislamiento de lectura confirmada y, por tanto, no presenta un nuevo nivel de aislamiento.  
  
 La cara optimizada para memoria de la transacción puede alcanzar uno de dos niveles: si condition1 es true, llega al nivel serializable mientras que, si es false, la cara optimizada para memoria solo alcanza el aislamiento de instantánea.  
  
```sql  
set transaction isolation level read committed  
go  
  
begin transaction  
  select * from t1 (repeatableread)  
  
  if condition1 begin  
    insert t3 select * from t4 (serializable)  
  end  
  else begin  
    insert t3 select * from t4 (snapshot)  
  end  
  
  delete from t1  
commit  
```  
  
### <a name="supported-isolation-levels-for-cross-container-transactions"></a>Niveles de aislamiento admitidos para transacciones entre contenedores  
 Hay ciertas limitaciones en cuanto a los niveles de aislamiento utilizados con las operaciones en tablas optimizadas para memoria en transacciones entre contenedores.  
  
 Las tablas con optimización para memoria admiten los niveles de aislamiento SNAPSHOT, REPEATABLE READ y SERIALIZABLE. Para las transacciones de confirmación automática, las tablas optimizadas para memoria admiten el nivel de aislamiento READ COMMITTED.  
  
 Se admiten los escenarios siguientes:  
  
-   Las transacciones entre contenedores READ UNCOMMITTED, READ COMMITTED y READ_COMMITTED_SNAPSHOT pueden tener acceso a tablas optimizadas para memoria con el aislamiento SNAPSHOT, REPEATABLE READ y SERIALIZABLE. La garantía de READ COMMITTED se mantiene para la transacción; todas las filas leídas por la transacción se han confirmado en la base de datos.  
  
-   Las transacciones REPEATABLE READ y SERIALIZABLE pueden tener acceso a tablas optimizadas para memoria con aislamiento SNAPSHOT.  
  
## <a name="read-only-cross-container-transactions"></a>Transacciones entre contenedores de solo lectura  
 La mayoría de las transacciones de solo lectura en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se revierten en el tiempo de confirmación. Dado que no hay ningún cambio que confirmar en la base de datos, el sistema simplemente libera los recursos utilizados por la transacción. Para las transacciones basadas en disco de solo lectura, todos los bloqueos adoptados por la transacción se liberan en este momento. Para las transacciones optimizadas para memoria de solo lectura que abarcan una sola ejecución de procedimiento compilado de forma nativa, no se realiza ninguna validación.  
  
 Las transacciones de solo lectura entre contenedores en modo de confirmación automática se revierten simplemente al final de la transacción. No se realiza ninguna validación.  
  
 Las transacciones explícitas o implícitas de solo lectura entre contenedores realizan la validación en tiempo de confirmación si la transacción tiene acceso a tablas optimizadas para memoria en aislamiento REPEATABLE READ o SERIALIZABLE. Para obtener más información sobre la validación, vea la sección sobre detección de conflictos, validación y comprobaciones de dependencias de confirmación en [transacciones en tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de las transacciones en tablas optimizadas para memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Directrices para los niveles de aislamiento de transacción con tablas con optimización para memoria](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)   
 [Instrucciones para la lógica de reintento de transacciones en tablas con optimización para memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
