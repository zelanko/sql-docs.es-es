---
title: Las transacciones en tablas optimizadas para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cd07d26-a1f1-4034-8d6f-f196eed1b763
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3712e3b2e602bd403f4c1d312603577a4045a95a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393074"
---
# <a name="transactions-in-memory-optimized-tables"></a>Transacciones en tablas con optimización para memoria
  La versión de las filas de las tablas basadas en disco (con el aislamiento de instantánea o READ_COMMITTED_SNAPSHOT) proporciona una forma de control de simultaneidad optimista. Los lectores y los escritores no se bloquean entre sí. Con las tablas optimizadas para memoria, los escritores no bloquean a los escritores. Con las versiones de fila de las tablas basadas en disco, una transacción cierra la fila y se bloquean las transacciones simultáneas que intentan actualizar la fila. Con las tablas optimizadas para memoria, no hay bloqueos. En su lugar, si dos transacciones intentan actualizar la misma fila, se produciría un conflicto de escritura/escritura (error 41302).  
  
 A diferencia de las tablas basadas en disco, las tablas optimizadas para memoria permiten un control de simultaneidad optimista con los mayores niveles de aislamiento, REPEATABLE READ y SERIALIZABLE. Los bloqueos no se adoptan para exigir los niveles de aislamiento. En su lugar, al final de la transacción, la validación garantiza las suposiciones de seriabilidad o de lectura repetible. Si las suposiciones se infringen, la transacción se termina. Para obtener más información, vea [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md).  
  
 La semántica de transacciones importantes para las tablas optimizadas para memoria es:  
  
-   Multiversión  
  
-   Aislamiento de transacción basada en instantánea  
  
-   Optimistic  
  
-   Detección de conflictos  
  
 Cada uno de estos elementos de la semántica se explica en las secciones siguientes.  
  
## <a name="multi-versioning-in-memory-optimized-tables"></a>Multiversión en tablas con optimización para memoria  
 Las filas de las tablas optimizadas para memoria pueden tener distintas versiones. Las transacciones simultáneas tienen acceso a versiones posiblemente diferentes de la misma fila.  
  
 Los datos de las tablas con optimización para memoria están basados en versiones. Para una fila, puede haber varias versiones de fila diferentes que sean válidas en momentos distintos. Las tablas basadas en disco mantienen varias versiones de fila distintas, si READ_COMMITTED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION están establecidos en ON. Las tablas con optimización para memoria mantienen diferentes versiones de fila, incluso si READ_COMMITTED_SNAPSHOT y ALLOW_SNAPSHOT_ISOLATION se establecen en OFF. Las versiones de fila de las tablas optimizadas para memoria no se mantienen en tempdb. En su lugar, las versiones de fila se mantienen insertadas, como parte de las estructuras de datos optimizados para memoria que almacenan las filas en memoria.  
  
## <a name="snapshot-based-transaction-isolation-for-memory-optimized-tables"></a>Aislamiento de transacciones basado en instantáneas para las tablas con optimización para memoria  
 Todas las operaciones de una sola transacción utilizan la misma instantánea coherente desde el punto de vista de las transacciones de las tablas optimizadas para memoria. Todo el aislamiento de transacciones para las tablas optimizadas para memoria se basan en las instantáneas. Por ejemplo, una transacción que usa el nivel de aislamiento serializable para tener acceso a las tablas optimizadas para memoria realizará todas las operaciones en la misma instantánea coherente desde el punto de vista de las transacciones.  
  
 Las transacciones que tienen acceso a las tablas optimizadas para memoria utilizan esta versión de fila para obtener una instantánea coherente con las transacciones de las filas de las tablas. Los datos leídos por cualquier instrucción de la transacción serán la versión coherente, desde el punto de vista transaccional, de los datos existentes en el momento en que la transacción se iniciara. Por tanto, las modificaciones realizadas simultáneamente ejecutando transacciones no son visibles para las instrucciones de la transacción actual.  
  
## <a name="optimistic-concurrency-control-for-memory-optimized-tables"></a>Control de simultaneidad optimista para las tablas con optimización para memoria  
 Los conflictos y errores son poco frecuentes y las transacciones en tablas optimizadas para memoria suponen que no hay ningún conflicto con transacciones simultáneas y que las operaciones se realizan correctamente. Las transacciones no utilizan bloqueos ni bloqueos temporales en tablas optimizadas para memoria al objeto de garantizar el aislamiento de las transacciones. Los escritores no bloquean a los lectores. Los escritores no bloquean a los escritores. En su lugar, las transacciones continúan con la suposición (optimista) de que no habrá ningún conflicto con otras transacciones. Al no utilizar bloqueos ni bloqueos temporales y al no esperar a que otras transacciones finalicen el procesamiento de las mismas filas, se mejora el rendimiento.  
  
 Además, si una transacción (TxA) lee filas que otra transacción (TxB) ha insertado o modificado y está en proceso de confirmación, se supondrá de forma optimista la confirmación de la otra transacción, en lugar de esperar a que la confirmación se produzca. En este caso, la transacción TxA tendrá una dependencia de confirmación de la transacción TxB.  
  
