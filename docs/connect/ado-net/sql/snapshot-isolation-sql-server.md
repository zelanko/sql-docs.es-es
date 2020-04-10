---
title: Aislamiento de instantáneas en SQL Server
description: Describe la compatibilidad con el aislamiento de instantánea, un mecanismo de control de versiones de fila diseñado para reducir el bloqueo en aplicaciones transaccionales.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 95f76cd9e4009292ec071a5faa2751b7afafc716
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920007"
---
# <a name="snapshot-isolation-in-sql-server"></a>Aislamiento de instantáneas en SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

El aislamiento de instantánea mejora la simultaneidad de las aplicaciones OLTP.  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>Descripción de las versiones de fila y el aislamiento de instantánea  
Una vez habilitado el aislamiento de instantánea, las versiones de fila actualizadas de cada transacción se mantienen en **tempdb**. Un número de secuencia de transacción único identifica cada transacción, y estos números únicos se registran para cada versión de fila. La transacción funciona con las versiones de fila más recientes que tienen un número de secuencia antes del número de secuencia de transacción. La transacción omite las versiones de fila más recientes creadas después de que se haya iniciado la transacción.  
  
El término "instantánea" refleja el hecho de que todas las consultas de la transacción ven la misma versión, o instantánea, de la base de datos, en función del estado de la base de datos en el momento en que se inicia la transacción. No se adquieren bloqueos en las filas de datos subyacentes ni en las páginas de datos de una transacción de instantánea, lo que permite que otras transacciones se ejecuten sin que una transacción sin completar anterior las bloquee. Las transacciones que modifican datos no bloquean las transacciones que leen datos, y las transacciones que leen datos no bloquean las transacciones que escriben datos, como ocurre normalmente en el nivel de aislamiento READ COMMITTED predeterminado de SQL Server. Este comportamiento de no bloqueo también reduce notablemente la probabilidad de que se produzcan interbloqueos en las transacciones complejas.  
  
El aislamiento de instantánea utiliza un modelo de simultaneidad optimista. Si una transacción de instantánea intenta confirmar modificaciones en los datos que han cambiado desde que se inició la transacción, esta se revertirá y se producirá un error. Puede evitarlo usando sugerencias UPDLOCK para las instrucciones SELECT que tienen acceso a los datos que se van a modificar. Visite el artículo "Sugerencias de bloqueo" de Libros en pantalla de SQL Server para obtener más información.  
  
El aislamiento de instantánea se debe habilitar estableciendo la opción ALLOW_SNAPSHOT_ISOLATION en ON en la base de datos antes de que se utilice en las transacciones. Con esto se activa el mecanismo para almacenar versiones de fila en la base de datos temporal (**tempdb**). Debe habilitar el aislamiento de instantánea en cada base de datos en que se utilice con la instrucción ALTER DATABASE de Transact-SQL. En este sentido, el aislamiento de instantánea difiere de los niveles de aislamiento tradicionales de READ COMMITTED, REPEATABLE READ, SERIALIZABLE y READ UNCOMMITTED, que no requieren ninguna configuración. Las siguientes instrucciones activan el aislamiento de instantánea y reemplazan el comportamiento READ COMMITTED predeterminado por SNAPSHOT:  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
Al establecer la opción READ_COMMITTED_SNAPSHOT ON, se permite el acceso a las filas con versión en el nivel de aislamiento READ COMMITTED predeterminado. Si la opción READ_COMMITTED_SNAPSHOT está establecida en OFF, debe establecer explícitamente el nivel de aislamiento de instantánea en cada sesión con el fin de acceder a las filas con versiones.  
  
## <a name="managing-concurrency-with-isolation-levels"></a>Administración de la simultaneidad con niveles de aislamiento  
El nivel de aislamiento en el que se ejecuta una instrucción Transact-SQL determina su bloqueo y el comportamiento de las versiones de fila. Un nivel de aislamiento tiene definido el ámbito en toda la conexión y, una vez que se establece en una conexión con la instrucción SET TRANSACTION ISOLATION LEVEL, continúa activo hasta que se cierra la conexión o se establece otro nivel de aislamiento. Cuando se cierra una conexión y se devuelve al grupo, se conserva el nivel de aislamiento de la última instrucción SET TRANSACTION ISOLATION LEVEL. Las conexiones posteriores que reutilizan una conexión agrupada usan el nivel de aislamiento que estaba activo en el momento en que se agrupó la conexión.  
  
