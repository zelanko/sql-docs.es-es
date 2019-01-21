---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 871d79c805451e1710dbc400914d2dace01c7eea
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143445"
---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Controla un grupo de valores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conjuntamente especifican parte del comportamiento del estándar ISO.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Sintaxis

```
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>Notas  
ANSI_DEFAULTS es una configuración del servidor que el cliente no modifica. El cliente administra su propia configuración. De manera predeterminada, esta configuración es la opuesta a la configuración del servidor. Los usuarios no deben modificar la configuración del servidor. Para cambiar el comportamiento del cliente, los usuarios deben utilizar SQL_COPT_SS_PRESERVE_CURSORS. Para más información, vea [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
Cuando se habilita (ON), esta opción habilita las opciones siguientes de ISO:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
Juntas, estas opciones SET del estándar ISO definen el entorno de procesamiento de consultas durante la sesión de trabajo del usuario, la ejecución de un desencadenador o un procedimiento almacenado. Sin embargo, estas opciones SET no son todas las necesarias para cumplir el estándar ISO.  
  
Cuando se trabaja con índices en columnas calculadas y vistas indizadas, cuatro de estos valores predeterminados (ANSI_NULLS, ANSI_PADDING, ANSI_WARNINGS y QUOTED_IDENTIFIER) deben ser ON. Estos valores predeterminados son siete opciones SET a las que se deben asignar los valores requeridos para crear y cambiar índices de columnas calculadas y vistas indizadas. Las demás opciones SET son ARITHABORT (ON), CONCAT_NULL_YIELDS_NULL (ON) y NUMERIC_ROUNDABORT (OFF). Para más información sobre las configuraciones de las opciones SET requeridas con vistas indexadas e índices en columnas calculadas, vea [Consideraciones al utilizar las instrucciones SET](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements).  
  
El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente ANSI_DEFAULTS en ON al conectarse. El controlador y el proveedor establecen a continuación CURSOR_CLOSE_ON_COMMIT e IMPLICIT_TRANSACTIONS en OFF. La opción OFF de CURSOR_CLOSE_ON_COMMIT e IMPLICIT_TRANSACTIONS se puede configurar en los orígenes de datos ODBC, los atributos de conexión ODBC o las propiedades de conexión OLE DB que se establecen en la aplicación antes de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado de ANSI_DEFAULTS es OFF para las conexiones desde aplicaciones DB-Library.  
  
Cuando se ejecuta SET ANSI_DEFAULTS, QUOTED_IDENTIFIER se establece en tiempo de análisis y se establecen las opciones siguientes en tiempo de ejecución:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se establece ANSI_DEFAULTS en ON y se usa la instrucción `DBCC USEROPTIONS` para mostrar la configuración afectada.  
  
```sql  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  

-- Display the current settings.  
DBCC USEROPTIONS;  
GO 

-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
