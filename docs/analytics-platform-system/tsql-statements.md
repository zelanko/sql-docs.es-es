---
title: 'Instrucciones de T-SQL: almacenamiento de datos paralelos | Microsoft Docs'
description: Instrucciones de T-SQL para analíticas Platform System (APS) Parallel Data Warehouse (PDW de SQL Server).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ca12b3926fb848defc2a19a08ffa9702516726fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034942"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>Instrucciones de T-SQL para almacenamiento de datos paralelos
Instrucciones de Transact-SQL (T-SQL) para analíticas Platform System (APS) Parallel Data Warehouse (PDW de SQL Server).

## <a name="data-definition-language-ddl-statements"></a>Instrucciones de lenguaje de definición (DDL) de datos
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ALTER SCHEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREATE COLUMNSTORE INDEX](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREATE DATABASE](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [CREAR BASE DE DATOS CON ÁMBITO DE CREDENCIAL](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREAR ORIGEN DE DATOS EXTERNO](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREAR FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CREAR TABLA EXTERNA](../t-sql/statements/create-external-table-transact-sql.md)
* [CREAR FUNCIÓN](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CREATE SCHEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [INSTRUCCIÓN CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [QUITAR ORIGEN DE DATOS EXTERNO](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [QUITAR EL FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [QUITAR TABLA EXTERNA](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [QUITAR EL PROCEDIMIENTO](../t-sql/statements/drop-procedure-transact-sql.md)
* [QUITAR LAS ESTADÍSTICAS](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [ELIMINAR ESQUEMA](../t-sql/statements/drop-schema-transact-sql.md)
* [QUITAR VISTA](../t-sql/statements/drop-view-transact-sql.md)
* [RENAME](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>Instrucciones de lenguaje de manipulación (DML) de datos
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>Comandos de consola de base de datos
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>Instrucciones de consulta
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT e INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [EXPLAIN](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [Usar PIVOT y UNPIVOT](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [TOP](../t-sql/queries/top-transact-sql.md)
* [Creación de alias](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [Condición de búsqueda](../t-sql/queries/search-condition-transact-sql.md)
* [Subconsultas](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>Instrucciones de seguridad
* Permisos: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [MODIFICAR CERTIFICADO](../t-sql/statements/alter-certificate-transact-sql.md)
* [MODIFICAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [MODIFICAR CLAVE MAESTRA](../t-sql/statements/alter-master-key-transact-sql.md)
* [MODIFICAR ROL](../t-sql/statements/alter-role-transact-sql.md)
* [MODIFICAR USUARIO](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [CREAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
* [CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)
* [CREAR ROL](../t-sql/statements/create-role-transact-sql.md)
* [CREAR USUARIO](../t-sql/statements/create-user-transact-sql.md)
* [QUITAR CERTIFICADO](../t-sql/statements/drop-certificate-transact-sql.md)
* [DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [DROP LOGIN](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [QUITAR ROL](../t-sql/statements/drop-role-transact-sql.md)
* [QUITE EL USUARIO](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información de referencia, consulte [elementos del lenguaje T-SQL](tsql-language-elements.md) y [vistas del sistema T-SQL](tsql-system-views.md).

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
