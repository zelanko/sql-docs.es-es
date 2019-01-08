---
title: Sys.dm_sql_referencing_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf1f5b633b432d24ea143d857dcd7fbdf72968fd
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204544"
---
# <a name="sysdmsqlreferencingentities-transact-sql"></a>sys.dm_sql_referencing_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada entidad en la base de datos actual que hace referencia por nombre a otra entidad definida por el usuario. Se crea una dependencia entre dos entidades cuando una entidad, llamada la *hace referencia a entidad*, aparece por nombre en una expresión SQL persistente de otra entidad, llamada la *que hacen referencia a entidad*. Por ejemplo, si un tipo definido por el usuario (UDT) se especifica como la entidad a la que se hace referencia, esta función devuelve cada entidad definida por el usuario que hace referencia a ese tipo por nombre en su definición. La función no devuelve las entidades en otras bases de datos que pueden hacer referencia a la entidad especificada. Se puede ejecutar esta función en el contexto de la base de datos maestra para devolver un desencadenador DDL de nivel de servidor como una entidad que hace la referencia.  
  
 Puede usar esta función de administración dinámica para informar sobre los tipos siguientes de entidades de la base de datos actual que hacen referencia a la entidad especificada:  
  
-   Entidades enlazadas o no a un esquema.  
  
-   Desencadenadores DLL de nivel de base de datos   
  
-   Desencadenadores DDL de nivel de servidor   
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name.referenced*_*entity_name*  
 Es el nombre de la entidad a la que se hace referencia.  
  
 *schema_name* es necesaria excepto cuando la clase que se hace referencia es PARTITION_FUNCTION.  
  
 *schema_name.referenced_entity_name* es **nvarchar (517)**.  
  
 *< Referenced_class >* :: = {objeto | TIPO | XML_SCHEMA_COLLECTION | PARTITION_FUNCTION}  
 Es la clase de la entidad a la que se hace referencia. Solo se puede especificar una clase por instrucción.  
  
 *< referenced_class >* es **nvarchar**(60).  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|Esquema al que pertenece la entidad que hace la referencia. Acepta valores NULL.<br /><br /> NULL para desencadenadores DDL de nivel de base de datos y nivel de servidor.|  
|referencing_entity_name|**sysname**|Nombre de la entidad que hace la referencia. No admite valores NULL.|  
|referencing_id|**int**|Identificador de la entidad que hace la referencia. No admite valores NULL.|  
|referencing_class|**tinyint**|Clase de la entidad que hace la referencia. No admite valores NULL.<br /><br /> 1 = Objeto<br /><br /> 12 = Desencadenador DLL de nivel de base de datos <br /><br /> 13 = Desencadenador DDL de nivel de servidor |  
|referencing_class_desc|**nvarchar(60)**|Descripción de la clase de entidad de referencia.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|Indica que la resolución del identificador de la entidad a la que se hace referencia se realiza en tiempo de ejecución porque depende del esquema del autor de la llamada.<br /><br /> 1 = La entidad que hace la referencia tiene el potencial para hacer referencia a la entidad; sin embargo, la resolución del identificador de la entidad depende del autor de la llamada y no se puede determinar. Esto solo se produce para las referencias no enlazadas a un esquema a un procedimiento almacenado, un procedimiento almacenado extendido o una función definida por el usuario llamada en una instrucción EXECUTE.<br /><br /> 0 = La entidad a la que se hace referencia no depende del autor de la llamada.|  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve un conjunto de resultados vacío si se da alguna de las condiciones siguientes:  
  
-   Se especifica un objeto del sistema.  
  
-   La entidad especificada no existe en la base de datos actual.  
  
-   La entidad especificada no hace referencia a ninguna entidad.  
  
-   Se pasó un parámetro no válido.  
  
 Devuelve un error si la entidad especificada a la que se hace referencia es un procedimiento almacenado numerado.  
  
## <a name="remarks"></a>Comentarios  
 La tabla siguiente enumera los tipos de entidades para las que se crea y mantiene la información de dependencia. La información de dependencia no se crea ni mantiene para reglas, valores predeterminados, tablas temporales, procedimientos almacenados temporales u objetos del sistema.  
  
|Tipo de entidad|Entidad que hace la referencia|Entidad a la que se hace referencia|  
|-----------------|------------------------|-----------------------|  
|Table|Sí*|Sí|  
|Ver|Sí|Sí|  
|Procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)]**|Sí|Sí|  
|procedimiento almacenado CLR|No|Sí|  
|Función definida por el usuario de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|Sí|  
|Función CLR definida por el usuario|No|Sí|  
|Desencadenador CLR (DML y DDL)|No|No|  
|Desencadenador DML de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Desencadenador DDL de nivel de base de datos de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Desencadenador DDL de nivel de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Procedimientos almacenados extendidos|No|Sí|  
|Cola|No|Sí|  
|Synonym (Sinónimo)|No|Sí|  
|Tipo (tipo CLR y alias definido por el usuario)|No|Sí|  
|Colección de esquemas XML|No|Sí|  
|Función de partición|No|Sí|  
  
 \* Una tabla se realiza un seguimiento como una entidad de referencia solo cuando hace referencia a un [!INCLUDE[tsql](../../includes/tsql-md.md)] módulo, tipo definido por el usuario o la colección de esquemas XML en la definición de una columna calculada, restricción CHECK o restricción predeterminada.  
  
 ** No se realiza el seguimiento de los procedimientos almacenados numerados con un valor entero mayor que 1 como la entidad que hace referencia ni como la entidad a la que se hace referencia.  
  
## <a name="permissions"></a>Permisos  
  
### <a name="includesskatmaiincludessskatmai-mdmd---includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   Requiere el permiso CONTROL en el objeto al que se hace referencia. Cuando la entidad a la que se hace referencia es una función de partición, se requiere el permiso CONTROL en la base de datos.  
  
-   Requiere el permiso SELECT en sys.dm_sql_referencing_entities. De forma predeterminada, se concede el permiso SELECT a public.  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   No requiere permisos en el objeto al que se hace referencia. Se pueden devolver resultados parciales si el usuario tiene el permiso VIEW DEFINITION solo en algunas entidades de referencia.  
  
-   Requiere el permiso VIEW DEFINITION en el objeto si la entidad de referencia es un objeto.  
  
-   Requiere el permiso VIEW DEFINITION en la base de datos si la entidad de referencia es un desencadenador DDL de base de datos.  
  
-   Requiere el permiso VIEW ANY DEFINITION en el servidor si la entidad de referencia es un desencadenador DDL de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. Devolver las entidades que hacen referencia a una entidad determinada  
 El ejemplo siguiente devuelve las entidades en la base de datos actual que hacen referencia a la tabla especificada.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>b. Devolver las entidades que hacen referencia a un tipo determinado  
 El ejemplo siguiente devuelve las entidades que hacen referencia al tipo de alias `dbo.Flag`. El conjunto de resultados muestra que dos procedimientos almacenados utilizan este tipo. El `dbo.Flag` tipo también se utiliza en la definición de varias columnas en el `HumanResources.Employee` tabla; sin embargo, dado que el tipo no está en la definición de una columna calculada, restricción CHECK o restricción DEFAULT en la tabla, se devolverá ninguna fila para el `HumanResources.Employee`tabla.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>Vea también  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
