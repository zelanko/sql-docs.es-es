---
title: index_option (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: e7563f9fe992dcf4f9308cccbf11f6310b7925a7
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica un conjunto de opciones que se pueden aplicar a un índice que forma parte de una definición de restricción que se crea mediante [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 PAD_INDEX  **=**  {ON | **OFF** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el relleno del índice. El valor predeterminado es OFF.  
  
 ON  
 El porcentaje de espacio disponible especificado por FILLFACTOR se aplica a páginas de nivel intermedio del índice.  
  
 DESACTIVAR o *fillfactor* no se ha especificado  
 Las páginas de nivel intermedio se llenan casi al máximo de su capacidad, dejando espacio suficiente para al menos una fila del tamaño máximo que admite el índice, en función del conjunto de claves de las páginas intermedias.  
  
 Valor de FILLFACTOR  **=**  *fillfactor*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica un porcentaje que indica cuánto debe llenar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] el nivel hoja de cada página de índice durante la creación o modificación de los índices. El valor especificado debe ser un entero de 1 a 100. El valor predeterminado es 0.  
  
> [!NOTE]  
>  Los valores de factor de relleno 0 y 100 son idénticos en todos los sentidos.  
  
 IGNORE_DUP_KEY  **=**  {ON | **OFF** }  
 Especifica la respuesta de error cuando una operación de inserción intenta insertar valores de clave duplicados en un índice único. La opción IGNORE_DUP_KEY se aplica solamente a operaciones de inserción realizadas tras crear o volver a generar el índice. La opción no tiene ningún efecto cuando se ejecuta [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), o [actualización](../../t-sql/queries/update-transact-sql.md). El valor predeterminado es OFF.  
  
 ON  
 Un mensaje de advertencia se produce cuando se insertan valores de clave duplicados en un índice único. Solo las filas que infrinjan la restricción de unicidad se producirá un error.  
  
 OFF  
 Un mensaje de error se produce cuando se insertan valores de clave duplicados en un índice único. Se revierte toda la operación de INSERCIÓN.  
  
 No se puede establecer IGNORE_DUP_KEY en ON para los índices creados en una vista, índices no únicos, los índices XML, índices espaciales y los índices filtrados.  
  
 Para ver IGNORE_DUP_KEY, utilice [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 En la sintaxis compatible con versiones anteriores, WITH IGNORE_DUP_KEY es equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 Especifica si se vuelven a calcular las estadísticas. El valor predeterminado es OFF.  
  
 ON  
 Las estadísticas obsoletas no se vuelven a calcular automáticamente.  
  
 OFF  
 Se habilita la actualización automática de las estadísticas.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica si se permiten los bloqueos de fila. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de fila se admiten al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila.  
  
 OFF  
 No se usan los bloqueos de fila.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica si se permiten bloqueos de página. El valor predeterminado es ON.  
  
 ON  
 Los bloqueos de página se permiten al obtener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página.  
  
 OFF  
 No se utilizan bloqueos de página.  
  
 SORT_IN_TEMPDB  **=**  {ON | **OFF** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica si se deben almacenar los resultados de ordenación en **tempdb**. El valor predeterminado es OFF.  
  
 ON  
 Los resultados de orden intermedio que se usan para generar el índice se almacenan en **tempdb**. Esto puede reducir el tiempo necesario para crear un índice si **tempdb** está en un conjunto diferente de discos que en la base de datos de usuario. Sin embargo, esto aumenta la cantidad de espacio en disco utilizado durante la generación del índice.  
  
 OFF  
 Los resultados de orden intermedios se almacenan en la misma base de datos que el índice.  
  
 EN LÍNEA  **=**  {ON | **OFF** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica si las tablas subyacentes y los índices asociados están disponibles para realizar consultas y modificar datos durante la operación de índice. El valor predeterminado es OFF. REBUILD se puede realizar como una operación ONLINE.  
  
> [!NOTE]  
>  No es posible crear índices clúster únicos en línea. Entre estos se incluyen los índices creados a causa de una restricción UNIQUE o KEY PRIMARY.  
  
 ON  
 Los bloqueos de tabla de larga duración no se mantienen durante la operación de indización. Durante la fase principal de la operación de índice, solo se mantiene un bloqueo preventivo en la tabla de origen. Esto habilita las consultas o actualizaciones en la tabla subyacente y en los índices. Al inicio de la operación, se mantiene un bloqueo compartido (S) en el objeto de origen durante un período de tiempo muy corto. Al final de la operación, se adquiere un bloqueo S (compartido) sobre el origen durante un corto período, si se está creando un índice no clúster; o bien, se adquiere un bloqueo SCH-M (modificación del esquema) cuando se crea o se quita un índice clúster en línea, y cuando se vuelve a crear un índice clúster o no clúster. Aunque los bloqueos de índice en línea son bloqueos de metadatos cortos, especialmente el bloqueo Sch-M debe esperar a que todas las transacciones de bloqueo se completen en esta tabla. Durante el tiempo de espera, bloqueo Sch-M bloquea las demás transacciones que esperen a este bloqueo al tener acceso a la misma tabla. ONLINE no se puede establecer en ON cuando se crea un índice en una tabla temporal local.  
  
> [!NOTE]  
>  La reconstrucción de índices en línea puede establecer el *low_priority_lock_wait* opciones descritas más adelante en esta sección. *low_priority_lock_wait* administra la prioridad de bloqueos S y Sch-M durante la reconstrucción de índices en línea.  
  
 OFF  
 Los bloqueos de tabla se aplican durante la operación de índice. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación. Una operación de índice sin conexión para crear, volver a crear o quitar un índice clúster, o para volver a crear o quitar un índice no clúster, adquiere un bloqueo de modificación del esquema (Sch-M) de la tabla. Esto evita que todos los usuarios tengan acceso a la tabla subyacente durante la operación. Una operación de índice sin conexión que crea un índice no clúster adquiere un bloqueo compartido (S) en la tabla. Esto evita que se realicen actualizaciones en la tabla subyacente, pero permite la realización de operaciones de lectura, como instrucciones SELECT.  
  
 Para obtener más información, consulte [cómo funcionan de las operaciones de índice en línea](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de índice. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
 *max_degree_of_parallelism* puede ser:  
  
 - 1 - Suprime la generación de planes paralelos.  
 - \>1 - restringe el número máximo de procesadores utilizados en una operación de índice en paralelo al número especificado.  
 - 0 (valor predeterminado): se utiliza el número real de procesadores o menos, según la carga de trabajo del sistema actual.  
  
 Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operaciones de índice en paralelo no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la opción de compresión de datos para la tabla, el número de partición o el intervalo de particiones especificados. Las opciones son las siguientes:  
  
 NONE  
 No se comprimen la tabla ni las particiones especificadas. Solo se aplica a tablas de almacén de filas; no se aplica a tablas de almacén de columnas.  
  
 ROW  
 La tabla o las particiones especificadas se comprimen utilizando la compresión de fila. Solo se aplica a tablas de almacén de filas; no se aplica a tablas de almacén de columnas.  
  
 PAGE  
 La tabla o las particiones especificadas se comprimen utilizando la compresión de página. Solo se aplica a tablas de almacén de filas; no se aplica a tablas de almacén de columnas.  
  
 COLUMNSTORE  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a tablas de almacén de columnas. COLUMNSTORE especifica que se descomprima una partición que se comprimió con la opción COLUMNSTORE_ARCHIVE. Cuando se restauran los datos, el índice de almacén sigue estando comprimidos con la compresión de almacén de columnas que se usa para todas las tablas de almacén de columnas.  
  
 COLUMNSTORE_ARCHIVE  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a las tablas de almacén de columnas almacenadas con un índice clúster de almacén de columnas. COLUMNSTORE_ARCHIVE más comprime la partición especificada a un tamaño menor. Esto se puede usar para el archivado o para otras situaciones que requieran menos almacenamiento y en las que pueda permitirse más tiempo para el almacenamiento y recuperación.  
  
 Para obtener más información acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
EN las particiones **(** { \<partition_number_expression > | \<intervalo >} [ **,**...  *n*  ] **)** **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica las particiones a las que se aplica el valor DATA_COMPRESSION. Si la tabla no tiene particiones, el argumento ON PARTITIONS generará un error. Si no se proporciona la cláusula ON PARTITIONS, la opción DATA_COMPRESSION se aplica a todas las particiones de una tabla con particiones.  
  
\<partition_number_expression > se puede especificar de las maneras siguientes:  
  
-   Proporcionando el número de una partición, por ejemplo: ON PARTITIONS (2).  
-   Proporcionar los números de partición de varias particiones separados por comas, por ejemplo: ON PARTITIONS (1, 5).  
-   Proporcionar intervalos y particiones individuales: ON PARTITIONS (2, 4, 6 TO 8).  
  
\<intervalo > se puede especificar como números de partición separados por la palabra TO, por ejemplo: ON PARTITIONS (6 a 8).  
  
 Para establecer diferentes tipos de compresión de datos para distintas particiones, especifique la opción DATA_COMPRESSION más de una vez, por ejemplo:  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option >**  
 En la mayoría de los casos, la regeneración de un índice hace que se vuelvan a generar todas las particiones de un índice con particiones. Cuando las opciones siguientes se aplican a una partición única, no vuelven a generar todas las particiones.  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 A **conmutador** o regeneración de índice en línea completa tan pronto como hay ninguna operación bloqueo para esta tabla. *WAIT_AT_LOW_PRIORITY* indica que si el **conmutador** o la operación de regeneración de índice en línea no se puede completar inmediatamente, esperará. La operación contiene los bloqueos de prioridad baja, lo que permite a otras operaciones que mantengan bloqueos en conflicto con la instrucción DDL para continuar. Si se omite la **WAIT AT LOW PRIORITY** opción es equivalente a `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.  
  
MAX_DURATION = *tiempo* [**minutos** ]  
 El tiempo de espera (valor entero especificado en minutos) que el **conmutador** o esperas de bloqueo de regeneración de índice en línea que debe adquirirse, al ejecutar el comando DDL. SWITCH o la operación de regeneración de índices en línea intenta completarse inmediatamente. Si la operación se bloquea durante la **MAX_DURATION** tiempo, uno de los **ABORT_AFTER_WAIT** las acciones se ejecutan. **MAX_DURATION** hora es siempre en minutos y la palabra **minutos** puede omitirse.  
  
ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOQUEADORES** }]  
 Ninguno  
 Continúa la **conmutador** o la operación de regeneración sin cambiar la prioridad de bloqueos (con prioridad normal) de índice en línea.  
  
SELF  
 Cierra el **conmutador** o la operación de DDL de regeneración de índice en línea que se está ejecutando actualmente sin realizar ninguna acción.  
  
BLOCKERS  
 Elimina todas las transacciones de usuario que bloqueen actualmente la **conmutador** u operación DDL de regeneración para que pueda continuar la operación de índice en línea.  
 BLOQUEADORES requiere la **ALTER ANY CONNECTION** permiso.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener una descripción completa de opciones de índice, vea [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [definición_de_columna_calculada &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 

