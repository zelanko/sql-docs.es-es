---
title: Instrucciones de T-SQL
description: Instrucciones T-SQL para el sistema de plataforma analítica (APS) SQL Server almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ce80d7a27384f628af02bfa58abcaa351b569d56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399810"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>Instrucciones T-SQL para almacenamiento de datos paralelos
Instrucciones Transact-SQL (T-SQL) para el sistema de plataforma analítica (APS) SQL Server almacenamiento de datos paralelos (PDW).

## <a name="data-definition-language-ddl-statements"></a>Instrucciones del Lenguaje de definición de datos (DDL)
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [MODIFICAR ESQUEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREAR ÍNDICE DE ALMACÉN DE COLUMNAS](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREAR BASE DE DATOS](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [CREAR CREDENCIAL CON ÁMBITO DE BASE DE DATOS](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREAR ORIGEN DE DATOS EXTERNO](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREAR FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CREAR TABLA EXTERNA](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE (FUNCIÓN)](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREAR ÍNDICE](../t-sql/statements/create-index-transact-sql.md)
* [CREAR PROCEDIMIENTO](../t-sql/statements/create-procedure-transact-sql.md)
* [CREAR ESQUEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREAR ESTADÍSTICAS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE COMO SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREAR VISTA](../t-sql/statements/create-view-transact-sql.md)
* [QUITAR ORIGEN DE DATOS EXTERNO](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [QUITAR FORMATO DE ARCHIVO EXTERNO](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [QUITAR TABLA EXTERNA](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP PROCEDURE](../t-sql/statements/drop-procedure-transact-sql.md)
* [QUITAR ESTADÍSTICAS](../t-sql/statements/drop-statistics-transact-sql.md)
* [QUITAR TABLA](../t-sql/statements/drop-table-transact-sql.md)
* [DROP SCHEMA](../t-sql/statements/drop-schema-transact-sql.md)
* [QUITAR VISTA](../t-sql/statements/drop-view-transact-sql.md)
* [CAMBIAR el nombre](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [ACTUALIZAR ESTADÍSTICAS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>Instrucciones del Lenguaje de manipulación de datos (DML)
* [ELIMÍNELOS](../t-sql/statements/delete-transact-sql.md)
* [INTRODUCIR](../t-sql/statements/insert-transact-sql.md)
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
* [NO](../t-sql/queries/select-transact-sql.md)
* [CON common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [Except e INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [Explique](../t-sql/queries/explain-transact-sql.md)
* [De](../t-sql/queries/from-transact-sql.md)
* [Usar PIVOT y UnPivot](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [AGRUPAR POR](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDENAR POR](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [DESEA](../t-sql/queries/option-clause-transact-sql.md)
* [Unión](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [MIENTRAS](../t-sql/queries/where-transact-sql.md)
* [TOP](../t-sql/queries/top-transact-sql.md)
* [Alias](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [Condición de búsqueda](../t-sql/queries/search-condition-transact-sql.md)
* [Subconsultas](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>Instrucciones de seguridad
* Permisos: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [MODIFICAR CERTIFICADO](../t-sql/statements/alter-certificate-transact-sql.md)
* [MODIFICAR LA CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [MODIFICAR CLAVE MAESTRA](../t-sql/statements/alter-master-key-transact-sql.md)
* [MODIFICAR ROL](../t-sql/statements/alter-role-transact-sql.md)
* [MODIFICAR USUARIO](../t-sql/statements/alter-user-transact-sql.md)
* [CERTIFICADO DE COPIA DE SEGURIDAD](../t-sql/statements/backup-certificate-transact-sql.md)
* [CERRAR CLAVE MAESTRA](../t-sql/statements/close-master-key-transact-sql.md)
* [CREAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
* [CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREAR INICIO DE SESIÓN](../t-sql/statements/create-login-transact-sql.md)
* [CREAR CLAVE MAESTRA](../t-sql/statements/create-master-key-transact-sql.md)
* [CREAR ROL](../t-sql/statements/create-role-transact-sql.md)
* [CREAR USUARIO](../t-sql/statements/create-user-transact-sql.md)
* [QUITAR CERTIFICADO](../t-sql/statements/drop-certificate-transact-sql.md)
* [QUITAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [QUITAR INICIO DE SESIÓN](../t-sql/statements/drop-login-transact-sql.md)
* [QUITAR CLAVE MAESTRA](../t-sql/statements/drop-master-key-transact-sql.md)
* [QUITAR ROL](../t-sql/statements/drop-role-transact-sql.md)
* [QUITAR USUARIO](../t-sql/statements/drop-user-transact-sql.md)
* [ABRIR CLAVE MAESTRA](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información de referencia, vea [elementos del lenguaje t-SQL](tsql-language-elements.md) y [vistas del sistema t-SQL](tsql-system-views.md).

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