Las consultas individuales emitidas en una conexión pueden contener sugerencias de bloqueo que modifiquen el aislamiento de una única instrucción o transacción, pero no afectan al nivel de aislamiento de la conexión. Los niveles de aislamiento o las sugerencias de bloqueo que se establecen en procedimientos almacenados o funciones no cambian el nivel de aislamiento de la conexión que los llama y solo están activos mientras dure el procedimiento almacenado o la llamada a la función.  
  
En las versiones anteriores de SQL Server se admitían cuatro niveles de aislamiento definidos en el estándar SQL-92:  
  
- READ UNCOMMITTED es el nivel de aislamiento menos restrictivo porque omite los bloqueos colocados por otras transacciones. Las transacciones que se ejecutan en READ UNCOMMITTED pueden leer valores de datos modificados que aún no han confirmado otras transacciones; estas se denominan lecturas de datos "sucios".  
  
- READ COMMITTED es el nivel de aislamiento predeterminado de SQL Server. Impide las lecturas de datos sucios especificando que las instrucciones no pueden leer valores de datos modificados, pero aún no confirmados por otras transacciones. Otras transacciones pueden seguir modificando, insertando o eliminando datos entre ejecuciones de instrucciones específicas dentro de la transacción actual, lo que da lugar a lecturas no repetibles o datos "fantasma".  
  
- REPEATABLE READ es un nivel de aislamiento más restrictivo que READ COMMITTED. Engloba READ COMMITTED y especifica, además, que ninguna otra transacción puede modificar o eliminar los datos leídos por la transacción actual hasta que esta se confirme. La simultaneidad es menor que en READ COMMITTED porque los bloqueos compartidos en los datos de lectura se mantienen mientras dure la transacción, en lugar de liberarse al final de cada instrucción.  
  
- SERIALIZABLE es el nivel de aislamiento más restrictivo, porque bloquea intervalos de claves completos y mantiene esos bloqueos hasta que la transacción finaliza. Engloba REPEATABLE READ y agrega la restricción de que otras transacciones no pueden insertar nuevas filas en intervalos leídos por la transacción hasta que se complete la transacción.  
  
Para obtener más información, vea la [Guía de versiones de fila y bloqueo de transacciones](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md).  
  
### <a name="snapshot-isolation-level-extensions"></a>Extensiones de nivel de aislamiento de instantánea  
SQL Server ha incorporado extensiones a los niveles de aislamiento SQL-92 con la presentación del nivel de aislamiento SNAPSHOT y una implementación adicional de READ COMMITTED. El nivel de aislamiento READ_COMMITTED_SNAPSHOT puede sustituir de forma transparente a READ COMMITTED en todas las transacciones.  
  
- El aislamiento SNAPSHOT especifica que los datos leídos en una transacción nunca reflejarán los cambios realizados por otras transacciones simultáneas. La transacción utiliza las versiones de fila de datos que existen cuando se inicia la transacción. No se aplican bloqueos a los datos cuando se leen, por lo que las transacciones SNAPSHOT no impiden que otras transacciones escriban datos. Las transacciones que escriben datos no bloquean la lectura de datos de las transacciones de tipo SNAPSHOT. Debe habilitar el aislamiento de instantánea estableciendo la opción de base de datos ALLOW_SNAPSHOT_ISOLATION para poder usarlo.  
  
