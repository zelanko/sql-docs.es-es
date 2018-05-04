---
title: Sys.sp_cdc_get_ddl_history (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4a830d8d3c79987b56b79d0a87f329018b070c4b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcgetddlhistory-transact-sql"></a>sys.sp_cdc_get_ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el historial del lenguaje de definición de datos (DDL, Data Definition Language) asociado con la instancia de captura especificada desde que se habilitó la captura de datos de cambio para dicha instancia de captura. La captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance =] '*capture_instance*'  
 Es el nombre de la instancia de captura asociada a una tabla de origen. *capture_instance* es **sysname** y no puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nombre del esquema de la tabla de origen.|  
|source_table|**sysname**|Nombre de la tabla de origen.|  
|capture_instance|**sysname**|Nombre de la instancia de captura.|  
|required_column_update|**bit**|Indica que para cambiar el archivo DDL ha sido necesario modificar una columna de la tabla de cambios para reflejar que se cambiado un tipo de datos en la columna de origen.|  
|ddl_command|**nvarchar(max)**|Instrucción DDL aplicada a la tabla de origen.|  
|ddl_lsn|**binary(10)**|Número de secuencia de registro (LSN) asociado con el cambio de DDL.|  
|ddl_time|**datetime**|Hora asociada al cambio de DDL.|  
  
## <a name="remarks"></a>Comentarios  
 Modificaciones de DDL en la tabla de origen que cambian la estructura de columnas de tabla de origen, como agregar o quitar una columna o cambiar el tipo de datos de una columna existente, se mantienen en la [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) tabla. Se puede crear un informe de estos cambios usando este procedimiento almacenado. Las entradas en cdc.ddl_history se realizan cuando el proceso de captura lee la transacción de DDL en el registro.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de base de datos db_owner para devolver filas para todas las instancias de captura de la base de datos. Para el resto de usuarios, requiere el permiso SELECT en todas las columnas capturadas en la tabla de origen y, si se ha definido un rol de acceso para la instancia de captura, la pertenencia a ese rol de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega una columna a la tabla de origen `HumanResources.Employee` y luego se ejecuta el procedimiento almacenado `sys.sp_cdc_get_ddl_history` para informar sobre los cambios del DDL que se aplican a la tabla de origen asociada con la instancia de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
