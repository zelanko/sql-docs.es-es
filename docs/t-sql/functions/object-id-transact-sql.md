---
title: OBJECT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
caps.latest.revision: 63
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6b9a84b092790a11f9efb5bef8e433a11d0afdd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055232"
---
# <a name="objectid-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el número de Id. del objeto de base de datos de un objeto de ámbito de esquema.  
  
> [!IMPORTANT]  
>  Los objetos que no están en el ámbito del esquema, por ejemplo los desencadenadores DDL, no se pueden consultar utilizando OBJECT_ID. En el caso de objetos que no están en la vista de catálogo [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md), debe obtener los números de identificación de objeto mediante consultas realizadas a la vista de catálogo correspondiente. Por ejemplo, para devolver el número de identificación de objeto de un desencadenador DDL, use `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *object_name* **'**  
 Es el objeto que va a utilizarse. *object_name* es **varchar** o **nvarchar**. Si *object_name* es **varchar**, se convierte implícitamente a **nvarchar**. Especificar los nombres de la base de datos y del esquema es opcional.  
  
 **'** *object_type* **'**  
 Es el tipo de objeto de ámbito del esquema. *object_type* es **varchar** o **nvarchar**. Si *object_type* es **varchar**, se convierte implícitamente en **nvarchar**. Para ver una lista de tipos de objeto, eche un vistazo a la columna **type** en [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="exceptions"></a>Excepciones  
 Para un índice espacial, OBJECT_ID devuelve NULL.  
  
 Devuelve NULL si se produce un error.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECT_ID, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Notas  
 Cuando el parámetro de una función del sistema es opcional, se asumen la base de datos, el equipo host, el usuario del servidor o el usuario de la base de datos actuales. Las funciones integradas siempre deben ir seguidas de paréntesis.  
  
 Cuando se especifica un nombre de tabla temporal, el nombre de base de datos debe ir antes del nombre de tabla temporal, a menos que la base de datos temporal sea **tempdb**. Por ejemplo: `SELECT OBJECT_ID('tempdb..#mytemptable')`.  
  
 Las funciones del sistema se pueden usar en la lista de selección, en la cláusula WHERE y en cualquier lugar donde se permita una expresión. Para más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) y [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. Devolver el identificador de objeto de un objeto especificado  
 En este ejemplo se devuelve el Id. de objeto para la tabla `Production.WorkOrder` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. Comprobar la existencia de un objeto  
 En el ejemplo siguiente se comprueba la existencia de una tabla especificada comprobando si la tabla tiene un identificador de objeto. Si la tabla existe, se elimina. Si la tabla no existe, la instrucción `DROP TABLE` no se ejecuta.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-objectid-to-specify-the-value-of-a-system-function-parameter"></a>C. Usar OBJECT_ID para especificar el valor de un parámetro de función del sistema  
 En este ejemplo se devuelve información de todos los índices y particiones de la tabla `Person.Address` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] con la función [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).  
  
> [!IMPORTANT]  
>  Cuando utilice las funciones DB_ID y OBJECT_ID de [!INCLUDE[tsql](../../includes/tsql-md.md)] para devolver un valor de parámetro, asegúrese de que siempre se devuelva un Id. válido. Si el nombre de objeto o base de datos no se puede encontrar, por ejemplo, cuando no existe o se ha escrito incorrectamente, las dos funciones devolverán NULL. La función **sys.dm_db_index_operational_stats** interpreta NULL como un valor de carácter comodín que especifica todas las bases de datos o todos los objetos. Puesto que ésta puede ser una operación accidental, los ejemplos de esta sección demuestran una forma segura para determinar los Id. de bases de datos y objetos.  
  
```  
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D. Devolver el identificador de objeto de un objeto especificado  
 En este ejemplo se devuelve el Id. de objeto para la tabla `FactFinance` en la base de datos [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```  
SELECT OBJECT_ID('AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