- La opción de base de datos READ_COMMITTED_SNAPSHOT determina el comportamiento del nivel de aislamiento READ COMMITTED predeterminado cuando el aislamiento de instantánea está habilitado en una base de datos. Si no especifica explícitamente READ_COMMITTED_SNAPSHOT en ON, READ COMMITTED se aplica a todas las transacciones implícitas. Esto produce el mismo comportamiento que si se establece READ_COMMITTED_SNAPSHOT en OFF (el valor predeterminado). Cuando READ_COMMITTED_SNAPSHOT OFF está en vigor, el Motor de base de datos utiliza bloqueos compartidos para aplicar el nivel de aislamiento predeterminado. Si establece la opción de base de datos READ_COMMITTED_SNAPSHOT en ON, el Motor de base de datos utilizará las versiones de fila y el aislamiento de instantánea de forma predeterminada, en lugar de usar bloqueos para proteger los datos.  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>Funcionamiento del aislamiento de instantánea y las versiones de fila  
Cuando se habilita el nivel de aislamiento SNAPSHOT, cada vez que se actualiza una fila, el motor de base de datos de SQL Server almacena una copia de la fila original en **tempdb** y agrega un número de secuencia de transacción a la fila. A continuación se presenta la secuencia de eventos que se produce:  
  
1. Se inicia una nueva transacción y se le asigna un número de secuencia de transacción.  
  
2. El motor de base de datos lee una fila de la transacción y recupera la versión de fila de **tempdb** cuyo número de secuencia se aproxima más a, y es inferior a, el número de la secuencia de transacción.  
  
3. El Motor de base de datos comprueba si el número de secuencia de transacción no está en la lista de números de secuencia de transacción de las transacciones no confirmadas activas cuando se inició la transacción de instantánea.  
  
4. La transacción lee la versión de la fila de **tempdb** que era la actual al inicio de la transacción. Esta no verá las nuevas filas insertadas una vez iniciada la transacción porque esos valores de número de secuencia serán mayores que el valor del número de secuencia de transacción.  
  
5. La transacción actual ve las filas que se han eliminado tras su inicio, porque hay una versión de fila en **tempdb** con un valor de número de secuencia inferior.  
  
El efecto real del aislamiento de instantánea es que la transacción ve todos los datos tal como se encontraban en el inicio de la transacción, sin tener en cuenta ni colocar los bloqueos en las tablas subyacentes. Esta acción mejorar el rendimiento en situaciones en las que hay contención.  
  
Una transacción de instantánea siempre utiliza el control de simultaneidad optimista, que retiene los bloqueos que impiden que otras transacciones actualicen las filas. Si una transacción de instantánea intenta confirmar una actualización en una fila que se cambió una vez iniciada la transacción, la transacción se revierte y se produce un error.  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>Uso del aislamiento de instantánea en ADO.NET  
La clase <xref:Microsoft.Data.SqlClient.SqlTransaction> admite el aislamiento de instantánea en ADO.NET. Si se ha habilitado en una base de datos el aislamiento de instantánea pero no se ha configurado como READ_COMMITTED_SNAPSHOT ON, debe iniciar una <xref:Microsoft.Data.SqlClient.SqlTransaction> mediante el valor de enumeración **IsolationLevel.Snapshot** cuando llame al método <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A>. En este fragmento de código se da por hecho que la conexión es un objeto <xref:Microsoft.Data.SqlClient.SqlConnection> abierto.  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra cómo se comportan los distintos niveles de aislamiento intentando acceder a los datos bloqueados; no está diseñado para usarse en el código de producción.  
  
El código conecta a la base de datos de ejemplo **AdventureWorks** de SQL Server, crea una tabla denominada **TestSnapshot** e inserta una fila de datos. El código usa la instrucción ALTER DATABASE de Transact-SQL para activar el aislamiento de instantánea en la base de datos, pero no establece la opción READ_COMMITTED_SNAPSHOT, lo que deja activo el comportamiento del nivel de aislamiento READ COMMITTED predeterminado. El código realiza las siguientes acciones:  
  
1. Inicia sqlTransaction1 sin completarla, que usa el nivel de aislamiento SERIALIZABLE para iniciar una transacción de actualización. Con esto, se bloquea la tabla.  
  
2. Se abre una segunda conexión y se inicia una segunda transacción con el nivel de aislamiento SNAPSHOT para leer los datos de la tabla **TestSnapshot**. Dado que el aislamiento de instantánea está habilitado, esta transacción puede leer los datos que existían antes de que se iniciara sqlTransaction1.  
  
