---
title: "Modifique la función de partición (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION FUNCTION
- ALTER_PARTITION_FUNCTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- splitting partitions [SQL Server]
- partitioned tables [SQL Server], splitting
- ALTER PARTITION FUNCTION statement
- merging partitions [SQL Server]
- partitioned indexes [SQL Server], merging
- partitioned indexes [SQL Server], splitting
- modifying partition functions
- partition functions [SQL Server], modifying
- partitioned tables [SQL Server], merging
ms.assetid: 70866dac-0a8f-4235-8108-51547949ada4
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66b921eb3bd6378d20de11a0197a20c957d14ac6
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="alter-partition-function-transact-sql"></a>ALTER PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Modifica una función de partición dividiendo o mezclando sus valores de límite. Ejecutando ALTER PARTITION FUNCTION, se puede dividir una partición de cualquier tabla o índice que utilice la función de partición en dos particiones, o bien se pueden mezclar dos particiones en una partición menos.  
  
> [!CAUTION]  
>  Varias tablas o índices pueden utilizar la misma función de partición. ALTER PARTITION FUNCTION afecta a todas ellas en una única transacción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER PARTITION FUNCTION partition_function_name()  
{   
    SPLIT RANGE ( boundary_value )  
  | MERGE RANGE ( boundary_value )   
} [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_function_name*  
 Es el nombre de la función de partición que se va a modificar.  
  
 SPLIT RANGE ( *boundary_value* )  
 Agrega una partición a la función de partición. *boundary_value* determina el intervalo de la nueva partición y debe diferir de los intervalos de límites existentes de la función de partición. En función de *boundary_value*, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] uno de los intervalos existentes se divide en dos. De estos dos, donde la nueva *boundary_value* reside se considera la nueva partición.  
  
 Debe existir un grupo de archivos en línea y estar marcado por el esquema de partición que utiliza la función de partición como NEXT USED para contener la nueva partición. Los grupos de archivos se asignan a particiones de una instrucción CREATE PARTITION SCHEME. Si la instrucción CREATE PARTITION SCHEME asigna más grupos de archivos de los necesarios (se crean menos particiones en la instrucción CREATE PARTITION FUNCTION que grupos de archivos para contenerlos), habrá entonces grupos de archivos sin asignar y el esquema de partición marcará uno de ellos como NEXT USED. Este grupo de archivos contendrá la partición nueva. Si no hay grupos de archivos marcados como NEXT USED por el esquema de partición, debe usar ALTER PARTITION SCHEME para agregar un grupo de archivos o designar uno existente a fin de que contenga la partición nueva. Se puede designar a un grupo de archivos que ya contenga particiones para contener particiones adicionales. Puesto que una función de partición puede participar en más de un esquema de partición, todos los esquemas de partición que utilizan la función de partición a la que esté agregando particiones deben tener un grupo de archivos NEXT USED. De lo contrario, ALTER PARTITION FUNCTION produce un error que muestra el esquema o esquemas de partición a los que les falta un grupo de archivos NEXT USED.  
  
 Si crea todas las particiones en el mismo grupo de archivos, ese grupo se asigna inicialmente para que sea el grupo de archivos NEXT USED automáticamente. Sin embargo, después de realizarse una operación de división ya no hay ningún grupo de archivos NEXT USED designado. Debe asignar explícitamente el grupo de archivos para que sea el grupo de archivos NEXT USED usando ALTER PARTITION SCHEME; de lo contrario, una operación de división posterior producirá errores.  
  
> [!NOTE]  
>  Limitaciones en el índice de almacén de columnas: solo las particiones vacías se pueden dividir en cuando existe un índice de almacén de columnas en la tabla. Debe quitar o deshabilitar el índice de almacén de columnas antes de realizar esta operación  
  
 COMBINAR [intervalo ( *boundary_value*)]  
 Quita una partición y mezcla cualquier valor que exista en la partición en una de las particiones restantes. INTERVALO (*boundary_value*) debe ser un valor de límite existente, en la que se combinan los valores de la partición quitada. El grupo de archivos que originalmente contenía *boundary_value* se quitará el esquema de partición a menos que se usa una partición restante o se marca con la propiedad NEXT USED. La partición mezclada se encuentra en el grupo de archivos que originalmente no contenía *boundary_value*. *boundary_value* es una expresión constante que puede hacer referencia a variables (incluidas las variables de tipo definido por el usuario) o funciones (incluidas funciones definidas por el usuario). No puede hacer referencia a una expresión de [!INCLUDE[tsql](../../includes/tsql-md.md)]. *boundary_value* debe cualquiera coincidan con o poder convertirse implícitamente al tipo de datos de la columna de partición correspondiente y no se puede truncar durante la conversión implícita de forma que el tamaño y la escala del valor no coincidan con su correspondiente *input_parameter_type*.  
  
