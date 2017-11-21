---
title: "CREAR el esquema de partición (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 04/10/2017
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
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13bd8b623604f8bfe93dcf4483c65be14f43f003
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un esquema en la base de datos actual que asigna a grupos de archivos las particiones de una tabla o índice con particiones. El número y el dominio de las particiones de una tabla o índice con particiones se determinan en una función de partición. Una función de partición debe crearse en un [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md) instrucción antes de crear un esquema de partición.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_scheme_name*  
 Es el nombre del esquema de partición. Los nombres de esquema de partición deben ser únicos dentro de la base de datos y cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *partition_function_name*  
 Es el nombre de la función de partición que utiliza el esquema de partición. Las particiones creadas por la función de partición se asignan a los grupos de archivos especificados en el esquema de partición. *partition_function_name* ya debe existir en la base de datos. Una única partición no puede contener grupos de archivos FILESTREAM y no FILESTREAM a la vez.  
  
 ALL  
 Especifica que todas las particiones se asignan al grupo de archivos proporcionado en *file_group_name*, o al grupo de archivos principal si **[**principal**]** se especifica. Si se especifica ALL, solo un *file_group_name* se puede especificar.  
  
 *file_group_name* | **[** principal **]** [ **,***.. .n*]  
 Especifica los nombres de los grupos de archivos para almacenar las particiones especificadas por *partition_function_name*. *file_group_name* ya debe existir en la base de datos.  
  
 Si **[**principal**]** se especifica, la partición se almacena en el grupo de archivos principal. Si se especifica ALL, solo un *file_group_name* se puede especificar. Las particiones se asignan a grupos de archivos, a partir de la partición 1, en el orden en que se muestran los grupos de archivos en [**,***.. .n*]. El mismo *file_group_name* se puede especificar más de una vez en [**,***.. .n*]. Si  *n*  no es suficiente para contener el número de particiones especificadas en *partition_function_name*, CREATE PARTITION SCHEME generará un error.  
  
 Si *partition_function_name* genera menos particiones que grupos de archivos, el primer grupo de archivos sin asignar se marca como NEXT USED y nomenclatura de archivos NEXT USED muestra un mensaje de información. Si se especifica ALL, el mero *file_group_name* mantiene su propiedad NEXT USED para este *partition_function_name*. El grupo de archivos NEXT USED recibirá una partición adicional si se crea una en una instrucción ALTER PARTITION FUNCTION. Si desea crear más grupos de archivos sin asignar para almacenar las nuevas particiones, utilice ALTER PARTITION SCHEME.  
  
 Cuando se especifica el grupo de archivos principal en *file_group_name* [1**,***.. .n*], PRIMARY debe estar delimitado, como en **[**principal**]** , porque es una palabra clave.  
  
 Solo se admite PRIMARY para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]. Vea el ejemplo siguiente de E. 
  
## <a name="permissions"></a>Permissions  
 Se pueden utilizar los permisos siguientes para ejecutar CREATE PARTITION SCHEME:  
  
-   Permiso ALTER ANY DATASPACE. De forma predeterminada, este permiso corresponde a los miembros del rol fijo de servidor **sysadmin** y a los roles fijos de base de datos **db_owner** y **db_ddladmin** .  
  
-   Permiso CONTROL o ALTER en la base de datos en la que se va a crear el esquema de partición.  
  
-   Permiso CONTROL SERVER o ALTER ANY DATABASE en el servidor de la base de datos en la que se va a crear el esquema de partición.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>A. Crear un esquema de partición que asigne cada partición a un grupo de archivos diferente  
 En el ejemplo siguiente se crea una función de partición para crear cuatro particiones en una tabla o en un índice. Después, se crea un esquema de partición que especifica los grupos de archivos que van a contener cada una de las cuatro particiones. En este ejemplo se asume que los grupos de archivos ya existen en la base de datos.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 Las particiones de una tabla que usa la función de partición `myRangePF1` en la columna de partición **col1** se asignarían como se muestra en la tabla siguiente.  
  
||||||  
|-|-|-|-|-|  
|**Grupo de archivos**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**Partición**|1|2|3|4|  
|**Valores**|**col1** <= `1`|**col1**  >  `1` AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>B. Crear un esquema de partición que asigne varias particiones al mismo grupo de archivos  
 Si todas las particiones se asignan al mismo grupo de archivos, utilice la palabra clave ALL. Sin embargo, si se asignan varias particiones (no todas) al mismo grupo de archivos, el nombre del grupo de archivos debe repetirse, tal como se muestra en el ejemplo siguiente.  
  
```  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 Las particiones de una tabla que usa la función de partición `myRangePF2` en la columna de partición **col1** se asignarían como se muestra en la tabla siguiente.  
  
||||||  
|-|-|-|-|-|  
|**Grupo de archivos**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**Partición**|1|2|3|4|  
|**Valores**|**col1** <= `1`|**col1** > 1 AND **col1** <= `100`|**col1**  >  `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>C. Crear un esquema de partición que asigne todas las particiones al mismo grupo de archivos  
 En el ejemplo siguiente se crea la misma función de partición que en los ejemplos anteriores y se crea un esquema de partición que asigna todas las particiones al mismo grupo de archivos.  
  
```  
CREATE PARTITION FUNCTION myRangePF3 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>D. Crear un esquema de partición que especifica un grupo de archivos NEXT USED  
 En el ejemplo siguiente se crea la misma función de partición que en los ejemplos anteriores y se crea un esquema de partición que especifica un número de grupos de archivos superior al número de particiones creadas por la función de partición asociada.  
  
```  
CREATE PARTITION FUNCTION myRangePF4 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 Al ejecutar la instrucción se devuelve el mensaje siguiente.  
  
Esquema de partición 'myRangePS4' se ha creado correctamente. 'test5fg' está marcado como el siguiente grupo de archivos utilizado en el esquema de partición 'myRangePS4'.  
  
  
 Si la función de partición `myRangePF4` se cambia para agregar una partición, el grupo de archivos `test5fg` recibe la partición que acaba de crearse.  

### <a name="e-creating-a-partition-schema-only-on-primary---only-primary-is-supported-for-includesqldbesaincludessqldbesa-mdmd"></a>E. Crear un esquema de partición solo en principal: principal solo se admite para[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

 En el ejemplo siguiente se crea una función de partición para crear cuatro particiones en una tabla o en un índice. Se crea, a continuación, un esquema de partición que especifica que todas las particiones se crean en el grupo de archivos principal.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>Vea también  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear tablas con particiones e índices](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [Sys.partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [Sys.destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

