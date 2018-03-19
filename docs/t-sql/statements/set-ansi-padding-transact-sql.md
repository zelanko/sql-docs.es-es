---
title: SET ANSI_PADDING (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 532df95a03b15d545c682d30b3b4d68e10ea5913
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Controla el modo en que la columna almacena valores más cortos que el tamaño definido y el modo en que almacena valores con espacios en blanco finales en datos de tipo **char**, **varchar**, **binary**y **varbinary** .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis
  
```
-- Syntax for SQL Server

SET ANSI_PADDING { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_PADDING ON
```

## <a name="remarks"></a>Notas  
 Las columnas definidas con tipos de datos **char**, **varchar**, **binary** y **varbinary** tienen un tamaño definido.  
  
 Esta opción solo afecta a la definición de nuevas columnas. Una vez creada la columna, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena los valores de acuerdo con la opción establecida en el momento de su creación. Las columnas existentes no se ven afectadas por los cambios posteriores de esta opción.  
  
> [!NOTE]  
>  Se recomienda que ANSI_PADDING siempre se establezca ON.  
  
 En esta tabla se muestran los efectos del parámetro SET ANSI_PADDING cuando se insertan valores en columnas con los tipos de datos **char**, **varchar**, **binary** y **varbinary**.  
  
|Configuración|char(*n*) NOT NULL o binary(*n*) NOT NULL|char(*n*) NULL o binary(*n*) NULL|varchar(*n*) o varbinary(*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|Rellena el valor original (con espacios en blanco finales en las columnas **char** y con ceros finales en las columnas **binary**) hasta completar la longitud de la columna.|Sigue las mismas reglas que para **char(***n***)** o **binary(***n***)** NOT NULL cuando SET ANSI_PADDING está en ON.|Los espacios en blanco finales en los valores de caracteres insertados en las columnas **varchar** no se recortan. Los ceros a la derecha en los valores binarios insertados en las columnas **varbinary** no se recortan. Los valores no se rellenan hasta completar la longitud de la columna.|  
|OFF|Rellena el valor original (con espacios en blanco finales en las columnas **char** y con ceros finales en las columnas **binary**) hasta completar la longitud de la columna.|Sigue las mismas reglas que para **varchar** o **varbinary** cuando SET ANSI_PADDING está en OFF.|Los espacios en blanco finales en los valores de carácter insertados en una columna **varchar** se recortan. Los ceros a la derecha en los valores binarios insertados en una columna **varbinary** se recortan.|  
  
> [!NOTE]  
>  Cuando se rellenan las columnas **char**, se incluyen espacios en blanco y en las columnas **binary** se incluyen ceros. Cuando se recortan las columnas **char**, se recortan los espacios en blanco finales; en las columnas **binary** se recortan los ceros finales.  
  
 SET ANSI_PADDING también debe ser ON al crear o cambiar índices en columnas calculadas o vistas indizadas. Para obtener más información sobre las configuraciones de las opciones SET requeridas con vistas indizadas e índices en columnas calculadas, vea el apartado "Considerations When You Use the SET Statements" (Consideraciones al utilizar las instrucciones SET) en [SET Statements &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md) (Instrucciones SET (Transact-SQL).  
  
 El valor predeterminado de SET ANSI_PADDING es ON. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente ANSI_PADDING en ON al conectarse. Esta opción se puede configurar en los orígenes de datos ODBC, en los atributos de conexión de ODBC o en las propiedades de conexión OLE DB establecidas en la aplicación antes de conectar. SET ANSI_PADDING tiene como opción predeterminada OFF en las conexiones desde aplicaciones DB-Library.  
  
 La opción SET ANSI_PADDING no afecta a los tipos de datos **nchar**, **nvarchar**, **ntext**, **text**, **image**, **varbinary(max)**, **varchar(max)** y **nvarchar(max)**. Siempre muestran el comportamiento SET ANSI_PADDING ON. Esto significa que no se recortan los espacios y ceros a la derecha.  
  
 Cuando SET ANSI_DEFAULTS es ON, se habilita SET ANSI_PADDING.  
  
 La configuración de SET ANSI_PADDING se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Para ver la configuración actual de este valor, ejecute la consulta siguiente.  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra cómo afecta esta opción a cada uno de los tipos de datos.  
  
```  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
  
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>Ver también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
