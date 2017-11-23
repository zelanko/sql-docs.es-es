---
title: Core.sp_purge_data (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs: TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b03e5ef5984431f3fe2867e2dc303ca2ba710435
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="coresppurgedata-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita los datos del almacén de administración de datos basándose en una directiva de retención. Este procedimiento lo ejecuta diariamente el mdw_purge_data[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente en el almacén de datos de administración asociado a la instancia especificada. Puede utilizar este procedimiento almacenado para realizar una eliminación a petición de los datos del almacén de administración de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@retention_days =] *retention_days*  
 Número de días que se van a retener los datos en las tablas de almacén de administración de datos. Datos con una marca de tiempo anterior a *retention_days* se quita. *retention_days* es **smallint**, su valor predeterminado es null. Si se especifica, el valor debe ser positivo. Cuando es NULL, el valor de la columna valid_through de la vista core.snapshots determina las filas que pueden eliminarse.  
  
 [@instance_name =] '*instance_name*'  
 Nombre de la instancia del conjunto de recopilación. *instance_name* es **sysname**, su valor predeterminado es null.  
  
 *instance_name* debe ser el nombre de instancia completo, que consta del nombre del equipo y el nombre de instancia en el formulario *computername*\\*nombreDeInstancia*. Cuando es NULL, se utiliza la instancia predeterminada en el servidor local.  
  
 [@collection_set_uid =] '*collection_set_uid*'  
 GUID del conjunto de recopilación. *collection_set_uid* es **uniqueidentifier**, su valor predeterminado es null. Cuando es NULL, se quitan las filas certificadas de todos los conjuntos de recopilación. Para obtener este valor, consulte la vista de catálogo syscollector_collection_sets.  
  
 [@duration =] *duración*  
 El número máximo de minutos que debe durar la ejecución de la operación de purga. *duración* es **smallint**, su valor predeterminado es null. Si se especifica, el valor debe ser cero o un entero positivo. Cuando es NULL, la operación se ejecuta hasta que se quitan todas las filas certificadas o se detiene manualmente la operación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento selecciona las filas de la vista core.snapshots que pueden quitarse de acuerdo con el período de retención. Todas las filas que se pueden quitar se eliminan de la tabla core.snapshots_internal. La eliminación de las filas precedentes desencadenará una acción de eliminación en cascada en todas las tablas del almacén de administración de datos. Esto se consigue al usar la cláusula ON DELETE CASCADE, que se define para todas las tablas que contienen datos recopilados.  
  
 Cada instantánea y sus datos asociados se eliminan dentro de una transacción explícita y, a continuación, se confirma la operación. Por lo tanto, si la operación de purga se detuvo manualmente, o el valor especificado para @duration se supera, solo los datos no confirmados permanecen. Estos datos se pueden quitar la próxima vez que se ejecute el trabajo.  
  
 El procedimiento se debe ejecutar en el contexto de la base de datos de almacén de administración de datos.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **mdw_admin** (con permiso EXECUTE) rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-running-sppurgedata-with-no-parameters"></a>A. Ejecución de sp_purge_data sin parámetros  
 En el ejemplo siguiente se ejecuta core.sp_purge_data sin especificar ningún parámetro. Por consiguiente, el valor predeterminado NULL se utiliza para todos los parámetros, con el comportamiento asociado.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. Especificación de valores de retención y duración  
 En el ejemplo siguiente se quitan los datos del almacén de administración de datos anteriores a 7 días. Además, el @duration se especifica el parámetro para que se ejecutará la operación no supere los 5 minutos.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. Especificación de un nombre de instancia y un conjunto de recopilación  
 En el ejemplo siguiente se quitan los datos del almacén de administración de datos que contiene un conjunto de recopilación determinado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada. Dado que @retention_days no se especifica, el valor de la columna valid_through de la vista core.snapshots se usa para determinar las filas del conjunto de recopilación que pueden quitarse.  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
