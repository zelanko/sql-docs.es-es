---
title: "Crear tabla (SQL gráfico) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe8ace1b8f8c55c14d4807514fcb1436f6966fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-sql-graph"></a>Crear tabla (gráfico SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Crea una nueva tabla de gráfico SQL como un `NODE` o un `EDGE` tabla. 
  
> [!NOTE]   
>  Para instrucciones Transact-SQL estándar, consulte [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>Argumentos  
Este documento enumera solo los argumentos pertenecen al gráfico SQL. Para una lista completa y una descripción de los argumentos admitidos, vea [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 Es el nombre de la base de datos en la que se crea la tabla. *database_name* debe especificar el nombre de una base de datos existente. Si no se especifica, *database_name* el valor predeterminado es la base de datos actual. El inicio de sesión para la conexión actual debe estar asociado con un identificador de usuario existente en la base de datos especificada por *database_name*, y el Id. de usuario debe tener permisos CREATE TABLE.  
  
 *schema_name*    
 Es el nombre del esquema al que pertenece la nueva tabla.  
  
 *table_name*    
 Es el nombre de la tabla de nodo o borde. Los nombres de tabla deben seguir las reglas para [identificadores](../../relational-databases/databases/database-identifiers.md). *table_name* puede tener un máximo de 128 caracteres, excepto para los nombres de tablas temporales locales (nombres precedidos de un solo signo de número (#)) que no puede superar los 116 caracteres.  
  
 NODO   
 Crea una tabla de nodo.

 BORDE  
 Crea una tabla irregular.  
  
## <a name="remarks"></a>Comentarios  
No se admite la creación de una tabla temporal como nodo o la tabla irregular.  

No se admite la creación de una tabla de nodo o edge como una tabla temporal.

Base de datos Stretch no se admite para el borde o nodo de tabla.

Tablas de borde o nodo no pueden ser tablas externas (no hay compatibilidad de polybase para las tablas de gráfico). 
  
 
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-a-node-table"></a>A. Crear un `NODE` tabla
 En el ejemplo siguiente se muestra cómo crear un `NODE` tabla

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Crear un `EDGE` tabla
Los ejemplos siguientes muestran cómo crear `EDGE` tablas

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (gráfico SQL)](../../t-sql/statements/insert-sql-graph.md)]  
 [Gráfico de procesamiento con SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)

