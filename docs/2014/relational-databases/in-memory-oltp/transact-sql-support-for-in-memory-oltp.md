---
title: Compatibilidad de Transact-SQL con OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8042534c8b22863c5a00abf4969bdb9754cef892
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702212"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Compatibilidad de Transact-SQL con OLTP en memoria
  Puede acceder a las tablas optimizadas para memoria con cualquier consulta de Transact-SQL o instrucción DML (SELECT, INSERT, UPDATE o DELETE), instrucción ad hoc o módulo SQL como, por ejemplo, procedimientos almacenados, funciones con valores de tabla, funciones escalares, desencadenadores y vistas. Para obtener más información, vea [obtener acceso a tablas optimizadas para memoria mediante Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 Los procedimientos almacenados que solo hacen referencia a tablas optimizadas para memoria se pueden compilar de forma nativa en código máquina. Por lo general, proporcionan un rendimiento considerable que los procedimientos almacenados interpretados (basados en disco). Para optimizar el acceso a las tablas optimizadas para memoria, utilice procedimientos almacenados compilados de forma nativa. Para más información, vea [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md).  
  
 Al crear y modificar objetos de base de datos (instrucciones DDL), se modificaron las siguientes instrucciones:  
  
-   [Opciones File y filegroup de Alter database &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (vea `MEMORY_OPTIMIZED_DATA` )  
  
-   [CREATE DATABASE &#40;SQL Server&#41;de Transact-SQL](/sql/t-sql/statements/create-database-sql-server-transact-sql) (vea `MEMORY_OPTIMIZED_DATA` )  
  
-   [Create procedure &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql) (vea `NATIVE_COMPILATION` , `SCHEMABINDING` , `EXECUTE AS` y `BEGIN ATOMIC` )  
  
-   [CREATE TABLE &#40;&#41;de Transact-SQL](/sql/t-sql/statements/create-table-transact-sql) (vea,,, `MEMORY_OPTIMIZED` `DURABILITY` `BUCKET_COUNT` `INDEX` y `HASH` )  
  
-   [Create Type &#40;&#41;de Transact-SQL](/sql/t-sql/statements/create-type-transact-sql) (vea `MEMORY_OPTIMIZED` ,, `BUCKET_COUNT` `INDEX` y `HASH` )  
  
-   [Declare @local_variable &#40;&#41;de TRANSACT-SQL](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (vea `NULL`  |  `NOT NULL` )  
  
 Las tablas con optimización para memoria admiten las restricciones `PRIMARY KEY` y `NOT NULL`. Para obtener información sobre la implementación de restricciones no admitidas, vea [migración de restricciones check y Foreign Key](../../database-engine/migrating-check-and-foreign-key-constraints.md).  
  
 Para obtener más información sobre las características no compatibles, vea [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Tipos de datos admitidos](supported-data-types-for-in-memory-oltp.md)  
  
-   [Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [Vistas del sistema, procedimientos almacenados, tipos de espera para OLTP en memoria y DMV](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>Consulte también  
 [&#40;de optimización en memoria de OLTP en memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Características admitidas de SQL Server](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