## <a name="conflict-detection-validation-and-commit-dependency-checks"></a>Detección de conflictos, validación y comprobaciones de las dependencias de confirmación  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detecta conflictos entre las operaciones simultáneas, así como las infracciones del nivel de aislamiento y condenará una de las transacciones en conflicto. Esta transacción tendrá que volver a intentarse. (Para obtener más información, vea [Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)).  
  
 El sistema supone de forma optimista que no hay conflictos ni infracciones de aislamiento de transacciones. Los conflictos que puedan provocar incoherencias en la base de datos o puedan infringir el aislamiento de la transacción, se detectan y se termina la transacción.  
  
 Si se detecta un conflicto, se termina la transacción y el cliente tiene que volver a intentarlo.  
  
 En la tabla siguiente se resumen las condiciones de error de las transacciones que tienen acceso a las tablas optimizadas para memoria.  
  
### <a name="error-conditions-for-transactions-accessing-memory-optimized-tables"></a>Condiciones de error para las transacciones que tienen acceso a las tablas optimizadas para memoria.  
  
|Error|Escenario|  
|-----------|--------------|  
|Conflicto de escritura. Intentando actualizar un registro que se ha actualizado desde que la transacción se inició.|UPDATE o DELETE una fila que ha sido actualizada o eliminada por una transacción simultánea.|  
|Error de validación de lectura repetible|Una fila que la transacción leyó ha cambiado (se ha actualizado o eliminado) desde que se inició la transacción. La validación de lectura repetible suele producirse cuando se usan los niveles de aislamiento de transacción REPEATABLE READ y SERIALIZABLE.|  
|Error de validación serializable.|Una nueva fila (fantasma) se ha insertado en uno de los intervalos de recorrido en la transacción, desde que esta se inició. La fila habría estado visible para la transacción si la fila se hubiera confirmado en la base de datos antes de que la transacción comenzara. La validación SERIALIZABLE se produce normalmente cuando se usa el aislamiento SERIALIZABLE y la validación de restricciones PRIMARY KEY.|  
|Confirme el error de dependencia.|La transacción adoptó una dependencia en otra transacción, que no puede confirmarse, debido a uno de los errores de esta tabla, a una condición de memoria insuficiente o a que no puede confirmarse en el registro de transacciones. Este error puede aparecer con las transacciones de lectura/escritura y de solo lectura.|  
  
### <a name="transaction-lifetime"></a>Período de duración de las transacciones  
 Los errores enumerados en la tabla anterior pueden producirse en varios momentos durante una transacción. La ilustración siguiente muestra las fases de una transacción que tiene acceso a tablas optimizadas para memoria.  
  
 ![Duración de una transacción. ](../../2014/database-engine/media/hekaton-transactions.gif "Duración de una transacción.")  
Duración de una transacción que tiene acceso a tablas optimizadas para memoria.  
  
#### <a name="regular-processing"></a>Procesamiento normal  
 Durante esta fase, se ejecutan las instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] emitidas por el usuario. Las filas se leen de las tablas y las nuevas versiones de fila se escriben en la base de datos. La transacción se aísla de todas las demás transacciones simultáneas. La transacción utiliza la instantánea de las tablas optimizadas para memoria que existen en el momento de iniciarse la transacción.  
  
 Las acciones de escritura en las tablas en esta fase de la transacción ya no están visibles para otras transacciones, con una excepción: las actualizaciones de fila y las eliminaciones están visibles para las operaciones de actualización y eliminación en otras transacciones, con el fin de detectar conflictos de escritura.  
  
 Si una operación de actualización o de eliminación considera que se ha actualizado o se ha eliminado una fila desde el inicio lógico de la transacción, la operación producirá el error 41302. El mensaje del error 41302 es “La transacción actual intentó actualizar un registro en la tabla X que se ha actualizado desde que esta transacción se inició. Se anuló la transacción."  
  
 Este error destruye la transacción (incluso si XACT_ABORT está en OFF), lo que significa que la transacción se revertirá cuando la sesión de usuario finaliza. Las transacciones condenadas no se puede confirmar y solo admiten operaciones de lectura que no escriben en el registro y no tienen acceso a las tablas optimizadas para memoria.  
  
#####  <a name="cd"></a> Confirmar las dependencias  
 Durante el procesamiento normal, una transacción puede leer las filas escritas por otras transacciones que están en la fase de confirmación o validación, pero aún no se hayan confirmado. Las filas están visibles porque la hora de finalización lógica de las transacciones se ha asignado al inicio de la fase de validación.  
  
 Si una transacción lee estas filas no confirmadas, realizará una dependencia de confirmación en esa transacción. Esto tiene dos implicaciones principales:  
  
