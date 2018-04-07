---
title: Almacenamiento de datos paralelos de sistema de plataforma de análisis de instrucciones de T-SQL | Documentos de Microsoft
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Instrucciones de Transact-SQL (T-SQL) para análisis Platform System (APS) SQL Server paralelo almacenamiento de datos (PDW).
documentationcenter: NA
editor: ''
ms.assetid: 0abc5934-1e67-491a-b7d7-8b520d1ae98e
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 12/15/2016
ms.openlocfilehash: 2109e1aaa48fb95da2b4d8b36aee7bbc86ea4ef4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="t-sql-topics"></a>Temas de T-SQL
Instrucciones de Transact-SQL (T-SQL) para análisis Platform System (APS) SQL Server paralelo almacenamiento de datos (PDW).

## <a name="data-definition-language-ddl-statements"></a>Instrucciones de lenguaje de definición (DDL) de datos
* [MODIFICAR BASE DE DATOS](../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ALTER SCHEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [MODIFICAR TABLA](../t-sql/statements/alter-table-transact-sql.md)
* [CREAR ÍNDICE DE ALMACÉN](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREAR BASE DE DATOS](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [CREAR BASE DE DATOS CON ÁMBITO DE CREDENCIAL](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREAR ORIGEN DE DATOS EXTERNO](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREAR FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CREAR TABLA EXTERNA](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE (FUNCIÓN)](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CREAR ESQUEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREAR TABLA COMO SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [COLOQUE EL ORIGEN DE DATOS EXTERNO](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [QUITAR EL FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [QUITAR TABLA EXTERNA](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [ELIMINAR EL PROCEDIMIENTO](../t-sql/statements/drop-procedure-transact-sql.md)
* [QUITAR LAS ESTADÍSTICAS](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [ESQUEMA DE DESTINO](../t-sql/statements/drop-schema-transact-sql.md)
* [ELIMINAR LA VISTA](../t-sql/statements/drop-view-transact-sql.md)
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
* [Uso de alias](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [Condición de búsqueda](../t-sql/queries/search-condition-transact-sql.md)
* [Subconsultas](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>Instrucciones de seguridad
* Permisos: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOCAR](../t-sql/statements/revoke-transact-sql.md)
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
* [CREAR EL INICIO DE SESIÓN](../t-sql/statements/create-login-transact-sql.md)
* [CREAR LA CLAVE MAESTRA](../t-sql/statements/create-master-key-transact-sql.md)
* [CREAR ROL](../t-sql/statements/create-role-transact-sql.md)
* [CREAR USUARIO](../t-sql/statements/create-user-transact-sql.md)
* [QUITAR CERTIFICADO](../t-sql/statements/drop-certificate-transact-sql.md)
* [QUITAR LA CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [QUITAR INICIO DE SESIÓN](../t-sql/statements/drop-login-transact-sql.md)
* [QUITAR LA CLAVE MAESTRA](../t-sql/statements/drop-master-key-transact-sql.md)
* [QUITAR ROL](../t-sql/statements/drop-role-transact-sql.md)
* [QUITE EL USUARIO](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>Pasos siguientes
Para obtener información de referencia, vea [elementos del lenguaje T-SQL](tsql-language-elements.md) y [vistas del sistema de T-SQL](tsql-system-views.md).

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
