---
title: Sugerencias (Transact-SQL) de tabla | Documentos de Microsoft
ms.custom: 
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TABLE_HINT_TSQL
- Table Hint
dev_langs: TSQL
helpviewer_keywords:
- SERIALIZABLE table hint
- UPDLOCK table hint
- HOLDLOCK table hint
- TABLOCKX table hint
- READUNCOMMITTED table hint
- hints [SQL Server], tables
- READCOMMITTEDLOCK table hint
- FORCESCAN table hint
- ROWLOCK table hint
- XLOCK table hint
- NOLOCK table hint
- READPAST table hint
- NOWAIT table hint
- FORCESEEK table hint
- table hints [SQL Server]
- TABLOCK table hint
- REPEATABLEREAD table hint
- READ COMMITTED table hint
- NOEXPAND table hint
- PAGLOCK table hint
ms.assetid: 8bf1316f-c0ef-49d0-90a7-3946bc8e7a89
caps.latest.revision: "174"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 92740f196f2bd0c79a84eb43826f764e93930e67
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="hints-transact-sql---table"></a>Sugerencias (Transact-SQL) - tabla
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Las sugerencias de tabla invalidan el comportamiento predeterminado del optimizador de consultas mientras dura la instrucción del lenguaje de manipulación de datos (DML) especificando un método de bloqueo, uno o varios índices, una operación de procesamiento de la consulta como un recorrido de tabla o una búsqueda de índice, u otras opciones. Las sugerencias de tabla se especifican en la cláusula FROM de la instrucción DML y solo afectan a la tabla o a la vista a la que se hace referencia en esa cláusula.  
  
> [!CAUTION]  
>  Como el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele seleccionar el mejor plan de ejecución de una consulta, se recomienda que únicamente los administradores de bases de datos y desarrolladores experimentados utilicen las sugerencias como último recurso.  
  
 **Se aplica a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WITH  ( <table_hint> [ [, ]...n ] )  
  
