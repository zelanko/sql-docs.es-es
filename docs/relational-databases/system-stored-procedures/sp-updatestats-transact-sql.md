---
title: sp_updatestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c00bdd453bc4d1bf467b37aca3639eb43f55e022
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085790"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Se `UPDATE STATISTICS` ejecuta en todas las tablas internas y definidas por el usuario en la base de datos actual.  
  
Para obtener más información `UPDATE STATISTICS`acerca de, consulte [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Para obtener más información sobre las estadísticas, vea [Estadísticas](../../relational-databases/statistics/statistics.md).  
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="arguments"></a>Argumentos  
`[ @resample = ] 'resample'`Especifica que **sp_updatestats** utilizará la opción volver a muestrear de la instrucción [Update Statistics](../../t-sql/statements/update-statistics-transact-sql.md) . Si no se especifica **' resample '** , **sp_updatestats** actualiza las estadísticas mediante el muestreo predeterminado. **resample** es de tipo **VARCHAR (8)** y su valor predeterminado es no.  
  
## <a name="remarks"></a>Observaciones  
 **sp_updatestats** ejecuta `UPDATE STATISTICS`, especificando la `ALL` palabra clave, en todas las tablas internas y definidas por el usuario en la base de datos. sp_updatestats muestra mensajes que indican su progreso. Cuando la actualización se ha completado, informa de que se han actualizado las estadísticas de todas las tablas.  
  
sp_updatestats actualiza las estadísticas en índices no clúster deshabilitados y no actualiza las estadísticas en índices clúster deshabilitados.  
  
En el caso de las tablas basadas en disco, **sp_updatestats** actualiza las estadísticas basadas en la información de **modification_counter** de la vista de catálogo **Sys. dm_db_stats_properties** , actualizando las estadísticas donde se ha modificado al menos una fila. Las estadísticas de las tablas optimizadas para memoria se actualizan siempre al ejecutar **sp_updatestats**. Por lo tanto, no ejecute **sp_updatestats** más de lo necesario.  
  
**sp_updatestats** puede desencadenar una nueva compilación de procedimientos almacenados u otro código compilado. Sin embargo, es posible que **sp_updatestats** no vuelva a compilar, si solo es posible un plan de consulta para las tablas a las que se hace referencia y los índices que hay en ellos. En estos casos sería necesaria una recompilación, aunque las estadísticas estén actualizadas.  
  
En el caso de las bases de datos con un nivel de compatibilidad inferior a 90, la ejecución de **sp_updatestats** no conserva el valor de NORECOMPUTE más reciente para estadísticas específicas. En el caso de las bases de datos con un nivel de compatibilidad de 90 o superior, sp_updatestats conserva la opción más reciente de NORECOMPUTE para estadísticas específicas. Para obtener más información sobre cómo deshabilitar y volver a habilitar las actualizaciones de estadísticas, vea [Estadísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** o la propiedad de la base de datos (**DBO**).  

## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se actualizan las estadísticas de las tablas de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>Administración automática de índice y estadísticas
Aproveche soluciones como la [desfragmentación de índice adaptable](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para administrar automáticamente las actualizaciones de estadísticas y la desfragmentación de índices para una o varias bases de datos. Este procedimiento elige automáticamente si se debe volver a generar o reorganizar un índice según su nivel de fragmentación, entre otros parámetros y actualiza las estadísticas con un umbral lineal.

## <a name="see-also"></a>Consulte también  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICs &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Procedimientos almacenados del sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
