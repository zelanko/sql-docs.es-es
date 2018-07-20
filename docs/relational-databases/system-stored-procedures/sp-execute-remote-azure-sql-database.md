---
title: sp_execute_remote (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
caps.latest.revision: 17
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 319eee940c5f5d90d6cfe9442c66f506670c26a0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082577"
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Ejecuta un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción en un único de Azure SQL Database remota o un conjunto de bases de datos que actúan como particiones en un esquema de partición horizontal.  
  
 El procedimiento almacenado forma parte de la característica de consulta elástica.  Consulte [información general sobre la consulta de bases de datos elásticas de Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) y [consultas de bases de datos elásticas para particionamiento (partición horizontal)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
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
 [ \@data_source_name =] *datasourcename*  
 Identifica el origen de datos externo que se ejecuta la instrucción. Consulte [crear origen de datos externo &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). El origen de datos externo puede ser de tipo "RDBMS" o "SHARD_MAP_MANAGER".  
  
 [ \@stmt =] *instrucción*  
 Es una cadena Unicode que contiene un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o lote. \@stmt debe ser una constante Unicode o una variable Unicode. No se permite utilizar expresiones Unicode más complejas, como una concatenación de dos cadenas con el operador +. Las constantes de caracteres no están permitidas. Si se especifica una constante Unicode, deben ir precedido por un **N**. Por ejemplo, la constante Unicode **N 'sp_who'** es válido, pero la constante de caracteres **'sp_who'** no es. El tamaño de la cadena solo está limitado por la memoria disponible en el servidor de bases de datos. En los servidores de 64 bits, el tamaño de la cadena se limita a 2 GB, el tamaño máximo de **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt puede contener parámetros que tengan el mismo formato que un nombre de variable, por ejemplo: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Cada parámetro incluido en \@stmt debe tener una entrada correspondiente tanto en el \@params lista de definiciones de parámetro y el parámetro de la lista de valores.  
  
 [ \@params =] N'\@*parameter_name ** data_type* [,... *n* ] '  
 Es una cadena que contiene las definiciones de todos los parámetros que se han incrustado en \@stmt. La cadena debe ser una constante Unicode o una variable Unicode. Cada definición de parámetro se compone de un nombre de parámetro y un tipo de datos. *n* es un marcador de posición que indica definiciones de parámetros adicionales. Todos los parámetros especificados en \@stmtmust definirse en \@params. Si el [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o lote en \@stmt no contiene parámetros, \@params no es necesario. El valor predeterminado de este parámetro es NULL.  
  
 [ \@param1 =] '*value1*'  
 Es un valor para el primer parámetro definido en la cadena de parámetros. El valor puede ser una constante Unicode o una variable Unicode. Debe haber un valor de parámetro proporcionado para cada parámetro incluido en \@stmt. Los valores no son necesarios cuando el [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o lote en \@stmt no tiene ningún parámetro.  
  
 *n*  
 Es un marcador de posición para los valores de los parámetros adicionales. Los valores solo pueden ser constantes o variables. Los valores no pueden ser expresiones más complejas como funciones ni expresiones generadas mediante operadores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o distinto de cero (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el conjunto de resultados de la primera instrucción SQL.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Notas  
 `sp_execute_remote` los parámetros deben especificarse en el orden específico, como se describe en la sección de sintaxis anterior. Si los parámetros se escriben desordenados, se producirá un mensaje de error.  
  
 `sp_execute_remote` tiene el mismo comportamiento que [EXECUTE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md) con respecto a los lotes y el ámbito de nombres. La instrucción Transact-SQL o el lote en el sp_execute_remote  *\@stmt* parámetro no se compila hasta que se ejecuta la instrucción sp_execute_remote.  
  
 `sp_execute_remote` Agrega una columna adicional para el conjunto de resultados llamado '$ShardName' que contiene el nombre de la base de datos remoto que generó la fila.  
  
 `sp_execute_remote` puede utilizarse de forma similar a [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
### <a name="simple-example"></a>Ejemplo sencillo  
 El ejemplo siguiente se crea y ejecuta una instrucción SELECT simple en una base de datos remota.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Ejemplo con varios parámetros  
Crear una credencial de ámbito de base de datos en una base de datos de usuario, especificar las credenciales de administrador para la base de datos maestra. Crear un origen de datos externo que apunta a la base de datos maestra y especificar la credencial con ámbito de base de datos. A continuación, ejecuta el siguiente ejemplo en la base de datos de usuario, el `sp_set_firewall_rule` procedimiento en la base de datos maestra. El `sp_set_firewall_rule` procedimiento requiere 3 parámetros y requiere la `@name` parámetro sea de Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Ver también:

[CREAR BASE DE DATOS CON ÁMBITO DE CREDENCIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[Crear origen de datos externo (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
