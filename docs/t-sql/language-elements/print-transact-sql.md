---
title: PRINT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: a1044fb78ebf3852a963d11607433fdb93d48007
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="print-transact-sql"></a>Imprimir-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve al cliente un mensaje definido por el usuario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_str*  
 Es una cadena de caracteres o una constante de cadena Unicode. Para obtener más información, vea [constantes &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***local_variable*  
 Es una variable de cualquier tipo de datos de caracteres válido. **@***local_variable* debe ser **char**, **nchar**, **varchar**, o **nvarchar**, o debe ser capaz de ser convierte implícitamente a esos tipos de datos.  
  
 *string_expr*  
 Es una expresión que devuelve una cadena. Puede incluir valores literales concatenados, funciones y variables. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Una cadena de mensaje puede tener una longitud de hasta 8.000 caracteres si es una cadena no Unicode, y de 4.000 caracteres si es una cadena Unicode. Las cadenas de mayor longitud se truncarán. El **varchar (max)** y **nvarchar (max)** tipos de datos se truncan en tipos de datos que no sean mayores que **varchar(8000)** y **nvarchar (4000)**.  
  
 RAISERROR también se puede utilizar para devolver mensajes. RAISERROR ofrece una serie de ventajas en comparación con PRINT:  
  
-   RAISERROR admite argumentos de sustitución en una cadena de mensaje de error con un mecanismo modelado en la función printf de la biblioteca estándar de lenguaje C.  
  
-   RAISERROR puede especificar un número de error único, un nivel de gravedad y un código de estado para el mensaje de texto.  
  
-   RAISERROR se puede utilizar para devolver mensajes definidos por el usuario y creados con el procedimiento almacenado del sistema sp_addmessage.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. Ejecutar condicionalmente una impresión (IF EXISTS)  
 En el siguiente ejemplo se utiliza la instrucción `PRINT` para devolver un mensaje de manera condicional.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. Generar y mostrar una cadena  
 En el siguiente ejemplo se convierte el resultado de la función `GETDATE` a un tipo de datos `nvarchar` y se concatena con el texto literal que devuelve `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. Ejecutar condicionalmente una impresión  
 En el siguiente ejemplo se utiliza la instrucción `PRINT` para devolver un mensaje de manera condicional.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  


