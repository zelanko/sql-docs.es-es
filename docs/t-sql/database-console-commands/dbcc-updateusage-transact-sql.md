---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 68e7743681c6023c86d0298eef022ef178eeb411
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611873"
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Informa sobre imprecisiones de recuento de filas y páginas de las vistas de catálogo y las corrige. Estas imprecisiones pueden causar la devolución de informes incorrectos sobre uso de espacio por parte del procedimiento almacenado del sistema sp_spaceused.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
*database_name* | *database_id* | 0  
Es el nombre o el identificador de la base de datos sobre cuyas estadísticas de uso de espacio se va a informar y las cuales se van a corregir. Si se especifica 0, se utiliza la base de datos actual. Los nombres de las bases de datos deben cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
*table_name* | *table_id* | *view_name* | *view_id*  
Es el nombre o el identificador de la tabla o la vista indizada sobre cuyas estadísticas de uso de espacio se va a informar y las que se van a corregir. Los nombres de las tablas y las vistas deben ajustarse a las reglas de los identificadores.  
  
*index_id* | *index_name*  
Es el identificador o el nombre del índice que se va a utilizar. Si no se especifica, la instrucción procesa todos los índices de la tabla o la vista especificada.  
  
por  
Permite la especificación de opciones.  
  
NO_INFOMSGS  
Suprime todos los mensajes de información.  
  
COUNT_ROWS  
Especifica que la columna row count se actualiza con el recuento actual del número de filas de la tabla o la vista.  
  
## <a name="remarks"></a>Notas  
Si una tabla o un índice tienen particiones, DBCC UPDATEUSAGE corrige los recuentos de las filas, las páginas utilizadas, las páginas reservadas, las páginas hoja y las páginas de datos. Si no hay imprecisiones en las tablas del sistema, DBCC UPDATEUSAGE no devuelve datos. Si se encuentran y se corrigen imprecisiones y no se utiliza WITH NO_INFOMSGS, DBCC UPDATEUSAGE devuelve las filas y las columnas que se están actualizando en las tablas del sistema.
  
DBCC CHECKDB se ha mejorado para detectar si los recuentos de páginas o filas devuelven valores negativos. En caso de que se detecte un recuento negativo, la salida de DBCC CHECKDB contiene una advertencia y una recomendación para que se ejecute DBCC UPDATEUSAGE con el fin de solucionar el problema.
  
## <a name="best-practices"></a>Procedimientos recomendados  
Se recomienda lo siguiente:
-   No ejecute DBCC UPDATEUSAGE de forma rutinaria. Dado que DBCC UPDATEUSAGE puede tardar algún tiempo en ejecutarse con tablas o bases de datos grandes, no se debería utilizar a menos que sospeche que sp_spaceused está devolviendo valores incorrectos.
-   Considere ejecutar DBCC UPDATEUSAGE habitualmente, por ejemplo cada semana, solo si la base de datos sufre con frecuencia modificaciones del Lenguaje de definición de datos (DDL), por ejemplo, con las instrucciones CREATE, ALTER o DROP.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC UPDATEUSAGE devuelve (los valores pueden variar):
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. Actualizar recuentos de páginas o filas, o ambos, para todos los objetos de la base de datos actual  
En el siguiente ejemplo se especifica `0` como nombre de la base de datos y `DBCC UPDATEUSAGE` devuelve información actualizada del recuento de filas o páginas de la base de datos actual.
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. Actualizar recuentos de páginas o filas, o ambos, para AdventureWorks y suprimir los mensajes informativos  
En el siguiente ejemplo se especifica [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como nombre de la base de datos y se suprimen todos los mensajes informativos.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Actualizar recuentos de páginas o filas, o ambos, para la tabla Employee  
En el siguiente ejemplo se devuelve información actualizada del recuento de filas o páginas de la tabla `Employee` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. Actualizar recuentos de página o fila, o ambos, para un índice específico de una tabla  
 En el siguiente ejemplo se especifica `IX_Employee_ManagerID` como nombre de índice.  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>Ver también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  
