---
title: sp_autostats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6264266f85edc1cae0821bbcf81c8c0993dba151
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62995687"
---
# <a name="spautostats-transact-sql"></a>sp_autostats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra o cambia la opción de actualización automática de estadísticas, AUTO_UPDATE_STATISTICS, para un índice, un objeto de estadísticas, una tabla o una vista indizada.  
  
 Para obtener más información acerca de la opción AUTO_UPDATE_STATISTICS, consulte [ALTER DATABASE SET Options &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) y [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tblname = ] 'table_or_indexed_view_name'` Es el nombre de la tabla o vista indizada para mostrar la opción AUTO_UPDATE_STATISTICS en. *table_or_indexed_view_name* es **nvarchar(776)** , no tiene ningún valor predeterminado.  
  
`[ @flagc = ] 'stats_value'` Actualiza la opción AUTO_UPDATE_STATISTICS a uno de estos valores:  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 Cuando *stats_flag* no es se especifica, muestra la configuración actual de AUTO_UPDATE_STATISTICS. *stats_value* es **varchar (10)** , su valor predeterminado es null.  
  
`[ @indname = ] 'statistics_name'` Es el nombre de las estadísticas para mostrar o actualizar la opción AUTO_UPDATE_STATISTICS en. Para que se muestren las estadísticas de un índice, se puede usar el nombre del mismo; un índice y su objeto de estadísticas correspondiente tienen el mismo nombre.  
  
 *statistics_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si *stats_flag* se especifica, **sp_autostats** informa acerca de la acción que se realizó, pero no devuelve ningún conjunto de resultados.  
  
 Si *stats_flag* no se especifica, **sp_autostats** devuelve el siguiente conjunto de resultados.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre de índice**|**varchar(60)**|Nombre del índice o de las estadísticas.|  
|**AUTOSTATS**|**varchar(3)**|Valor actual para la opción AUTO_UPDATE_STATISTICS.|  
|**Última actualización**|**datetime**|Fecha de la actualización más reciente de las estadísticas.|  
  
 El conjunto de resultados para una tabla o vista indizada incluye estadísticas creadas para índices, estadísticas de columna única generadas con la opción AUTO_CREATE_STATISTICS y estadísticas crean con el [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) instrucción.  
  
## <a name="remarks"></a>Comentarios  
 Si el índice especificado está deshabilitado, o si la tabla especificada tiene un índice clúster deshabilitado, aparece un mensaje de error.  
  
 AUTO_UPDATE_STATISTICS siempre es OFF para las tablas optimizadas para memoria  
  
## <a name="permissions"></a>Permisos  
 Para cambiar el AUTO_UPDATE_STATISTICS opción requiere la pertenencia a n el **db_owner** rol fijo de base de datos o permiso ALTER *table_name*. Para mostrar el AUTO_UPDATE_STATISTICS opción requiere la pertenencia a la **pública** rol.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. Mostrar el estado de todas las estadísticas de una tabla  
 En el ejemplo siguiente, se muestra el estado de todas las estadísticas de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>b. Habilitar AUTO_UPDATE_STATISTICS para todas las estadísticas de una tabla  
 En el ejemplo siguiente, se habilita la opción AUTO_UPDATE_STATISTICS para todas las estadísticas de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>C. Deshabilitar AUTO_UPDATE_STATISTICS para un índice especificado  
 En el ejemplo siguiente, se deshabilita la opción AUTO_UPDATE_STATISTICS para el índice `AK_Product_Name` de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