3. Se abre una tercera conexión y se inicia una transacción con el nivel de aislamiento READ COMMITTED para intentar leer los datos de la tabla. En este caso, el código no puede leer los datos porque no puede leer con posterioridad a los bloqueos realizados en la tabla en la primera transacción y el tiempo de espera se agota. Se produciría el mismo resultado si se usaran los niveles de aislamiento REPEATABLE READ y SERIALIZABLE, ya que estos niveles de aislamiento tampoco pueden leer después de los bloqueos realizados en la primera transacción.  
  
4. Se abre una cuarta conexión y se inicia una transacción con el nivel de aislamiento READ UNCOMMITTED, que realiza una lectura de datos sucios del valor sin confirmar en sqlTransaction1. Este valor nunca puede existir realmente en la base de datos si la primera transacción no se confirma.  
  
5. Se revierte la primera transacción y se procede a una limpieza con la eliminación de la tabla **TestSnapshot** y la desactivación del aislamiento de instantánea en la base de datos **AdventureWorks**.  
  
> [!NOTE]
>  En los ejemplos siguientes se usa la misma cadena de conexión con la agrupación de conexiones desactivada. Si una conexión se agrupa, al restablecer su nivel de aislamiento no se restablece el nivel de aislamiento en el servidor. Como resultado, las conexiones posteriores que usan la misma conexión interna agrupada se inician con sus niveles de aislamiento establecidos en el de la conexión agrupada. Una alternativa a desactivar la agrupación de conexiones es establecer el nivel de aislamiento explícitamente en cada conexión.  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>Ejemplo  
En el ejemplo siguiente se muestra el comportamiento del aislamiento de instantánea cuando se modifican los datos. El código realiza las siguientes acciones:  
  
1. Conecta a la base de datos de ejemplo **AdventureWorks** y habilita el aislamiento SNAPSHOT.  
  
2. Crea una tabla denominada **TestSnapshotUpdate** e inserta tres filas de datos de ejemplo.  
  
3. Inicia sqlTransaction1 sin completarla, mediante el aislamiento SNAPSHOT. En la transacción se seleccionan tres filas de datos.  
  
4. Crea una segunda **SqlConnection** a **AdventureWorks** y crea una segunda transacción con el nivel de aislamiento READ COMMITTED que actualiza un valor de una de las filas seleccionadas en sqlTransaction1.  
  
5. Confirma sqlTransaction2.  
  
6. Vuelve a sqlTransaction1 e intenta actualizar la misma fila que sqlTransaction1 ya confirmó. Se produce el error 3960 y sqlTransaction1 se revierte automáticamente. **SqlException.Number** y **SqlException.Message** se muestran en la ventana Consola.  
  
7. Ejecuta el código de limpieza para desactivar el aislamiento de instantánea en **AdventureWorks** y eliminar la tabla **TestSnapshotUpdate**.  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>Uso de sugerencias de bloqueo con aislamiento de instantánea  
En el ejemplo anterior, la primera transacción selecciona los datos, y una segunda transacción actualiza los datos antes de que se pueda completar la primera, lo que provoca un conflicto de actualización cuando la primera transacción intenta actualizar la misma fila. Puede reducir la posibilidad de conflictos de actualización en transacciones de instantánea de ejecución prolongada proporcionando sugerencias de bloqueo al inicio de la transacción. La siguiente instrucción SELECT usa la sugerencia UPDLOCK para bloquear las filas seleccionadas:  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
Al usar la sugerencia de bloqueo UPDLOCK, se bloquean las filas que intentan actualizar las filas antes de que se complete la primera transacción. Esto garantiza que las filas seleccionadas no tengan conflictos cuando se actualicen posteriormente en la transacción. Consulte el artículo "Sugerencias de bloqueo" en Libros en pantalla de SQL Server.  
  
Si la aplicación tiene muchos conflictos, es posible que el aislamiento de instantánea no sea la mejor opción. Las sugerencias solo deben usarse cuando realmente se necesite. La aplicación no debe estar diseñada para que funcionen dependiendo constantemente de las sugerencias de bloqueo.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
- [Guía de versiones de fila y bloqueo de transacciones](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
