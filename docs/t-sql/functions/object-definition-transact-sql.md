---
title: OBJECT_DEFINITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 437b69ca7a8c06a4f19b5c4c76e3c7327d978960
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784356"
---
# <a name="object_definition-transact-sql"></a>OBJECT_DEFINITION (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve el texto de origen de [!INCLUDE[tsql](../../includes/tsql-md.md)] para la definición de un objeto especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OBJECT_DEFINITION ( object_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el identificador del objeto que se va a utilizar. *object_id* es **int** y se considera que representa un objeto del contexto de la base de datos actual.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **nvarchar(max)**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECT_DEFINITION, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Observaciones  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] da por hecho que *object_id* se encuentra en el contexto de la base de datos actual. La intercalación de la definición del objeto siempre coincide con la del contexto de la base de datos que realiza la llamada.  
  
 OBJECT_DEFINITION se aplica a los siguientes tipos de objeto:  
  
-   C = Restricción CHECK  
  
-   D = Default (restricción o independiente)  
  
-   P = Procedimiento almacenado de SQL  
  
-   FN = Función escalar de SQL  
  
-   R = Regla  
  
-   RF = Procedimiento de filtro de replicación  
  
-   TR = Desencadenador SQL (desencadenador DML en el ámbito del esquema o desencadenador DDL en el ámbito de la base de datos o del servidor)  
  
-   IF = Función SQL insertada con valores de tabla  
  
-   TF = Función con valores de tabla de SQL  
  
-   V = Vista  
  
## <a name="permissions"></a>Permisos  
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
  
## <a name="see-also"></a>Consulte también  
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
  
