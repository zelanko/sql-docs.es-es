---
title: sp_createstats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c89f3aed714fba775e2271425fb86949e3f26ac
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spcreatestats-transact-sql"></a>sp_createstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Llamadas a la [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrucción para crear estadísticas de columna única en columnas que no sean la primera columna de un objeto de estadísticas. La creación de estadísticas de columna única aumenta el número de histogramas, lo que puede mejorar las estimaciones de cardinalidad, los planes de consulta y el rendimiento de las consultas. La primera columna de un objeto de estadísticas tiene un histograma; otras columnas no tienen un histograma.  
  
 sp_createstats es útil para aplicaciones como las pruebas comparativas cuando los tiempos de ejecución de la consulta resultan críticos y no se puede esperar a que el optimizador de consultas genere estadísticas de columna única. En la mayoría de los casos, no es necesario utilizar sp_createstats; el optimizador de consultas genera estadísticas de columna única según sea necesario para mejorar los planes cuando la **AUTO_CREATE_STATISTICS** opción está activada.  
  
 Para obtener más información acerca de las estadísticas, vea [estadísticas](../../relational-databases/statistics/statistics.md). Para obtener más información acerca de cómo generar estadísticas de columna única, consulte la **AUTO_CREATE_STATISTICS** opción [ALTER DATABASE SET Options &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@indexonly=** ] **'indexonly'**  
 Crea estadísticas solo en columnas que se encuentran en un índice existente y que no son la primera columna de cualquier definición de índice. **indexonly** es **char (9)**. El valor predeterminado es NO.  
  
 [  **@fullscan=** ] **'fullscan'**  
 Usa el [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrucción con el **FULLSCAN** opción. **FULLSCAN** es **char (9)**.  El valor predeterminado es NO.  
  
 [  **@norecompute=** ] **'norecompute'**  
 Usa el [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrucción con el **NORECOMPUTE** opción. **NORECOMPUTE** es **char(12)**.  El valor predeterminado es NO.  
  
 [  **@incremental=** ] **"incremental"**  
 Usa el [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrucción con el **INCREMENTAL = ON** opción. **Incremental** es **char(12)**.  El valor predeterminado es NO.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Cada nuevo objeto de estadísticas tiene el mismo nombre que la columna en la que se creó.  
  
## <a name="remarks"></a>Comentarios  
 sp_createstats no crea ni actualiza estadísticas en columnas que son la primera columna de un objeto de estadísticas existente;  Esto incluye la primera columna de las estadísticas creadas para índices, columnas con estadísticas de columna única generadas con la opción AUTO_CREATE_STATISTICS y la primera columna de las estadísticas creadas con la instrucción CREATE STATISTICS. sp_createstats no crea estadísticas en las primeras columnas de índices deshabilitados a menos que esa columna se utiliza en otro índice habilitado. sp_createstats no crea estadísticas en tablas con un índice clúster deshabilitado.  
  
 Cuando la tabla contiene un conjunto de columnas, sp_createstats no crea automáticamente estadísticas en columnas dispersas. Para obtener más información sobre conjuntos de columnas y las columnas dispersas, vea [usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md) y [usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere pertenencia al rol fijo de base de datos db_owner.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>A. Crear estadísticas de columna única en todas las columnas coincidentes  
 En el siguiente ejemplo, se crean estadísticas de columna única en todas las columnas coincidentes de la base de datos actual.  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. Crear estadísticas de columna única en todas las columnas de índice coincidentes  
 En el ejemplo siguiente, se crean estadísticas de columna única en todas las columnas coincidentes que ya se encuentran en un índice y que no son la primera columna del índice.  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Estadísticas](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