-   Una transacción no puede confirmarse hasta que las transacciones de las que depende se hayan confirmado. Es decir, no puede entrar en la fase de confirmación hasta que todas las dependencias se hayan borrado.  
  
-   Además, no se devuelven los conjuntos de resultados al cliente hasta que todas las dependencias se han borrado. Esto evita que el cliente observe datos los no confirmados.  
  
 Si alguna de las transacciones dependientes no se puede confirmar, hay un error de dependencia de confirmación. Esto significa que la transacción no podrá confirmarse con el error 41301 (“ Una transacción previa en la que la transacción actual tenía una dependencia ha sido anulada y la transacción actual ya no puede confirmarse").  
  
#### <a name="validation-phase"></a>Fase de validación  
 Durante la fase de validación, el sistema comprueba que las suposiciones necesarias para el nivel de aislamiento de transacción solicitado se ha cumplido entre el inicio lógico y la finalización lógica de la transacción.  
  
 Al comienzo de la fase de validación, a la transacción se le asigna una hora de finalización lógica. Las versiones de fila escritas en la base de datos se hacen visibles para otras transacciones en el momento de finalización lógica. Para obtener más información, vea [Confirmar las dependencias](#cd).  
  
##### <a name="repeatable-read-validation"></a>Validación de lectura repetible  
 Si el nivel de aislamiento de la transacción es REPEATABLE READ o SERIALIZABLE o bien, si se tiene acceso a las tablas con aislamiento REPEATABLE READ o SERIALIZABLE (para obtener más información, vea la sección sobre el aislamiento de operaciones individuales en [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md)), el sistema validará que las lecturas son repetibles. Esto significa que comprueba que las versiones de las filas leídas por la transacción son todavía versiones de fila válidas con la lógica y la hora de la transacción.  
  
 Si alguna de las filas se ha actualizado o se ha modificado, la transacción no puede confirmarse con el error 41305 (“La transacción actual no pudo confirmarse debido a un error de validación de lectura repetible").  
  
 Este error también puede producirse si se quita una tabla después de una operación de inserción, una actualización o una operación de eliminación y antes de que se confirme la transacción. Esto se aplica solo a las operaciones de inserción, actualización o eliminación en procedimientos almacenados compilados de forma nativa. Tales operaciones de escritura realizadas a través de [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado ocasionan que la instrucción DROP TABLE bloquee y espere hasta que la transacción se confirme.  
  
##### <a name="serializable-validation"></a>Validación serializable  
 La validación serializable se realiza en dos casos:  
  
-   Si el nivel de aislamiento de la transacción es SERIALIZABLE o se tiene acceso a las tablas con el aislamiento SERIALIZABLE.  
  
-   Si las filas se insertan en un índice único, como el índice creado para una restricción PRIMARY KEY. El sistema comprueba que no se han insertado simultáneamente filas con la misma clave.  
  
 El sistema comprueba que no se han escrito filas fantasma en la base de datos. Las operaciones de lectura realizadas por la transacción se evalúan para determinar que no se insertaron nuevas filas en los intervalos de recorrido de estas operaciones de lectura.  
  
 La inserción de una clave en un índice único incluye una operación de lectura implícita para determinar que la clave no es un duplicado. La validación serializable para índices únicos garantiza que estos índices no puedan tener duplicados en caso de que dos transacciones inserten simultáneamente la misma clave.  
  
 Si se detectan filas fantasma, la transacción no puede confirmarse con el error 41325 (“La transacción actual no pudo confirmarse debido a un error de validación serializable").  
  
#### <a name="commit-processing"></a>Procesamiento de la confirmación  
 Si la validación es correcta y todas las dependencias de la transacción se borran, la transacción entra en la fase de procesamiento de confirmación. Durante esta fase, los cambios en las tablas durables se escriben en el registro y el registro se escribe en el disco, para asegurar la durabilidad. Una vez que el registro de la transacción se ha escrito en el disco, el control se devuelve al cliente.  
  
 Se borran todas las dependencias confirmadas en esta transacción y todas las transacciones que habían estado esperando esta transacción para confirmarse pueden continuar.  
  
## <a name="limitations"></a>Limitaciones  
  
-   Las transacciones entre bases de datos no se admiten con tablas optimizadas para memoria. Cada transacción que tiene acceso a tablas optimizadas para memoria no puede tener acceso a más de una base de datos, excepto para el acceso de lectura y escritura a tempdb y el acceso de solo lectura a la base de datos maestra del sistema.  
  
-   Las transacciones distribuidas no se admiten con tablas optimizadas para memoria. Las transacciones distribuidas iniciadas con BEGIN DISTRIBUTED TRANSACTION no pueden tener acceso a las tablas optimizadas para memoria.  
  
-   Las tablas con optimización para memoria no admiten bloqueos. Los bloqueos explícitos con sugerencias de bloqueo (como TABLOCK, XLOCK, ROWLOCK) no se admiten con las tablas optimizadas para memoria.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de las transacciones en tablas optimizadas para memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
  
