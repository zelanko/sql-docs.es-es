---
description: sp_execute_remote (Azure SQL Database)
title: sp_execute_remote (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1642baedb44cc6eab4474616d03abd2f429f4276
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447170"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Ejecuta una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción en un solo Azure SQL Database remoto o conjunto de bases de datos que sirven de particiones en un esquema de particionamiento horizontal.  
  
 El procedimiento almacenado forma parte de la característica de consulta elástica.  Consulte [Azure SQL Database información general sobre consultas de bases de datos elásticas](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) y [consultas de bases de datos elásticas para particionamiento (particionamiento horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ \@ data_source_name =] *datasourcename*  
 Identifica el origen de datos externo donde se ejecuta la instrucción. Vea [Create external Data SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). El origen de datos externo puede ser de tipo "RDBMS" o "SHARD_MAP_MANAGER".  
  
 [ \@ stmt =] ( *instrucción* )  
 Es una cadena Unicode que contiene una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o un lote. \@stmt debe ser una constante Unicode o una variable Unicode. No se permite utilizar expresiones Unicode más complejas, como una concatenación de dos cadenas con el operador +. Las constantes de caracteres no están permitidas. Si se especifica una constante Unicode, debe ir precedida de **N**. Por ejemplo, la constante Unicode **N ' sp_who '** es válida, pero la constante de caracteres **' sp_who '** no lo es. El tamaño de la cadena solo está limitado por la memoria disponible en el servidor de bases de datos. En los servidores de 64 bits, el tamaño de la cadena está limitado a 2 GB, el tamaño máximo de **nvarchar (Max)**.  
  
> [!NOTE]  
>  \@stmt puede contener parámetros que tengan el mismo formato que un nombre de variable, por ejemplo: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Cada parámetro incluido en \@ stmt debe tener una entrada correspondiente en la \@ lista de definición de parámetros params y en la lista de valores de parámetro.  
  
 [ \@ params =] N ' \@ *parameter_name * * data_type* [,... *n* ] '  
 Es una cadena que contiene las definiciones de todos los parámetros que se han incrustado en \@ stmt. La cadena debe ser una constante Unicode o una variable Unicode. Cada definición de parámetro se compone de un nombre de parámetro y un tipo de datos. *n* es un marcador de posición que indica definiciones de parámetros adicionales. Cada parámetro especificado en \@ stmtmust se debe definir en \@ params. Si la [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o el lote de \@ stmt no contiene parámetros, \@ no es necesario realizar ningún parámetro. El valor predeterminado de este parámetro es NULL.  
  
 [ \@ parám1 =] '*value1*'  
 Es un valor para el primer parámetro definido en la cadena de parámetros. El valor puede ser una constante Unicode o una variable Unicode. Debe haber un valor de parámetro proporcionado para cada parámetro incluido en \@ stmt. Los valores no son necesarios cuando la [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o el lote en \@ stmt no tiene parámetros.  
  
 *n*  
 Es un marcador de posición para los valores de los parámetros adicionales. Los valores solo pueden ser constantes o variables. Los valores no pueden ser expresiones más complejas como funciones ni expresiones generadas mediante operadores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o distinto de cero (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el conjunto de resultados de la primera instrucción SQL.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Observaciones  
 `sp_execute_remote` los parámetros deben especificarse en el orden específico, tal y como se describe en la sección de sintaxis anterior. Si los parámetros se escriben desordenados, se producirá un mensaje de error.  
  
 `sp_execute_remote` tiene el mismo comportamiento que [execute &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md) con respecto a los lotes y el ámbito de los nombres. La instrucción o el lote de Transact-SQL del parámetro sp_execute_remote * \@ stmt* no se compila hasta que se ejecuta la instrucción sp_execute_remote.  
  
 `sp_execute_remote` agrega una columna adicional al conjunto de resultados denominado ' $ShardName ' que contiene el nombre de la base de datos remota que creó la fila.  
  
 `sp_execute_remote` se puede usar de forma similar a [sp_executesql &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
### <a name="simple-example"></a>Ejemplo sencillo  
 En el ejemplo siguiente se crea y se ejecuta una instrucción SELECT simple en una base de datos remota.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Ejemplo con varios parámetros  
Cree una credencial con ámbito de base de datos en una base de datos de usuario y especifique las credenciales de administrador para la base de datos maestra. Cree un origen de datos externo que apunte a la base de datos maestra y especifique la credencial con ámbito de base de datos. A continuación, en el ejemplo de la base de datos de usuario, se ejecuta el `sp_set_firewall_rule` procedimiento en la base de datos maestra. El `sp_set_firewall_rule` procedimiento requiere 3 parámetros y requiere que el `@name` parámetro sea Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Ver también:

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
