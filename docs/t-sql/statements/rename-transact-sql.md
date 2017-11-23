---
title: RENAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/20/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: "15"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ee5395145b72108b63256a7e3742eca6a9289e06
ms.sourcegitcommit: ef1fa818beea435f58986af3379853dc28f5efd8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Cambia el nombre de una tabla creada por el usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Cambia el nombre de una tabla creada por el usuario o una base de datos en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
> [!NOTE]  
>  Para cambiar el nombre de una base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_renamedb &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md). Para cambiar el nombre de una base de datos en la base de datos de SQL Azure, use la [ALTER DATABASE (base de datos de SQL Azure)](/statements/alter-database-azure-sql-database.md) instrucción. 
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [ :: ]  [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 CAMBIAR EL NOMBRE DE OBJETO [:]   
          [[*database_name* . [ *schema_name* ]. ] | [ *schema_name* . []]*table_name* TO *new_table_name*  
 **SE APLICA A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Cambiar el nombre de una tabla definida por el usuario. Especificar la tabla que se va a cambiar con un uno, dos o nombre de tres partes.    Especifique la nueva tabla *new_table_name* como un nombre de una sola parte.  
  
 CAMBIAR EL NOMBRE DE BASE DE DATOS [:]   
          [ *database_name* TO *new_database_name*  
 **SE APLICA A:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Cambiar el nombre de una base de datos definido por el usuario de *database_name* a *new_database_name*.  No se puede cambiar el nombre de una base de datos a cualquiera de esos [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]nombres de base de datos reservados:  
  
-   maestra  
  
-   model  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   : DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este comando que necesita este permiso:  
  
-   **ALTER** permiso en la tabla  
   
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>No se puede cambiar el nombre de una tabla externa, índices o vistas
No se puede cambiar el nombre de una tabla externa, índices o vistas. En lugar de cambiar el nombre, puede quitar la tabla externa, el índice o la vista y, a continuación, volver a crearla con el nuevo nombre.

### <a name="cannot-rename-a-table-in-use"></a>No se puede cambiar el nombre de una tabla en uso  
 No se puede cambiar el nombre una tabla o una base de datos mientras está en uso. Cambiar el nombre de una tabla, requiere un bloqueo exclusivo en la tabla. Si la tabla está en uso, debe finalizar las sesiones que usan la tabla. Puede utilizar el comando KILL para terminar una sesión. Utilice KILL con precaución, ya que cuando se termina una sesión de cualquier trabajo no confirmado se revertirá. Las sesiones en el almacén de datos de SQL llevan el prefijo 'SID'. Debe incluir esto y el número de sesión al invocar el comando KILL. Este ejemplo muestra una lista de sesiones activas o inactivas y, a continuación, finaliza la sesión 'SID1234'.  
  
### <a name="views-are-not-updated"></a>No se actualizan las vistas  
 Al cambiar el nombre de una base de datos, todas las vistas que usan el nombre de la base de datos anterior ya no serán válidas. Esto se aplica a las vistas, tanto dentro como fuera de la base de datos. Por ejemplo, si se cambia el nombre de la base de datos de ventas, una vista que contiene `SELECT * FROM Sales.dbo.table1` dejarán de ser válidos. Para resolver este problema, puede evitar el uso de nombres de tres partes en vistas o actualizar las vistas para hacer referencia al nombre de la base de datos nueva.  
  
 Al cambiar el nombre de una tabla, las vistas no se actualizan para que haga referencia el nuevo nombre de tabla. Cada vista, ya sea dentro o fuera de la base de datos, que hace referencia el nombre de la tabla anterior dejará de ser válida. Para resolver este problema, puede actualizar cada vista para hacer referencia al nombre de la tabla nueva.  
  
## <a name="locking"></a>Bloqueo  
 Cambiar el nombre de una tabla tiene un bloqueo compartido en el objeto de base de datos, un bloqueo compartido en el objeto de esquema y un bloqueo exclusivo en la tabla.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-rename-a-database"></a>A. Cambiar el nombre de una base de datos  
 **Se aplica a:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] sólo  
  
 Este ejemplo cambia el nombre de la base de datos definido por el usuario AdWorks a AdWorks2.  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 Al cambiar el nombre de una tabla, se actualizan todos los objetos y propiedades asociadas a la tabla para hacer referencia al nombre de la tabla nueva. Por ejemplo, tabla definiciones, índices, restricciones y se actualizan permisos. No se actualizan las vistas.  
  
### <a name="b-rename-a-table"></a>B. Cambiar de nombre una tabla  
 **SE APLICA A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Este ejemplo cambia el nombre de la tabla Customer para Customer1.  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 Al cambiar el nombre de una tabla, se actualizan todos los objetos y propiedades asociadas a la tabla para hacer referencia al nombre de la tabla nueva. Por ejemplo, tabla definiciones, índices, restricciones y se actualizan permisos. No se actualizan las vistas.  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. Mover una tabla a un esquema diferente  
 **SE APLICA A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Si su intención es mover el objeto a un esquema diferente, use [ALTER SCHEMA &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-schema-transact-sql.md). Por ejemplo, mueve el elemento de la tabla desde el esquema de producto al esquema dbo.  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. Terminar sesiones antes de cambiar el nombre de una tabla  
 **SE APLICA A:**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)],  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Es importante recordar que no se puede cambiar el nombre una tabla mientras está en uso. Un cambio de nombre de una tabla requiere un bloqueo exclusivo en la tabla. Si la tabla está en uso, debe finalizar la sesión mediante la tabla. Puede utilizar el comando KILL para terminar una sesión. Utilice KILL con precaución, ya que cuando se termina una sesión de cualquier trabajo no confirmado se revertirá. Las sesiones en el almacén de datos de SQL llevan el prefijo 'SID'. Debe incluir esto y el número de sesión al invocar el comando KILL. Este ejemplo muestra una lista de sesiones activas o inactivas y, a continuación, finaliza la sesión 'SID1234'.  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
