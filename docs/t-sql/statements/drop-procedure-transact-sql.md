---
title: DROP PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aef67c09e34bf23fa1185cc10b12ff3fb88e6a6c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita uno o más procedimientos almacenados o grupos de procedimientos de la base de datos actual en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita el procedimiento condicionalmente solo si ya existe.  
  
 *schema_name*  
 El nombre del esquema al que pertenece el procedimiento. No se puede especificar un nombre de servidor o un nombre de base de datos.  
  
 *procedure*  
 Nombre del procedimiento almacenado o grupo de procedimientos almacenados que se van a quitar. No se pueden quitar procedimientos concretos de un grupo de procedimientos numerados, ya que de este modo se quita el grupo de procedimientos completo.  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Antes de quitar un procedimiento almacenado, compruebe los objetos dependientes y modifique estos objetos como corresponda. La acción de quitar un procedimiento almacenado puede hacer que los objetos dependientes y los scripts sufran errores cuando estos objetos no están actualizados. Para más información, vea [Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
## <a name="metadata"></a>Metadatos  
 Para consultar una lista de procedimientos existentes, vea la vista de catálogo **sys.objects**. Para consultar la definición del procedimiento, vea la vista de catálogo **sys.sql_modules**.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Se necesita el permiso **CONTROL** en el procedimiento o el permiso **ALTER** en el esquema al que corresponde el procedimiento, o la pertenencia al rol fijo de servidor **db_ddladmin**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita el procedimiento almacenado `dbo.uspMyProc` de la base de datos actual.  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 En el siguiente ejemplo se quitan varios procedimientos almacenados de la base de datos actual.  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 En este ejemplo se quita el procedimiento almacenado `dbo.uspMyProc`, si existe, pero no se produce un error si el procedimiento no existe. Esta sintaxis es nueva en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>Ver también  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Eliminar un procedimiento almacenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  


