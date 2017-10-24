---
title: ALTER PARTITION SCHEME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545fe3da48f0d0c98d72b32e5a82d9fd55579d00
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un grupo de archivos a un esquema de partición o altera la designación del grupo de archivos NEXT USED para el esquema de partición.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_scheme_name*  
 Es el nombre del esquema de partición que se va a modificar.  
  
 *filegroup_name*  
 Especifica el grupo de archivos que el esquema de partición debe marcar como NEXT USED. Esto significa que el grupo de archivos aceptará una nueva partición que se crea mediante un [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md) instrucción.  
  
 En un esquema de partición, solo un grupo de archivos puede designarse como NEXT USED. Puede especificarse un grupo de archivos que no esté vacío. Si *filegroup_name* se especifica y actualmente no hay ningún grupo de archivos marcado como NEXT USED, *filegroup_name* se marca como NEXT USED. Si *filegroup_name* se especifica y ya existe un grupo de archivos con la propiedad NEXT USED, la propiedad NEXT USED se transfiere desde el grupo de archivos existente a *filegroup_name*.  
  
 Si *filegroup_name* no se especifica y ya existe un grupo de archivos con la propiedad NEXT USED, ese grupo de archivos pierde su estado NEXT USED para que no hay ningún grupo de archivos NEXT USED de *partition_scheme_name*.  
  
 Si *filegroup_name* no se especifica y no hay ningún grupos de archivos marcados como NEXT USED, ALTER PARTITION SCHEME devuelve una advertencia.  
  
## <a name="remarks"></a>Comentarios  
 Los grupos de archivos afectados por ALTER PARTITION SCHEME deben estar en línea.  
  
## <a name="permissions"></a>Permissions  
 Sección los siguientes permisos puede utilizarse para ejecutar ALTER PARTITION SCHEME:  
  
-   Permiso ALTER ANY DATASPACE. De forma predeterminada, este permiso corresponde a los miembros del rol fijo de servidor **sysadmin** y a los roles fijos de base de datos **db_owner** y **db_ddladmin** .  
  
-   Permiso CONTROL o ALTER en la base de datos en la que se ha creado el esquema de partición.  
  
-   Permiso CONTROL SERVER o ALTER ANY DATABASE en el servidor de la base de datos en la que se ha creado el esquema de partición.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se asume que el esquema de partición `MyRangePS1` y el grupo de archivos `test5fg` existen en la base de datos actual.  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 El grupo de archivos `test5fg` recibirá las particiones adicionales de una tabla o índice con particiones como resultado de una instrucción ALTER PARTITION FUNCTION.  
  
## <a name="see-also"></a>Vea también  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sys.partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [Sys.destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

