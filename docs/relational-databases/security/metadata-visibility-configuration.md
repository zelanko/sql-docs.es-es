---
title: "Configuración de visibilidad de los metadatos | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9381b69a605ed7928851a18e64d7054d43fcb65c
ms.lasthandoff: 04/11/2017

---
# <a name="metadata-visibility-configuration"></a>Configuración de visibilidad de los metadatos
  La visibilidad de los metadatos se limita a los elementos protegibles que son propiedad de un usuario o sobre los que el usuario tienen algún permiso. Por ejemplo, la siguiente consulta devuelve una fila si se ha concedido al usuario un permiso como SELECT o INSERT sobre la tabla `myTable`.  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = 'myTable';  
GO  
```  
  
 Sin embargo, si el usuario no dispone de ningún permiso sobre `myTable`, la consulta devuelve un conjunto de resultados vacío.  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>Ámbito e impacto de la configuración de visibilidad de los metadatos  
 La configuración de visibilidad de los metadatos solo se aplica a los siguientes elementos protegibles:  
  
|||  
|-|-|  
|Vistas de catálogo|Procedimientos almacenados **sp_help** de [!INCLUDE[ssDE](../../includes/ssde-md.md)]|  
|Funciones integradas que exponen metadatos|Vistas de esquema de información|  
|Vistas de compatibilidad|Propiedades extendidas|  
  
 La configuración de visibilidad de los metadatos no se aplica a los siguientes elementos protegibles:  
  
|||  
|-|-|  
|Tablas de sistema de trasvase de registros|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tablas de sistema del Agente|  
|Tablas de sistema de planes de mantenimiento de bases de datos|Tablas de sistema de copia de seguridad|  
|Tablas de sistema de replicación|Procedimientos almacenados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_help **de replicación y del Agente**|  
  
 Una accesibilidad limitada a los metadatos significa lo siguiente:  
  
-   Las aplicaciones que asuman un acceso **public** a los metadatos se interrumpirán.  
  
-   Las consultas que se realicen en vistas del sistema puede que solo devuelvan un subconjunto de filas o, en ocasiones, un conjunto de resultados vacío.  
  
-   Las funciones integradas que emiten metadatos, como OBJECTPROPERTYEX, pueden devolver NULL.  
  
-   Los procedimientos almacenados [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** stored procedures might return only a subset of rows, or NULL.  
  
 Los módulos SQL, como procedimientos almacenados y desencadenadores, se ejecutan en el contexto de seguridad del autor de la llamada y, por tanto, tienen un acceso limitado a los metadatos. Por ejemplo, en el siguiente código, cuando el procedimiento almacenado intenta obtener acceso a los metadatos de la tabla `myTable` sobre la que el autor de la llamada no tienen ningún derecho, se devuelve un conjunto de resultados vacío. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se devuelve una fila.  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, id   
FROM sysobjects   
WHERE name = 'myTable';  
END;  
GO  
```  
  
 Para permitir que los autores de la llamada vean los metadatos, puede concederles un permiso VIEW DEFINITION en un ámbito adecuado: nivel de objeto, base de datos o servidor. Por lo tanto, en el ejemplo anterior, si el autor de la llamada dispone de permiso VIEW DEFINITION sobre `myTable`, el procedimiento almacenado devuelve una fila. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) y [GRANT &#40;permisos de base de datos de Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
 También puede modificar el procedimiento almacenado para que se ejecute bajo las credenciales del propietario. Cuando el propietario del procedimiento y el propietario de la tabla son el mismo, se aplica el encadenamiento de propiedad, y el contexto de seguridad del propietario del procedimiento permite el acceso a los metadatos de `myTable`. En un escenario de este tipo, el siguiente código devuelve una fila de metadatos al autor de la llamada.  
  
> [!NOTE]  
>  En el siguiente ejemplo se usa la vista de catálogo [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) en lugar de la vista de compatibilidad [sys.sysobjects](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md) .  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, id  
FROM sys.objects   
WHERE name = 'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  Puede utilizar EXECUTE AS para cambiar temporalmente al contexto de seguridad del autor de la llamada. Para obtener más información, vea [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md).  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>Beneficios y límites de la configuración de visibilidad de los metadatos  
 La configuración de visibilidad de los metadatos puede desempeñar un rol importante en el plan de seguridad global. Sin embargo, hay casos en los que un usuario con conocimientos y determinación puede forzar la divulgación de algunos metadatos. Es recomendable implementar permisos sobre los metadatos como una de las distintas medidas de defensa más completa.  
  
 Teóricamente, es posible forzar la emisión de metadatos en los mensajes de error mediante la manipulación del orden de evaluación de predicados en las consultas. La posibilidad de estos *ataques de prueba y error* no es específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es una implicación de las transformaciones asociativas y conmutativas que admite el álgebra relacional. Puede mitigar este riesgo mediante la limitación de la información que se devuelve en los mensajes de error. Para restringir más la visibilidad de metadatos de esta manera, puede iniciar el servidor con la marca de seguimiento 3625. Esta marca de seguimiento limita la cantidad de información que se muestra en los mensajes de error. A su vez, ayuda a evitar divulgaciones forzadas. La contrapartida es que los mensajes de error se simplificarán y puede resultar difícil su uso para fines de depuración. Para obtener más información, vea [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md) y [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
 Los metadatos que se muestran a continuación no están sujetos a una divulgación forzada:   
  
-   El valor almacenado en la columna **provider_string** de **sys.servers**. Un usuario que no disponga de permiso ALTER ANY LINKED SERVER verá un valor NULL en esta columna.  
  
-   La definición de origen de un objeto especificado por el usuario, como un procedimiento almacenado o desencadenador. El código fuente solo es visible cuando una de las siguientes afirmaciones es cierta:  
  
    -   El usuario dispone de permiso VIEW DEFINITION sobre el objeto.  
  
    -   No se ha denegado al usuario el permiso VIEW DEFINITION sobre el objeto y dispone de permiso CONTROL, ALTER o TAKE OWNERSHIP sobre el objeto. El resto de usuarios verán NULL.  
  
-   Las columnas de definición de las siguientes vistas de catálogo:  
  
    |||  
    |-|-|  
    |**sys.all_sql_modules**|**sys.sql_modules**|  
    |**sys.server_sql_modules**|**sys.check_constraints**|  
    |**sys.default_constraints**|**sys.computed_columns**|  
    |**sys.numbered_procedures**||  
  
-   La columna **ctext** de la vista de compatibilidad **syscomments** .  
  
-   El resultado del procedimiento **sp_helptext** .  
  
-   Las siguientes columnas de las vistas de esquema de información:  
  
    |||  
    |-|-|  
    |INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE|INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT|INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION|INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION|  
  
-   La función OBJECT_DEFINITION()  
  
-   El valor almacenado en la columna password_hash de **sys.sql_logins**.  Un usuario que no tenga un permiso CONTROL SERVER verá un valor NULL en esta columna.  
  
> [!NOTE]  
>  Las definiciones SQL de procedimientos y funciones del sistema integrados son visibles de forma pública a través de la vista de catálogo **sys.system_sql_modules** , el procedimiento almacenado **sp_helptext** y la función OBJECT_DEFINITION().  
  
## <a name="general-principles-of-metadata-visibility"></a>Principios generales de visibilidad de los metadatos  
 A continuación, se muestran algunos de los principios generales que hay que tener en cuenta de cara a la visibilidad de los metadatos:  
  
-   Permisos implícitos de roles fijos  
  
-   Ámbito de los permisos  
  
-   Prioridad de DENY  
  
-   Visibilidad de los metadatos de subcomponentes  
  
### <a name="fixed-roles-and-implicit-permissions"></a>Roles fijos y permisos implícitos  
 Los metadatos a los que pueden obtener acceso los roles fijos dependen de sus permisos implícitos correspondientes.  
  
### <a name="scope-of-permissions"></a>Ámbito de los permisos  
 Los permisos de un ámbito implican la posibilidad de ver los metadatos en dicho ámbito y en todos los ámbitos incluidos en el mismo. Por ejemplo, el permiso SELECT sobre un esquema implica que el receptor dispone del permiso SELECT sobre todos los elementos protegibles incluidos en dicho esquema. Por tanto, la concesión del permiso SELECT sobre un esquema permite al usuario ver los metadatos del esquema y todas las tablas, vistas, funciones, procedimientos, colas, sinónimos, tipos y colecciones de esquemas XML que estén incluidos en el mismo. Para obtener más información sobre ámbitos, vea [Jerarquía de permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
### <a name="precedence-of-deny"></a>Prioridad de DENY   
 Normalmente, DENY tiene prioridad sobre otros permisos. Por ejemplo, si se concede a un usuario de la base de datos el permiso EXECUTE sobre un esquema, pero se le deniega el permiso EXECUTE sobre un procedimiento almacenado de dicho esquema, el usuario no podrá ver los metadatos de dicho procedimiento almacenado.  
  
 Además, si a un usuario se le deniega el permiso EXECUTE sobre un esquema pero se le concede el permiso EXECUTE sobre un procedimiento almacenado de dicho esquema, el usuario no podrá ver los metadatos de dicho procedimiento almacenado.  
  
 Otro ejemplo sería que a un usuario se le concediese y denegase a la vez el permiso EXECUTE sobre un procedimiento almacenado (esto es posible a través de la pertenencia a distintos roles); en este caso, DENY tendría prioridad y el usuario no podría ver los metadatos del procedimiento almacenado.  
  
### <a name="visibility-of-subcomponent-metadata"></a>Visibilidad de los metadatos de subcomponentes  
 La visibilidad de subcomponentes, como índices, restricciones CHECK y desencadenadores, viene determinada por los permisos del elemento principal. Estos subcomponentes no disponen de permisos que puedan concederse. Por ejemplo, si a un usuario se le concede algún permiso sobre una tabla, el usuario podrá ver los metadatos de las tablas, columnas, índices, restricciones CHECK, desencadenadores y otros subcomponentes de este tipo.  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>Metadatos a los que pueden obtener acceso todos los usuarios de la base de datos  
 Algunos metadatos están disponibles para todos los usuarios de una base de datos específica. Por ejemplo, los grupos de archivos no disponen de permisos que puedan concederse; por lo tanto, no se puede conceder permiso a un usuario para ver los metadatos de un grupo de archivos. Pero cualquier usuario que pueda crear una tabla deberá poder acceder a los metadatos de un grupo de archivos para usar las cláusulas ON *filegroup* o TEXTIMAGE_ON *filegroup* de la instrucción CREATE TABLE.  
  
 Los metadatos devueltos por las funciones DB_ID() y DB_NAME() se encuentran visibles para todos los usuarios.  
  
 En la siguiente tabla se muestran las vistas de catálogo que se encuentran visibles para el rol **public** .  
  
|||  
|-|-|  
|**sys.partition_functions**|**sys.partition_range_values**|  
|**sys.partition_schemes**|**sys.data_spaces**|  
|**sys.filegroups**|**sys.destination_data_spaces**|  
|**sys.database_files**|**sys.allocation_units**|  
|**sys.partitions**|**sys.messages**|  
|**sys.schemas**|**sys.configurations**|  
|**sys.sql_dependencies**|**sys.type_assembly_usages**|  
|**sys.parameter_type_usages**|**sys.column_type_usages**|  
  
## <a name="see-also"></a>Vea también  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [EXECUTE AS &#40;cláusula de Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

