---
title: SET ANSI_WARNINGS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_WARNINGS
- ANSI_WARNINGS_TSQL
- ANSI_WARNINGS
- SET_ANSI_WARNINGS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], ISO standard behavior
- warnings [SQL Server]
- SET ANSI_WARNINGS statement
- ANSI_WARNINGS option
ms.assetid: f82aaab0-334f-427b-89b0-de4af596b4fa
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feee804808cb9ba8d6e3dd97fb512a3a73301e17
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica el comportamiento estándar de ISO para diversas condiciones de error.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ANSI_WARNINGS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_WARNINGS ON;  
```  
  
## <a name="remarks"></a>Comentarios  
 SET ANSI_WARNINGS afecta a las condiciones siguientes:  
  
-   Si es ON y aparecen valores NULL en funciones de agregado, como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP o COUNT, se genera un mensaje de advertencia. Si es OFF, no se genera ninguna advertencia.  
  
-   Si es ON, los errores de división por cero y desbordamiento aritmético hacen que la instrucción se revierta y que se genere un mensaje de error. Si es OFF, los errores de división por cero y de desbordamiento aritmético hacen que se devuelvan valores NULL. El comportamiento en el que un error de división por cero o desbordamiento aritmético provoca que se devuelvan valores null se produce si se intenta una INSERCIÓN o actualización un **caracteres**, Unicode, o **binario** columna en la que la longitud del nuevo valor excede el tamaño máximo de la columna. Si SET ANSI_WARNINGS es ON, la instrucción INSERT o UPDATE se cancela tal y como especifica el estándar ISO. No se tienen en cuenta los espacios en blanco a la derecha en las columnas de carácter ni los valores NULL a la derecha en las columnas binarias. Cuando es OFF, los datos se truncan para ajustarlos al tamaño de la columna y la instrucción se ejecuta correctamente.  
  
    > [!NOTE]  
    >  Cuando se produce el truncamiento en alguna conversión a o desde **binario** o **varbinary** datos, ningún error ni advertencia se emite, sin tener en cuenta las opciones SET.  
  
    > [!NOTE]  
    >  No se respeta ANSI_WARNINGS al pasar parámetros de un procedimiento almacenado, una función definida por el usuario o al declarar y establecer variables en una instrucción de lote. Por ejemplo, si una variable se define como **char (3)**y, a continuación, establece en un valor mayor que tres caracteres, se truncan los datos para el tamaño definido y la INSERCIÓN o instrucción de actualización se realiza correctamente.  
  
 Se puede utilizar la opción user options de sp_configure para establecer el valor predeterminado de ANSI_WARNINGS en todas las conexiones al servidor. Para obtener más información, vea [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 SET ANSI_WARNINGS también debe ser ON al crear o manipular índices en columnas calculadas o vistas indizadas. Si SET ANSI_WARNINGS es OFF, las instrucciones CREATE, UPDATE, INSERT y DELETE provocarán errores en tablas con índices en columnas calculadas y vistas indizadas. Para obtener más información acerca de las configuraciones de opción de SET requeridas con vistas indizadas e índices en columnas calculadas, vea "Consideraciones cuando se Use las instrucciones SET" en [instrucciones SET &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye la opción de base de datos ANSI_WARNINGS. Es equivalente a SET ANSI_WARNINGS. Cuando SET ANSI_WARNINGS es ON, se producen errores o advertencias si hay división por cero, cadenas demasiado largas para la columna correspondiente de la base de datos y otras situaciones similares. Cuando SET ANSI_WARNINGS es OFF, no se generan tales errores y advertencias. La opción predeterminada en la base de datos model para SET ANSI_WARNINGS es OFF. Si no se especifica, se aplica la opción de ANSI_WARNINGS. Si SET ANSI_WARNINGS es OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el valor de la columna is_ansi_warnings_on de la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
 ANSI_WARNINGS debe establecerse en ON para ejecutar consultas distribuidas.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente ANSI_WARNINGS en ON al conectarse. Esta opción se puede configurar en los orígenes de datos ODBC, en los atributos de conexión de ODBC, establecidos en la aplicación antes de conectar. El valor predeterminado de SET ANSI_WARNINGS es OFF en las conexiones desde aplicaciones DB-Library.  
  
 Cuando SET ANSI_DEFAULTS es ON, se habilita SET ANSI_WARNINGS.  
  
 La opción SET ANSI_WARNINGS se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Si SET ARITHABORT o SET ARITHIGNORE es OFF y SET ANSI_WARNINGS es ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error cuando haya errores de división por cero o desbordamiento.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestran las tres situaciones mencionadas anteriormente con SET ANSI_WARNINGS en ON y en OFF.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE T1   
(  
   a int,   
   b int NULL,   
   c varchar(20)  
);  
GO  
  
SET NOCOUNT ON;  
  
INSERT INTO T1   
VALUES (1, NULL, '')   
      ,(1, 0, '')  
      ,(2, 1, '')  
      ,(2, 2, '');  
  
SET NOCOUNT OFF;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS ON';  
GO  
  
SET ANSI_WARNINGS ON;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (3, 3, 'Text string longer than 20 characters');  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS OFF';  
GO  
SET ANSI_WARNINGS OFF;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (4, 4, 'Text string longer than 20 characters');  
GO  
SELECT a, b, c   
FROM T1  
WHERE a = 4;  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
DROP TABLE T1  
```  
  
## <a name="see-also"></a>Vea también  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