> [!NOTE]  
>  Limitaciones en el índice de almacén de columnas: no se pueden combinar dos particiones no vacías que contiene un índice de almacén de columnas. Debe quitar o deshabilitar el índice de almacén de columnas antes de realizar esta operación  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Mantenga siempre las particiones vacías en ambos extremos del rango de partición para garantizar que la división de particiones (antes de cargar nuevos datos) y la combinación de particiones (después de descargar datos antiguos) no realicen ningún movimiento de datos. Evite dividir o combinar particiones con datos. Esto puede ser extremadamente ineficaz, ya que puede multiplicar por cuatro la generación de registros y causar bloqueos graves.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 ALTER PARTITION FUNCTION vuelve a crear particiones en cualquier tabla o índice que utilice la función en una única operación atómica. Sin embargo, esta operación se produce sin conexión, y dependiendo del alcance de las reparticiones puede consumir muchos recursos.  
  
 ALTER PARTITION FUNCTION se puede utilizar solamente para dividir una partición en dos o mezclar dos particiones en una. Para cambiar el modo en el que se crean particiones en una tabla (por ejemplo, de 10 particiones a 5), puede aplicar cualquiera de las opciones siguientes. Dependiendo de la configuración del sistema, estas opciones pueden tener un consumo de recursos diferente:  
  
-   Cree una nueva tabla con particiones con la función de partición deseada y, a continuación, inserte los datos de la tabla antigua en la tabla nueva mediante la instrucción INSERT INTO...SELECT FROM.  
  
-   Cree un índice clúster con particiones en un montón.  
  
    > [!NOTE]  
    >  El resultado de quitar un índice clúster con particiones es un montón con particiones.  
  
-   Quite y vuelva a generar un índice con particiones existente mediante la instrucción CREATE INDEX de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la cláusula DROP EXISTING = ON.  
  
-   Ejecute una secuencia de instrucciones ALTER PARTITION FUNCTION.  
  
 Todos los grupos de archivos que estén afectados por ALTER PARTITION FUNCTION deben estar en línea.  
  
 ALTER PARTITION FUNCTION produce un error cuando existe un índice clúster deshabilitado en cualquiera de las tablas que utilizan la función de partición.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no proporciona compatibilidad de replicación para modificar una función de partición. Los cambios en la función de partición de la base de datos de publicaciones se deben aplicar manualmente en la base de datos de suscripciones.  
  
## <a name="permissions"></a>Permissions  
 Se pueden utilizar cualquiera de los siguientes permisos para ejecutar ALTER PARTITION FUNCTION:  
  
-   Permiso ALTER ANY DATASPACE. De forma predeterminada, este permiso corresponde a los miembros del rol fijo de servidor **sysadmin** y a los roles fijos de base de datos **db_owner** y **db_ddladmin** .  
  
-   Permiso CONTROL o ALTER en la base de datos en la que se ha creado la función de partición.  
  
-   Permiso CONTROL SERVER o ALTER ANY DATABASE en el servidor de la base de datos en la que se ha creado la función de partición.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-splitting-a-partition-of-a-partitioned-table-or-index-into-two-partitions"></a>A. Dividir una partición de una tabla o un índice con particiones en dos particiones  
 En el ejemplo siguiente se crea una función de partición para crear cuatro particiones en una tabla o en un índice. `ALTER PARTITION FUNCTION` divide una de las particiones en dos para crear un total de cinco particiones.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Split the partition between boundary_values 100 and 1000  
--to create two partitions between boundary_values 100 and 500  
--and between boundary_values 500 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
SPLIT RANGE (500);  
```  
  
### <a name="b-merging-two-partitions-of-a-partitioned-table-into-one-partition"></a>B. Mezclar dos particiones de una tabla con particiones en una partición  
 En el ejemplo siguiente se crea la misma función de partición que antes y después se mezclan dos de las particiones en una partición para conseguir un total de tres particiones.  
  
```sql  
IF EXISTS (SELECT * FROM sys.partition_functions  
    WHERE name = 'myRangePF1')  
DROP PARTITION FUNCTION myRangePF1;  
GO  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
GO  
--Merge the partitions between boundary_values 1 and 100  
--and between boundary_values 100 and 1000 to create one partition  
--between boundary_values 1 and 1000.  
ALTER PARTITION FUNCTION myRangePF1 ()  
MERGE RANGE (100);  
```  
  
## <a name="see-also"></a>Vea también  
 [Índices y tablas con particiones](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Sys.partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [Sys.partition_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [Sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
