---
title: Compatibilidad de Transact-SQL con OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db4c6895fb499458c198008319302a25b8cd34b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156214"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Compatibilidad de Transact-SQL con OLTP en memoria
  Puede acceder a las tablas optimizadas para memoria con cualquier consulta de Transact-SQL o instrucción DML (SELECT, INSERT, UPDATE o DELETE), instrucción ad hoc o módulo SQL como, por ejemplo, procedimientos almacenados, funciones con valores de tabla, funciones escalares, desencadenadores y vistas. Para obtener más información, consulte [acceso tablas mediante Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 Los procedimientos almacenados que solo hacen referencia a tablas optimizadas para memoria se pueden compilar de forma nativa en código máquina. Por lo general, proporcionan un rendimiento considerable que los procedimientos almacenados interpretados (basados en disco). Para optimizar el acceso a las tablas optimizadas para memoria, utilice procedimientos almacenados compilados de forma nativa. Para más información, vea [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md).  
  
 Al crear y modificar objetos de base de datos (instrucciones DDL), se modificaron las siguientes instrucciones:  
  
-   [Opciones ALTER DATABASE File y Filegroup &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (consulte `MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41; ](/sql/t-sql/statements/create-database-sql-server-transact-sql) (consulte `MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-procedure-transact-sql) (consulte `NATIVE_COMPILATION`, `SCHEMABINDING`, `EXECUTE AS`, y `BEGIN ATOMIC`)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) (consulte `MEMORY_OPTIMIZED`, `DURABILITY`, `BUCKET_COUNT`, `INDEX`, y `HASH`)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql) (consulte `MEMORY_OPTIMIZED`, `BUCKET_COUNT`, `INDEX`, y `HASH`)  
  
-   [DECLARAR @local_variable &#40;Transact-SQL&#41; ](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (consulte `NULL`  |  `NOT NULL`)  
  
 Las tablas con optimización para memoria admiten las restricciones `PRIMARY KEY` y `NOT NULL`. Para obtener información sobre la implementación de restricciones no admitidas, vea [restricciones Foreign Key y comprobación de migración](../../database-engine/migrating-check-and-foreign-key-constraints.md).  
  
 Para obtener más información sobre las características no compatibles, vea [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Tipos de datos admitidos](supported-data-types-for-in-memory-oltp.md)  
  
-   [Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [Vistas del sistema, procedimientos almacenados, tipos de espera para OLTP en memoria y DMV](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Características admitidas de SQL Server](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
