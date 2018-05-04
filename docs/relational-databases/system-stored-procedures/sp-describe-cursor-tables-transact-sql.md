---
title: sp_describe_cursor_tables (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_tables_TSQL
- sp_describe_cursor_tables
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_tables
ms.assetid: 02c0f81a-54ed-4ca4-aa4f-bb7463a9ab9a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0cd7f5ad8d89097e1e08b03824fd5b95c8128637
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdescribecursortables-transact-sql"></a>sp_describe_cursor_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa acerca de los objetos o las tablas base a las que hace referencia un cursor de servidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_describe_cursor_tables   
     [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
     , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
     , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cursor_return=] *output_cursor_variable*salida  
 Es el nombre de una variable de cursor declarada que recibirá la salida del cursor. *output_cursor_variable* es **cursor**, no tiene ningún valor predeterminado y debe no ser asociado a ningún cursor en el momento en que se llama a sp_describe_cursor_tables. El cursor devuelto es un cursor desplazable, dinámico y de solo lectura.  
  
 [ @cursor_source=] {N ' | N'global' | N'variable'}  
 Especifica si el cursor del que se informa está especificado con el nombre de un cursor local, un cursor global o una variable de cursor. El parámetro es **nvarchar (30)**.  
  
 [ @cursor_identity=] N'*local_cursor_name*'  
 El nombre de un cursor creado por una instrucción DECLARE CURSOR que tiene la palabra clave LOCAL o que su valor predeterminado LOCAL. *local_cursor_name* es **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*global_cursor_name*'  
 Es el nombre de un cursor creado por una instrucción DECLARE CURSOR que tiene la palabra clave GLOBAL u obtuvo el valor predeterminado GLOBAL. *global_cursor_name* también puede ser el nombre de un cursor de servidor API abierto por una aplicación ODBC que, a continuación, dio nombre al cursor mediante una llamada a SQLSetCursorName. *global_cursor_name* es **nvarchar (128)**.  
  
 [ @cursor_identity=] N'*input_cursor_variable*'  
 Es el nombre de una variable de cursor asociada a un cursor abierto. *input_cursor_variable* es **nvarchar (128)**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="cursors-returned"></a>Cursores devueltos  
 sp_describe_cursor_tables encapsula su informe como un [!INCLUDE[tsql](../../includes/tsql-md.md)] **cursor** parámetro de salida. De esta forma, los lotes, los procedimientos almacenados y los desencadenadores de [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden trabajar con la salida de fila en fila. También significa que no se puede llamar al procedimiento directamente desde funciones de una API. El **cursor** parámetro de salida debe estar enlazado a una variable de programa, pero las API no admiten el enlace **cursor** parámetros o variables.  
  
 En la tabla siguiente se muestra el formato del cursor devuelto por sp_describe_cursor_tables.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|table owner|**sysname**|Id. de usuario del propietario de la tabla.|  
|Table_name|**sysname**|Nombre del objeto o tabla base. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los cursores de servidor siempre devuelven el objeto especificado por el usuario, no las tablas base.|  
|Optimizer_hints|**smallint**|Mapa de bits que incluye una o varias de las siguientes opciones:<br /><br /> 1 = Bloqueo de fila (ROWLOCK)<br /><br /> 4 = Bloqueo de página (PAGELOCK)<br /><br /> 8 = Bloqueo de tabla (TABLOCK)<br /><br /> 16 = Bloqueo exclusivo de tabla (TABLOCKX)<br /><br /> 32 = Bloqueo de actualización (UPDLOCK)<br /><br /> 64 = Sin bloqueo (NOLOCK)<br /><br /> 128 = Opción de primera fila rápida (FASTFIRST)<br /><br /> 4096 = Lectura de semántica repetible cuando se utiliza con DECLARE CURSOR (HOLDLOCK)<br /><br /> Cuando se especifican varias opciones, el sistema utiliza la más restrictiva. Sin embargo, sp_describe_cursor_tables muestra las marcas que se especifican en la consulta.|  
|lock_type|**smallint**|Tipo de bloqueo de desplazamiento requerido explícita o implícitamente para cada tabla base de este cursor. El valor puede ser uno de los siguientes:<br /><br /> 0 = Ninguno<br /><br /> 1 = Compartido<br /><br /> 3 = Actualización|  
|server_name|**sysname, que acepta valores null**|Nombre del servidor vinculado en el que reside la tabla. NULL cuando se utiliza OPENQUERY u OPENROWSET.|  
|Objectid|**int**|Id. de objeto de la tabla. 0 cuando se utiliza OPENQUERY u OPENROWSET.|  
|dbid|**int**|Identificador de la base de datos en la que reside la tabla. 0 cuando se utiliza OPENQUERY u OPENROWSET.|  
|dbname|**sysname**, **que aceptan valores null**|Nombre de la base de datos en la que reside la tabla. NULL cuando se utiliza OPENQUERY u OPENROWSET.|  
  
## <a name="remarks"></a>Comentarios  
 sp_describe_cursor_tables describe las tablas base a las que hace referencia un cursor de servidor. Utilice sp_describe_cursor_columns para obtener una descripción de los atributos del conjunto de resultados devuelto por el cursor. Para obtener una descripción de las características globales del cursor, como por ejemplo sus posibilidades de desplazamiento y actualización, use sp_describe_cursor. Para obtener un informe de la [!INCLUDE[tsql](../../includes/tsql-md.md)] cursores de servidor que están visibles en la conexión, use sp_cursor_list.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se abre un cursor global y se utiliza `sp_describe_cursor_tables` para informar acerca de las tablas a las que hace referencia el cursor.  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
  
OPEN abc;  
GO  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_tables.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_tables into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_tables  
      @cursor_return = @Report OUTPUT,  
      @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_tables output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_tables.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Cursores](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
