---
title: SET ANSI_DEFAULTS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 170fb1f5a95b9f6fe4fbe596906595475175b1a2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
  
SET ANSI_DEFAULTS ON;  
```  
  
## <a name="remarks"></a>Comentarios  
 SET ANSI_DEFAULTS es una configuración del servidor que el cliente no modifica. El cliente administra su propia configuración. De manera predeterminada, esta configuración es la opuesta a la configuración del servidor. Los usuarios no deben modificar la configuración del servidor. Para cambiar el comportamiento del cliente, los usuarios deben utilizar SQL_COPT_SS_PRESERVE_CURSORS. Para obtener más información, consulte [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Cuando se habilita (ON), esta opción habilita las opciones siguientes de ISO:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
 Juntas, estas opciones SET del estándar ISO definen el entorno de procesamiento de consultas durante la sesión de trabajo del usuario, la ejecución de un desencadenador o un procedimiento almacenado. Sin embargo, estas opciones SET no son todas las necesarias para cumplir el estándar ISO.  
  
 Cuando se trabaja con índices en columnas calculadas y vistas indizadas, cuatro de estos valores predeterminados (ANSI_NULLS, ANSI_PADDING, ANSI_WARNINGS y QUOTED_IDENTIFIER) deben ser ON. Estos valores predeterminados son siete opciones SET a las que se deben asignar los valores requeridos para crear y cambiar índices de columnas calculadas y vistas indizadas. Las demás opciones SET son ARITHABORT (ON), CONCAT_NULL_YIELDS_NULL (ON) y NUMERIC_ROUNDABORT (OFF). Para obtener más información acerca de las configuraciones de opción SET requeridas con vistas indizadas e índices en columnas calculadas, vea "Consideraciones cuando se Use las instrucciones SET" en [instrucciones SET &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente ANSI_DEFAULTS en ON al conectarse. El controlador y el proveedor establecen a continuación CURSOR_CLOSE_ON_COMMIT e IMPLICIT_TRANSACTIONS en OFF. La opción OFF de SET CURSOR_CLOSE_ON_COMMIT y SET IMPLICIT_TRANSACTIONS se puede configurar en los orígenes de datos ODBC, en los atributos de conexión ODBC o en las propiedades de conexión OLE DB que se establecen en la aplicación antes de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. SET ANSI_DEFAULTS tiene como opción predeterminada OFF en las conexiones desde aplicaciones DB-Library.  
  
 Cuando se ejecuta SET ANSI_DEFAULTS, SET QUOTED_IDENTIFIER se establece en tiempo de análisis y las opciones siguientes se establecen en tiempo de ejecución:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establece `SET ANSI_DEFAULTS ON` y se utiliza la instrucción `DBCC USEROPTIONS` para mostrar la configuración afectada.  
  
```  
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
  
## <a name="see-also"></a>Vea también  
 [DBCC USEROPTIONS &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40; Transact-SQL &#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

