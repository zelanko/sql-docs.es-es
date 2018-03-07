---
title: OBJECT_DEFINITION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_DEFINITION_TSQL
- OBJECT_DEFINITION
dev_langs:
- TSQL
helpviewer_keywords:
- viewing source text
- source text [SQL Server]
- displaying source text
- OBJECT_DEFINITION function
ms.assetid: 2ac837c7-eca9-4d29-b06e-72e30450c68d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98d50823e1f84060b94a8956b3ed885fc15cd593
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="objectdefinition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el texto de origen de [!INCLUDE[tsql](../../includes/tsql-md.md)] para la definición de un objeto especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el identificador del objeto que se va a utilizar. *object_id* es **int**y considera que representa un objeto en el contexto de base de datos actual.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECT_DEFINITION, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentarios  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se da por supuesto que *object_id* está en el contexto de base de datos actual. La intercalación de la definición del objeto siempre coincide con la del contexto de la base de datos que realiza la llamada.  
  
 OBJECT_DEFINITION se aplica a los siguientes tipos de objeto:  
  
-   C = Restricción CHECK  
  
-   D. = valor predeterminado (restricción o independiente)  
  
-   P = procedimiento almacenado de SQL  
  
-   FN = Función escalar de SQL  
  
-   R = Regla  
  
-   RF = procedimiento de filtro de replicación  
  
-   TR = Desencadenador SQL (desencadenador DML en el ámbito del esquema o desencadenador DDL en el ámbito de la base de datos o del servidor)  
  
-   IF = Función SQL insertada con valores de tabla  
  
-   TF = Función con valores de tabla de SQL  
  
-   V = Vista  
  
## <a name="permissions"></a>Permissions  
 Las definiciones de los objetos del sistema están visibles públicamente. La definición de los objetos de usuario está visible para el propietario del objeto o los receptores de los permisos siguientes: ALTER, CONTROL, TAKE OWNERSHIP o VIEW DEFINITION. Estos permisos corresponden implícitamente a los miembros de los roles fijos de base de datos **db_owner**, **db_ddladmin**y **db_securityadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-source-text-of-a-user-defined-object"></a>A. Devolver el texto de origen de un objeto definido por el usuario  
 En el ejemplo siguiente se devuelve la definición de un desencadenador definido por el usuario, `uAddress`, en el esquema `Person`. Se utiliza la función integrada `OBJECT_ID` para devolver el Id. de objeto del desencadenador a la instrucción `OBJECT_DEFINITION`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.uAddress')) AS [Trigger Definition];   
GO  
```  
  
### <a name="b-returning-the-source-text-of-a-system-object"></a>B. Devolver el texto de origen de un objeto del sistema  
 En el ejemplo siguiente se devuelve la definición del procedimiento almacenado del sistema `sys.sp_columns`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'sys.sp_columns')) AS [Object Definition];  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [Object_id &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  
