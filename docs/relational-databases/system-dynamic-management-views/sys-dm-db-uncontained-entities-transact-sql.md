---
title: sys.dm_db_uncontained_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_uncontained_entities
- dm_db_uncontained_entities_TSQL
- sys.dm_db_uncontained_entities_TSQL
- dm_db_uncontained_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_uncontained_entities dynamic management view
ms.assetid: f417efd4-8c71-4f81-bc9c-af13bb4b88ad
author: stevestein
ms.author: sstein
ms.openlocfilehash: 625c6134c91a9b452b8df2b7e235b78126c1354e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026920"
---
# <a name="sysdmdbuncontainedentities-transact-sql"></a>sys.dm_db_uncontained_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los objetos no contenidos que se usan en la base de datos. Los objetos no contenidos son objetos que traspasan el límite de la base de datos en una base de datos independiente. A esta vista se puede acceder tanto desde una base de datos independiente como desde una dependiente. Si sys.dm_db_uncontained_entities está vacía, la base de datos no usa entidades no contenidas.  
  
 Si un módulo traspasa el límite de la base de datos más de una vez, solo se notifica la primera incidencia detectada.  
  
||||  
|-|-|-|  
|**Nombre de columna**|**Tipo**|**Descripción**|  
|*class*|**int**|1 = Objeto o columna (incluye módulos, XP, vistas, sinónimos y tablas).<br /><br /> 4 = entidad de seguridad de base de datos<br /><br /> 5 = Ensamblado<br /><br /> 6 = Tipo<br /><br /> 7 = Índice (índice de texto completo)<br /><br /> 12 = desencadenador DDL de base de datos<br /><br /> 19 = Ruta<br /><br /> 30 = Especificación de auditoría|  
|*class_desc*|**nvarchar(120)**|Descripción de la clase de la entidad. Una de las siguientes acciones para que coincida con la clase:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **DATABASE_PRINCIPAL**<br /><br /> **ASSEMBLY**<br /><br /> **TYPE**<br /><br /> **INDEX**<br /><br /> **DATABASE_DDL_TRIGGER**<br /><br /> **ROUTE**<br /><br /> **AUDIT_SPECIFICATION**|  
|*major_id*|**int**|Identificador de la entidad.<br /><br /> Si *clase* = 1, entonces object_id<br /><br /> Si *clase* = 4, a continuación, sys.database_principals.principal_id.<br /><br /> Si *clase* = 5, entonces sys.assemblies.assembly_id.<br /><br /> Si *clase* = 6, entonces sys.types.user_type_id.<br /><br /> Si *clase* = 7, entonces sys.indexes.index_id.<br /><br /> Si *clase* = 12, entonces sys.triggers.object_id.<br /><br /> Si *clase* = 19, entonces sys.routes.route_id.<br /><br /> Si *clase* = 30, entonces sys. database_audit_specifications.database_specification_id.|  
|*statement_line_number*|**int**|Si la clase es un módulo, devuelve el número de línea en el que se encuentra el uso del objeto no contenido.  De lo contrario, el valor es NULL.|  
|*statement_ offset_begin*|**int**|Si la clase es un módulo, indica en bytes, comenzando por 0, la posición inicial donde comienza el uso del objeto no contenido. De lo contrario el valor devuelto es NULL.|  
|*statement_ offset_end*|**int**|Si la clase es un módulo, indica en bytes, comenzando por 0, la posición final del uso del objeto no contenido. El valor -1 indica el final del módulo. De lo contrario el valor devuelto es NULL.|  
|*statement_type*|**nvarchar(512)**|El tipo de instrucción.|  
|*nombre de feature_*|**nvarchar(256)**|Devuelve el nombre externo del objeto.|  
|*feature_type_name*|**nvarchar(256)**|Devuelve el tipo de característica.|  
  
## <a name="remarks"></a>Comentarios  
 Sys.dm_db_uncontained_entities muestra las entidades que podrían traspasar el límite de la base de datos. Devolverá cualquier entidad del usuario que tenga potencial para usar los objetos fuera de la base de datos.  
  
 Se notifican los siguientes tipos de características.  
  
-   Comportamiento de la contención desconocido (resolución diferida de nombres o SQL dinámico)  
  
-   comando DBCC  
  
-   Procedimiento almacenado del sistema  
  
-   Función escalar del sistema  
  
-   Función con valores de tabla del sistema  
  
-   Función integrada del sistema  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Sys.dm_db_uncontained_entities solo devuelve objetos para el que el usuario tiene algún tipo de permiso. Para evaluar exhaustivamente la contención de la base de datos se debe usar esta función por un usuario con privilegios elevados, como un miembro de la **sysadmin** rol fijo de servidor o el **db_owner** rol.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un procedimiento denominado P1 y, a continuación, se consulta `sys.dm_db_uncontained_entities`. La consulta notifica que P1 usa **sys.endpoints** , que está fuera de la base de datos.  
  
```sql  
CREATE DATABASE Test;  
GO  
  
USE Test;  
GO  
CREATE PROC P1  
AS   
SELECT * FROM sys.endpoints ;  
GO  
SELECT SO.name, UE.* FROM sys.dm_db_uncontained_entities AS UE  
LEFT JOIN sys.objects AS SO  
    ON UE.major_id = SO.object_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos independientes](../../relational-databases/databases/contained-databases.md)  
  
  