<table_hint> ::=   
[ NOEXPAND ] {   
    INDEX  ( index_value [ ,...n ] )   
  | INDEX =  ( index_value )      
  | FORCESEEK [( index_value ( index_column_name  [ ,... ] ) ) ]  
  | FORCESCAN  
  | FORCESEEK  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
  
<table_hint_limited> ::=  
{  
    KEEPIDENTITY   
  | KEEPDEFAULTS   
  | HOLDLOCK   
  | IGNORE_CONSTRAINTS   
  | IGNORE_TRIGGERS   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
```  
  
## <a name="arguments"></a>Argumentos  
 CON **(** \<sugerenciatabla > **)** [[**,** ]... *n* ]  
 Con algunas excepciones, las sugerencias de tabla se admiten en la cláusula FROM únicamente cuando las sugerencias se especifican con la palabra clave WITH. Las sugerencias de tabla deben especificarse también con paréntesis.  
  
> [!IMPORTANT]  
>  Omitir la palabra clave WITH es una característica obsoleta: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Las sugerencias de tabla permitidas con y sin la palabra clave WITH son las siguientes: NOLOCK, READUNCOMMITTED, UPDLOCK, REPEATABLEREAD, SERIALIZABLE, READCOMMITTED, FASTFIRSTROW, TABLOCK, TABLOCKX, PAGLOCK, ROWLOCK, NOWAIT, READPAST, XLOCK, SNAPSHOT y NOEXPAND. Cuando estas sugerencias de tabla se especifican sin la palabra clave WITH, deben especificarse solas. Por ejemplo:  
  
```  
FROM t (TABLOCK)  
```  
  
 Cuando la sugerencia se especifica con otra opción, debe especificarse con la palabra clave WITH:  
  
```  
FROM t WITH (TABLOCK, INDEX(myindex))  
```  
  
 Recomendamos utilizar comas entre las sugerencias de tabla.  
  
> [!IMPORTANT]  
>  La separación de las sugerencias con espacios en lugar de comas es una característica obsoleta: [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 NOEXPAND  
 Especifica que las vistas indizadas no se expandan para obtener acceso a las tablas subyacentes cuando el optimizador de consultas procesa la consulta. El optimizador de consultas trata la vista como una tabla con un índice clúster. NOEXPAND solo se aplica a las vistas indizadas. Para obtener más información, vea la sección Comentarios.  
  
 ÍNDICE **(***index_value* [**,**... *n* ] ) | ÍNDICE = ( *index_value***)**  
 La sintaxis de INDEX() especifica los nombres o los identificadores de los índices que el optimizador de consultas va a utilizar al procesar la instrucción. La sintaxis alternativa INDEX = especifica un valor de índice único. Solamente se puede especificar una sugerencia de índice por cada tabla.  
  
 Si existe un índice agrupado, INDEX(0) exige un recorrido del índice agrupado e INDEX(1) exige un recorrido o una búsqueda del índice agrupado. Si no existe un índice clúster, INDEX(0) exige un recorrido de tabla e INDEX(1) se interpreta como error.  
  
 Si se utilizan varios índices en una lista de sugerencias, los índices duplicados se omiten y el resto se utiliza para recuperar las filas de la tabla. El orden de los índices de la sugerencia de índice es importante. Una sugerencia de varios índices obliga a hacer AND entre los índices y el optimizador de consultas aplica todas las condiciones posibles a cada uno de los índices a los que tiene acceso. Si la colección de índices sugeridos no incluye todas las columnas a las que hace referencia la consulta, se realiza una captura para recuperar las columnas restantes, una vez que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] recupera todas las columnas indizadas.  
  
> [!NOTE]  
>  Cuando se utiliza una sugerencia de índice que hace referencia a varios índices en la tabla de hechos de una combinación en estrella, el optimizador pasa por alto la sugerencia de índice y devuelve un mensaje de advertencia. Asimismo, no se admiten las operaciones OR de índices para una tabla con una sugerencia de índice especificada.  
  
 El número máximo de índices de una sugerencia de tabla es 250 índices no clúster.  
  
 KEEPIDENTITY  
 Es aplicable únicamente en una instrucción INSERT cuando se usa la opción BULK con [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
 Especifica que se usará el valor o valores de identidad del archivo de datos importado para la columna de identidad. Si no se especifica KEEPIDENTITY, los valores de identidad de esta columna se comprueban pero no se importan, y el optimizador de consultas asigna automáticamente valores únicos basados en los valores de inicialización y de incremento especificados durante la creación de la tabla.  
  
> [!IMPORTANT]  
>  Si el archivo de datos no contiene valores para la columna de identidad de la tabla o vista, y la columna de identidad no es la última columna de la tabla, entonces deberá omitir la columna de identidad. Para obtener más información, vea [usar un archivo de formato para omitir un campo de datos &#40; SQL Server &#41; ](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md). Si una columna de identidad se omite correctamente, el optimizador de consultas asigna automáticamente valores únicos para la columna de identidad en las filas de la tabla importada.  
  
 Para obtener un ejemplo que utiliza esta sugerencia en una instrucción INSERT... Seleccione * FROM OPENROWSET BULK, vea [mantener identidad valores importaciones masivas de datos &#40; SQL Server &#41; ](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 Para obtener información acerca de cómo comprobar el valor de identidad para una tabla, vea [DBCC CHECKIDENT &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 KEEPDEFAULTS  
 Es aplicable únicamente en una instrucción INSERT cuando se usa la opción BULK con [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
 Especifica la inserción del valor predeterminado de la columna de una tabla, si existe, en lugar de NULL, cuando falta el valor del registro de datos de esa columna.  
  
 Para obtener un ejemplo que utiliza esta sugerencia en una instrucción INSERT... Seleccione * FROM OPENROWSET BULK, vea [mantener valores NULL o usar predeterminado valores durante la importación en bloque &#40; SQL Server &#41; ](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 FORCESEEK [ **(***index_value***(***index_column_name* [ **,**... *n* ] **))** ]  
 Especifica que el optimizador de consultas use solamente una operación de búsqueda de índice como ruta de acceso a los datos de la tabla o la vista. A partir de SQL Server 2008 R2 SP1, también se pueden especificar parámetros de índice. En ese caso, el optimizador de consultas solo considera las operaciones de búsqueda de índice mediante el índice especificado usando al menos las columnas de índice especificadas.  
  
 *index_value*  
 Es el nombre o el valor de identificador del índice. No se puede especificar el identificador de índice 0 (montón). Para devolver el nombre de índice o el identificador, consulte el **sys.indexes** vista de catálogo.  
  
 *index_column_name*  
 Es el nombre de la columna de índice que se va a incluir en la operación de búsqueda. Especificar FORCESEEK con parámetros de índice es similar a usar FORCESEEK con una sugerencia INDEX. Sin embargo, puede lograr mayor control sobre la ruta de acceso empleada por el optimizador de consultas si se especifican tanto el índice que se va a buscar como las columnas de índice que hay que tener en cuenta en la operación de búsqueda. El optimizador también puede considerar columnas adicionales si es necesario. Por ejemplo, si se especifica un índice no clúster, el optimizador puede elegir el uso de columnas de clave de índice clúster además de las columnas especificadas.  
  
 La sugerencia FORCESEEK se puede especificar de las maneras siguientes.  
  
|Sintaxis|Ejemplo|Description|  
|------------|-------------|-----------------|  
|Sin un índice o sugerencia INDEX|`FROM dbo.MyTable WITH (FORCESEEK)`|El optimizador de consultas sólo considera las operaciones de búsqueda de índice para tener acceso a la tabla o la vista mediante cualquier índice pertinente.|  
|Combinado con una sugerencia INDEX|`FROM dbo.MyTable WITH (FORCESEEK, INDEX (MyIndex))`|El optimizador de consultas solo considera las operaciones de búsqueda de índice para tener acceso a la tabla o la vista mediante el índice especificado.|  
|Parametrizado especificando un índice y columnas de índice|`FROM dbo.MyTable WITH (FORCESEEK (MyIndex (col1, col2, col3)))`|El optimizador de consultas solo considera las operaciones de búsqueda de índice para tener acceso a la tabla o la vista mediante el índice especificado usando al menos las columnas de índice especificadas.|  
  
 Cuando se usa la sugerencia FORCESEEK (con o sin parámetros de índice), tenga en cuenta las directrices siguientes.  
  
-   La sugerencia se puede especificar como sugerencia de tabla o como sugerencia de consulta. Para obtener más información acerca de las sugerencias de consulta, vea [sugerencias de consulta &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   Para aplicar FORCESEEK a una vista indizada, se debe especificar también la sugerencia NOEXPAND.  
  
-   La sugerencia se puede aplicar una vez por tabla o vista como máximo.  
  
-   No se puede especificar la sugerencia para un origen de datos remoto. Se devuelve el error 7377 cuando se especifica FORCESEEK con una sugerencia de índice y el error 8180 cuando se usa FORCESEEK sin una sugerencia de índice.  
  
-   Si FORCESEEK hace que no se encuentre ningún plan, se devuelve el error 8622.  
  
 Cuando FORCESEEK se especifica con parámetros de índice, se aplican las siguientes directrices y restricciones.  
  
-   La sugerencia no se puede especificar para una tabla que es el destino de una instrucción INSERT, UPDATE o DELETE.  
  
-   La sugerencia no se puede especificar junto con una sugerencia INDEX o con otra sugerencia FORCESEEK.  
  
-   Se debe especificar al menos una columna y debe ser la columna de clave inicial.  
  
-   Se pueden especificar columnas de índice adicionales, aunque no se pueden omitir columnas de clave. Por ejemplo, si el índice especificado contiene las columnas de clave `a`, `b` y `c`, `FORCESEEK (MyIndex (a))` y `FORCESEEK (MyIndex (a, b)` serían sintaxis válidas. También serían sintaxis válidas `FORCESEEK (MyIndex (c))` y `FORCESEEK (MyIndex (a, c)`.  
  
-   El orden de los nombres de columna especificados en la sugerencia debe coincidir con el orden de las columnas en el índice al que se hace referencia.  
  
-   No se pueden especificar columnas que no estén en la definición de clave de índice. Por ejemplo, en un índice no clúster solo se pueden especificar las columnas de clave de índice definidas. No se pueden especificar columnas de clave clúster que se incluyen automáticamente en el índice, aunque el optimizador puede usarlas.  
  
-   Un índice de almacén de columnas con optimización para memoria xVelocity no se puede especificar como parámetro de índice. Se devuelve el error 366.  
  
-   La modificación de la definición de índice (por ejemplo, agregando o quitando columnas) puede hacer que sea necesario modificar las consultas que hacen referencia a dicho índice.  
  
-   La sugerencia impide que el optimizador considere ningún índice espacial o XML de la tabla.  
  
-   La sugerencia no se puede especificar junto con la sugerencia FORCESCAN.  
  
-   En el caso de índices con particiones, la columna de partición agregada implícitamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede especificar en la sugerencia FORCESEEK.  
  
> [!CAUTION]  
>  Al especificar FORCESEEK con parámetros se limita el número de planes que el optimizador puede considerar en comparación con cuando se especifica FORCESEEK sin parámetros. Esto puede producir un error "No se puede generar el plan" en más casos. En una versión futura, las modificaciones internas realizadas en el optimizador pueden permitir que se consideren más planes.  
  
 FORCESCAN  
 Esta sugerencia, presentada en SQL Server 2008 R2 SP1, especifica que el optimizador de consultas solo usa una operación de examen de índice como ruta de acceso a la tabla o la vista a la que se hace referencia. La sugerencia FORCESCAN puede ser útil para consultas en las que el optimizador subestima el número de filas afectadas y elige una operación de búsqueda en lugar de una operación de examen. Cuando esto ocurre, la cantidad de memoria asignada a la operación es demasiado pequeña y el rendimiento de la consulta se ve afectado.  
  
 FORCESCAN se puede especificar con o sin una sugerencia INDEX. Cuando se combina con una sugerencia de índice, (`INDEX = index_name, FORCESCAN`), el optimizador de consultas solo considera el examen de rutas de acceso mediante el índice especificado al tener acceso a la tabla a la que se hace referencia. Se puede especificar FORCESCAN con la sugerencia de índice INDEX(0) para forzar una operación de recorrido de tabla en la tabla base.  
  
 En las tablas y los índices con particiones, FORCESCAN se aplica una vez eliminadas las particiones mediante la evaluación de predicados de las consultas. Esto significa que el recorrido se aplica únicamente a las particiones restantes, no a toda la tabla.  
  
 La sugerencia FORCESCAN tiene las restricciones siguientes.  
  
-   La sugerencia no se puede especificar para una tabla que es el destino de una instrucción INSERT, UPDATE o DELETE.  
  
-   La sugerencia no se puede emplear con más de una sugerencia de índice.  
  
-   La sugerencia impide que el optimizador considere ningún índice espacial o XML de la tabla.  
  
-   No se puede especificar la sugerencia para un origen de datos remoto.  
  
-   La sugerencia no se puede especificar junto con la sugerencia FORCESEEK.  
  
 HOLDLOCK  
 Equivalente a SERIALIZABLE. Para obtener más información, vea SERIALIZABLE más adelante en este tema. HOLDLOCK solo se aplica a la tabla o la vista para la que se especificó, y únicamente durante la transacción definida por la instrucción en la que se usa. HOLDLOCK no se puede usar en una instrucción SELECT que incluya la opción FOR BROWSE.  
  
 IGNORE_CONSTRAINTS  
 Es aplicable únicamente en una instrucción INSERT cuando se usa la opción BULK con [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
 Especifica que la operación de importación masiva ignora las restricciones de la tabla. De forma predeterminada, inserte comprobaciones [restricciones Unique y restricciones Check](../../relational-databases/tables/unique-constraints-and-check-constraints.md) y [principal y las restricciones de clave externa](../../relational-databases/tables/primary-and-foreign-key-constraints.md). Cuando IGNORE_CONSTRAINTS se especifica para una operación de importación masiva, INSERT debe ignorar estas restricciones en una tabla de destino. Tenga en cuenta que no puede deshabilitar las restricciones UNIQUE, PRIMARY KEY o NOT NULL.  
  
 Puede ser conveniente deshabilitar las instrucciones CHECK y FOREING KEY si los datos de entrada contienen filas que infringen las restricciones. Si se deshabilitan las restricciones CHECK y FOREIGN KEY, se pueden importar los datos y, a continuación, utilizar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para limpiarlos.  
  
 Sin embargo, si se omiten las restricciones CHECK y FOREIGN KEY, cada restricciones omitidas de la tabla se marcan como **is_not_trusted** en el [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) o [sys.foreign_keys ](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) vista de catálogo después de la operación. En algún momento, deberá comprobar las restricciones en la tabla completa. Si la tabla no estaba vacía antes de la operación de importación masiva, el costo de volver a validar la restricción puede ser mayor que el costo de aplicar las restricciones CHECK o FOREIGN KEY a los datos incrementales.  
  
 IGNORE_TRIGGERS  
 Es aplicable únicamente en una instrucción INSERT cuando se usa la opción BULK con [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
 Especifica que la operación de importación masiva ignore todos los desencadenadores definidos en la tabla. De manera predeterminada, INSERT aplica desencadenadores.  
  
 Use IGNORE_TRIGGERS únicamente si su aplicación no depende de ningún desencadenador y es importante maximizar el rendimiento.  
  
 NOLOCK  
 Equivalente a READUNCOMMITTED. Para obtener más información, vea READUNCOMMITTED más adelante en este mismo tema.  
  
> [!NOTE]  
>  Para las instrucciones UPDATE o DELETE: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 NOWAIT  
 Indica a [!INCLUDE[ssDE](../../includes/ssde-md.md)] que devuelva un mensaje cuando encuentre un bloqueo en la tabla. NOWAIT equivale a especificar SET LOCK_TIMEOUT 0 para una tabla específica. La sugerencia NOWAIT no funciona cuando también se incluye la sugerencia TABLOCK. Para terminar una consulta sin esperas cuando se usa la sugerencia TABLOCK, preceda el nombre de la consulta con `SETLOCK_TIMEOUT 0;` en su lugar.  
  
 PAGLOCK  
 Aplica bloqueos de página en los casos en que se suelen aplicar bloqueos individuales en filas o claves, o bien en los casos en los que se suele aplicar un único bloqueo de tabla. De manera predeterminada, utiliza el modo de bloqueo apropiado para la operación. Cuando se especifica en transacciones que funcionan con el nivel de aislamiento SNAPSHOT, no se utilizan bloqueos de página a menos que se combine PAGLOCK con otras sugerencias de tabla que requieran bloqueos, como UPDLOCK y HOLDLOCK.  
  
 READCOMMITTED  
 Especifica que las operaciones de lectura cumplan las reglas del nivel de aislamiento READ COMMITTED, a través del uso de bloqueos o control de versiones de filas. Si la opción de la base de datos READ_COMMITTED_SNAPSHOT está establecida en OFF, [!INCLUDE[ssDE](../../includes/ssde-md.md)] adquiere bloqueos compartidos a medida que se leen los datos y los libera cuando finaliza la operación de lectura. Si la opción de base de datos READ_COMMITTED_SNAPSHOT está establecida en ON, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no adquiere bloqueos y utiliza el control de versiones de filas. Para obtener más información acerca de los niveles de aislamiento, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
>  Para las instrucciones UPDATE o DELETE: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 READCOMMITTEDLOCK  
 Especifica que las operaciones de lectura cumplan, mediante el uso de bloqueos, las reglas del nivel de aislamiento READ COMMITTED. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] adquiere bloqueos compartidos a medida que se leen los datos y los libera cuando se completa la operación de lectura, independientemente de la configuración de la opción de base de datos READ_COMMITTED_SNAPSHOT. Para obtener más información acerca de los niveles de aislamiento, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Esta sugerencia no se puede especificar en la tabla de destino de una instrucción INSERT; de lo contrario, se devuelve el error 4140.  
  
 READPAST  
 Especifica que [!INCLUDE[ssDE](../../includes/ssde-md.md)] no lea las filas bloqueadas por otras transacciones. Cuando se especifica READPAST, se omiten los bloqueos de nivel de fila pero no se omiten los bloqueos de nivel de página. Es decir, [!INCLUDE[ssDE](../../includes/ssde-md.md)] omite las filas en lugar de bloquear la transacción actual hasta que se liberen los bloqueos. Suponga, por ejemplo, una tabla `T1` que contiene una única columna de tipo entero con los valores 1, 2, 3, 4, 5. Si una transacción A cambia el valor de 3 a 8 pero aún no se ha confirmado, una instrucción SELECT * FROM T1 (READPAST) generará los valores 1, 2, 4, 5. READPAST se utiliza principalmente para reducir la contención de bloqueo al implementar una cola de trabajo que usa un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. Un lector de cola que utilice READPAST omite las entradas de cola bloqueadas por otras transacciones y pasa a la siguiente entrada de cola disponible, sin tener que esperar a que las otras transacciones liberen los bloqueos.  
  
 READPAST se puede especificar para cualquier tabla a la que se haga referencia en una instrucción UPDATE o DELETE, o en una cláusula FROM. Cuando se especifica en una instrucción UPDATE, READPAST solamente se aplica al leer los datos para identificar los registros que se van a actualizar, independientemente de dónde se especifique en la instrucción. No se puede especificar READPAST para tablas en la cláusula INTO de una instrucción INSERT. Las operaciones de actualización o eliminación que utilizan READPAST se pueden bloquear al leer claves externas o vistas indizadas, o al modificar índices secundarios.  
  
 READPAST solamente se puede especificar en transacciones que funcionen con niveles de aislamiento READ COMMITTED o REPEATABLE READ. Cuando se especifica en transacciones que funcionan con el nivel de aislamiento SNAPSHOT, READPAST debe combinarse con otras sugerencias de tabla que requieran bloqueos, como UPDLOCK y HOLDLOCK.  
  
 No se puede especificar la sugerencia de tabla READPAST cuando la opción de base de datos READ_COMMITTED_SNAPSHOT esté establecida en ON y se cumpla alguna de las condiciones siguientes.  
  
-   El nivel de aislamiento de transacción de la sesión es READ COMMITTED.  
  
-   La sugerencia de tabla READCOMMITTED también se especifica en la consulta.  
  
 Para especificar la sugerencia READPAST en estos casos, quite la sugerencia de tabla READCOMMITTED, si está presente, e incluya la sugerencia de tabla READCOMMITTEDLOCK en la consulta.  
  
 READUNCOMMITTED  
 Especifica que se admiten lecturas no actualizadas. No se emiten bloqueos compartidos para impedir que otras transacciones modifiquen los datos leídos por la transacción actual, mientras que los bloqueos exclusivos establecidos por otras transacciones no impiden que la transacción actual lea los datos bloqueados. La posibilidad de efectuar lecturas no actualizadas aumenta en gran medida la simultaneidad, pero a costa de leer modificaciones de datos que otras transacciones revierten más adelante. Esto puede generar errores en la transacción, presentar a los usuarios datos no confirmados o hacer que los usuarios vean los registros dos veces (o nunca).  
  
 Las sugerencias READUNCOMMITTED y NOLOCK solamente se aplican a bloqueos de datos. Todas las consultas, incluidas las que tienen sugerencias READUNCOMMITTED y NOLOCK, adquieren bloqueos Sch-S (estabilidad del esquema) durante la compilación y la ejecución. Debido a ello, las consultas se bloquean cuando una transacción simultánea aloja un bloqueo de modificación del esquema (Sch-M) en la tabla. Por ejemplo, una operación de lenguaje de definición de datos (DDL) adquiere un bloqueo Sch-M antes de modificar la información del esquema de la tabla. Las consultas simultáneas, incluidas las que se ejecutan con sugerencias READUNCOMMITTED o NOLOCK, se bloquean cuando intentan adquirir un bloqueo Sch-S. A la inversa, una consulta que mantiene un bloqueo Sch-S bloquea una transacción simultánea que intenta adquirir un bloqueo Sch-M.  
  
 No se pueden especificar READUNCOMMITTED ni NOLOCK en tablas modificadas por operaciones de inserción, actualización y eliminación. El optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] omite las sugerencias READUNCOMMITTED y NOLOCK de la cláusula FROM que se aplica a la tabla de destino de una instrucción UPDATE o DELETE.  
  
> [!NOTE]  
>  En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quitará el uso de las sugerencias READUNCOMMITTED y NOLOCK en la cláusula FROM que se aplican a la tabla de destino de una instrucción UPDATE o DELETE. Evite usar estas sugerencias en este contexto en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que las usan actualmente.  
  
 Si lo desea, también puede reducir al mínimo el conflicto de bloqueos mientras protege las transacciones de lecturas de datos no actualizados de modificaciones de datos no confirmadas mediante una de estas dos alternativas:  
  
-   El nivel de aislamiento READ COMMITTED con la opción de base de datos READ_COMMITTED_SNAPSHOT establecida en ON.  
  
-   El nivel de aislamiento SNAPSHOT.  
  
 Para obtener más información acerca de los niveles de aislamiento, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
>  Si al especificar READUNCOMMITTED, recibe el mensaje de error 601, resuélvalo como si fueran errores de interbloqueo (1205) y vuelva a ejecutar la instrucción.  
  
 REPEATABLEREAD  
 Especifica que el recorrido se haga con la misma semántica de bloqueo que una transacción que se ejecute con el nivel de aislamiento REPEATABLE READ. Para obtener más información acerca de los niveles de aislamiento, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 ROWLOCK  
 Especifica que se apliquen bloqueos de fila cuando normalmente se aplicarían bloqueos de página o de tabla. Cuando se especifica en transacciones que funcionan con el nivel de aislamiento SNAPSHOT, no se utilizan bloqueos de fila a menos que se combine ROWLOCK con otras sugerencias de tabla que requieran bloqueos, como UPDLOCK y HOLDLOCK.  
  
 SERIALIZABLE  
 Equivalente a HOLDLOCK. Hace que los bloqueos compartidos sean más restrictivos, manteniéndolos hasta la finalización de la transacción, en lugar de liberarlos cuando la tabla o página de datos deja de ser necesaria, se haya completado la transacción o no. El recorrido se hace con la misma semántica que una transacción que se ejecuta con el nivel de aislamiento SERIALIZABLE. Para obtener más información acerca de los niveles de aislamiento, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 SNAPSHOT  
**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Se tiene acceso a la tabla optimizada para memoria con aislamiento SNAPSHOT. SNAPSHOT solo se puede utilizar con tablas optimizadas para memoria (no con tablas basadas en disco). Para obtener más información, consulte [Introducción a las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
```  
SELECT * FROM dbo.Customers AS c   
WITH (SNAPSHOT)   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id=oh.customer_id;  
```  
  
 SPATIAL_WINDOW_MAX_CELLS = *entero*  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número máximo de celdas que se van a usar para teselar un objeto de geometría o geografía. *número* es un valor entre 1 y 8192.  
  
 Esta opción permite optimizar el tiempo de ejecución de la consulta ajustando el equilibrio entre el tiempo de ejecución del filtro primario y secundario. Un número mayor reduce el tiempo de ejecución del filtro secundario, pero aumenta el tiempo de ejecución del filtro primario y un número menor disminuye el tiempo de ejecución del filtro primario, pero aumenta el tiempo de ejecución del filtro secundario. En el caso de datos espaciales más densos, un número mayor debe producir un tiempo de ejecución más rápido proporcionando una mejor aproximación con el filtro primario y reduciendo el tiempo de ejecución del filtro secundario. Si se trata de datos más dispersos, un número menor disminuirá el tiempo de ejecución del filtro primario.  
  
 Esta opción funciona para las teselaciones de cuadrícula manuales y automáticas.  
  
 TABLOCK  
 Especifica que el bloqueo adquirido se aplique en el nivel de tabla. El tipo de bloqueo que se ha adquirido depende de la instrucción que se esté ejecutando. Por ejemplo, una instrucción SELECT puede adquirir un bloqueo compartido. Al especificar TABLOCK, el bloqueo compartido se aplica a toda la tabla, no en el nivel de fila o de página. Si también se especifica HOLDLOCK, el bloqueo de tabla se mantiene hasta el final de la transacción.  
  
 Al importar datos en un montón mediante INSERT INTO \<target_table > seleccione \<columnas > FROM \<source_table > instrucción, puede habilitar el bloqueo de la instrucción mediante la especificación y el registro optimizados el Sugerencia TABLOCK para la tabla de destino. Además, el modelo de recuperación de la base de datos debe establecerse en registro simple o masivo. Para obtener más información, vea [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 Cuando se usa con la [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) proveedor de conjuntos de filas de forma masiva para importar datos en una tabla, TABLOCK permite que varios clientes carguen datos simultáneamente en la tabla de destino con el bloqueo y el registro optimizados. Para obtener más información, consulte [requisitos previos para el registro mínimo durante la importación masiva](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
 TABLOCKX  
 Especifica que se aplique un bloqueo exclusivo en la tabla.  
  
 UPDLOCK  
 Especifica que se apliquen bloqueos de actualización y se mantengan hasta que se complete la transacción. UPDLOCK aplica bloqueos de actualización para operaciones de lectura solo en el nivel de fila o de página. Si UPDLOCK se combina con TABLOCK, o si se aplica un bloqueo de nivel de tabla por alguna otra razón, se aplicará un bloqueo exclusivo (X) en su lugar.  
  
 Cuando se especifica UPDLOCK, las sugerencias de nivel de aislamiento READCOMMITTED y READCOMMITTEDLOCK se omiten. Por ejemplo, si el nivel de aislamiento de la sesión se establece en SERIALIZABLE y una consulta especifica (UPDLOCK, READCOMMITTED), la sugerencia READCOMMITTED se omitirá y la transacción se ejecutará usando el nivel de aislamiento SERIALIZABLE.  
  
 XLOCK  
 Especifica que se apliquen bloqueos exclusivos y se mantengan hasta que se complete la transacción. Si se especifica junto con ROWLOCK, PAGLOCK o TABLOCK, los bloqueos exclusivos se aplican al nivel de granularidad apropiado.  
  
## <a name="remarks"></a>Comentarios  
 Las sugerencias de tabla se pasan por alto si el plan de consulta no tiene acceso a la tabla. Esto puede deberse a que el optimizador elija no tener acceso a la tabla o a que, en su lugar, se tenga acceso a una vista indizada. En el último caso, el acceso a una vista indizada puede evitarse con la sugerencia de consulta OPTION (EXPAND VIEWS).  
  
 Todas las sugerencias de bloqueo se propagan a todas las tablas y vistas a las que tiene acceso el plan de consulta, incluidas las tablas y vistas a las que se hace referencia en una vista. Asimismo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lleva a cabo las comprobaciones de coherencia de bloqueo correspondientes.  
  
 Las sugerencias de bloqueo ROWLOCK, UPDLOCK y XLOCK que adquieren bloqueos de nivel de fila pueden aplicar bloqueos a claves de índice en lugar de a las filas de datos. Por ejemplo, si una tabla tiene un índice no clúster y un índice de cobertura controla una instrucción SELECT que utiliza una sugerencia de bloqueo, se aplicará un bloqueo a la clave de índice en el índice de cobertura en lugar de aplicarse a la fila de datos de la tabla base.  
  
 Si una tabla contiene columnas calculadas mediante expresiones o funciones que tienen acceso a columnas de otras tablas, las sugerencias de tabla no se utilizan en las otras tablas y no se propagan. Por ejemplo, una sugerencia de tabla NOLOCK se especifica para una tabla de la consulta. Esta tabla tiene columnas calculadas que se calculan mediante una combinación de expresiones y funciones que tienen acceso a columnas de otra tabla. En las tablas a las que hacen referencia estas expresiones y funciones no se utiliza la sugerencia de tabla NOLOCK cuando se tiene acceso.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite más de una sugerencia de tabla de cada uno de los siguientes grupos para cada tabla en la cláusula FROM:  
  
-   Sugerencias de granularidad: PAGLOCK, NOLOCK, READCOMMITTEDLOCK, ROWLOCK, TABLOCK o TABLOCKX.  
  
-   Sugerencias de nivel de aislamiento: HOLDLOCK, NOLOCK, READCOMMITTED, REPEATABLEREAD, SERIALIZABLE.  
  
## <a name="filtered-index-hints"></a>Sugerencias de índice filtrado  
 Un índice filtrado puede usarse como una sugerencia de tabla, pero hará que el optimizador de consultas generar el error 8622 si no cubre todas las filas que la consulta selecciona. A continuación se muestra un ejemplo de una sugerencia de índice filtrado no válida. En el ejemplo se crea el índice filtrado `FIBillOfMaterialsWithComponentID` que, a continuación, se utiliza como una sugerencia de índice para una instrucción SELECT. El predicado de índice filtrado incluye las filas de datos para los ComponentID 533, 324 y 753. El predicado de consulta también incluye las filas de datos para los ComponentID 533, 324 y 753, pero amplía el conjunto de resultados para incluir los ComponentID 855 y 924, que no están en el índice filtrado. Por tanto, el optimizador de consultas no puede usar la sugerencia de índice filtrado y genera el error 8622. Para obtener más información, consulte [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
```  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithComponentID'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithComponentID  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithComponentID"  
    ON Production.BillOfMaterials (ComponentID, StartDate, EndDate)  
    WHERE ComponentID IN (533, 324, 753);  
GO  
SELECT StartDate, ComponentID FROM Production.BillOfMaterials  
    WITH( INDEX (FIBillOfMaterialsWithComponentID) )  
    WHERE ComponentID in (533, 324, 753, 855, 924);  
GO  
```  
  
 El optimizador de consultas no considerará una sugerencia de índice si las opciones SET no tienen los valores necesarios para los índices filtrados. Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="using-noexpand"></a>Usar NOEXPAND  
 NOEXPAND solo se aplica a *vistas indizadas*. Una vista indizada es una vista con un único índice clúster creado en ella. Si una consulta tiene referencias a columnas que están presentes en una vista indizada y en tablas base, y el optimizador de consultas determina que el uso de vistas indizadas proporciona el mejor método para ejecutar la consulta, el optimizador de consultas utiliza el índice en la vista. Esta funcionalidad se denomina *coincidencia de vista indizada*. Anteriores a [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1, el uso automático de una vista indizada por el optimizador de consultas solo se admite en ediciones concretas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Sin embargo, para que el optimizador considere las vistas indizadas para establecer coincidencias o utilice una vista indizada a la que se hace referencia con una sugerencia NOEXPAND, las siguientes opciones SET deben estar establecidas en ON.  
 
> [!NOTE]  
>  La base de datos de SQL Azure es compatible con el uso automático de vistas indizadas sin especificar la sugerencia NOEXPAND.
  
||||  
|-|-|-|  
|ANSI_NULLS|ANSI_WARNINGS|CONCAT_NULL_YIELDS_NULL|  
|ANSI_PADDING|ARITHABORT<sup>1</sup>|QUOTED_IDENTIFIER|  
  
 <sup>1</sup> ARITHABORT se establece implícitamente en ON al establecer ANSI_WARNINGS en ON. Por lo tanto, no es necesario ajustar manualmente este valor.  
  
 Asimismo, la opción NUMERIC_ROUNDABORT debe establecerse en OFF.  
  
 Para exigir que el optimizador utilice un índice para una vista indizada, especifique la opción NOEXPAND. Esta sugerencia solo se puede usar si la vista también aparece en la consulta. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no proporciona ninguna sugerencia que obligue a usar una vista indizada determinada en una consulta que no mencione la vista directamente en la cláusula FROM. Sin embargo, el optimizador de consultas considera el uso de vistas indizadas, incluso aunque no se haga referencia directa a ellas en la consulta.  
  
## <a name="using-a-table-hint-as-a-query-hint"></a>Usar una sugerencia de tabla como una sugerencia de consulta  
 *Sugerencias de tabla* también puede especificarse como una sugerencia de consulta mediante la cláusula OPTION (TABLE HINT). Se recomienda usar una sugerencia de tabla como una sugerencia de consulta únicamente en el contexto de un [Guía de plan](../../relational-databases/performance/plan-guides.md). Para las consultas ad hoc, especifique estas sugerencias únicamente como sugerencias de tabla. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="permissions"></a>Permissions  
 Las sugerencias KEEPIDENTITY, IGNORE_CONSTRAINTS e IGNORE_TRIGGERS requieren permisos ALTER en la tabla.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-tablock-hint-to-specify-a-locking-method"></a>A. Usar la sugerencia TABLOCK para especificar un método de bloqueo  
 En el ejemplo siguiente se especifica que se aplique un bloqueo compartido a la tabla `Production.Product` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] y que se mantenga hasta que finalice la instrucción UPDATE.  
  
```sql  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
### <a name="b-using-the-forceseek-hint-to-specify-an-index-seek-operation"></a>B. Usar la sugerencia FORCESEEK para especificar una operación de búsqueda de índice  
 En el ejemplo siguiente se usa la sugerencia FORCESEEK sin especificar un índice para obligar a que el optimizador de consultas realice una operación de búsqueda de índice en la tabla `Sales.SalesOrderDetail` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT *  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d WITH (FORCESEEK)  
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
GO  
  
```  
  
 En el ejemplo siguiente se usa la sugerencia FORCESEEK con un índice para obligar a que el optimizador de consultas realice una operación de búsqueda de índice en el índice y la columna de índice especificados.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESEEK (PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID (SalesOrderID)))   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);   
GO  
  
```  
  
### <a name="c-using-the-forcescan-hint-to-specify-an-index-scan-operation"></a>C. Usar la sugerencia FORCESCAN para especificar una operación de examen de índice  
 En el ejemplo siguiente se usa la sugerencia FORCESCAN para obligar a que el optimizador de consultas realice una operación de examen en la tabla `Sales.SalesOrderDetail` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESCAN)   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
```  
  
## <a name="see-also"></a>Vea también  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Sugerencias de &#40; Transact-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)  
  
  
