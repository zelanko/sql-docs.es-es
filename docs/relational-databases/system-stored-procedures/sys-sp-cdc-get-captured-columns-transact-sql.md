---
title: Sys.sp_cdc_get_captured_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d5ee0208c59da7346316ae6ef5aa31d81717b6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcgetcapturedcolumns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la información de los metadatos de captura de datos de cambio para las columnas de origen de las que la instancia de captura especificada ha realizado un seguimiento. La captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance =] '*capture_instance*'  
 Es el nombre de la instancia de captura asociada a una tabla de origen. *capture_instance* es **sysname** y no puede ser NULL.  
  
 Para informar sobre las instancias de captura para la tabla, ejecute el [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) procedimiento almacenado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nombre del esquema de la tabla de origen.|  
|source_table|**sysname**|Nombre de la tabla de origen.|  
|capture_instance|**sysname**|Nombre de la instancia de captura.|  
|column_name|**sysname**|Nombre de la columna de origen capturada.|  
|column_id|**int**|Id. de la columna en la tabla de origen.|  
|ordinal_position|**int**|Posición de la columna dentro de la tabla de origen.|  
|data_type|**sysname**|Tipo de datos de la columna.|  
|character_maximum_length|**int**|Longitud máxima de caracteres de la columna basada en caracteres; en caso contrario, es NULL.|  
|numeric_precision|**tinyint**|Precisión de la columna, si está basada en números; en caso contrario, es NULL.|  
|numeric_precision_radix|**smallint**|Base de precisión de la columna, si está basada en números; en caso contrario, es NULL.|  
|numeric_scale|**int**|Escala de la columna, si está basada en números; en caso contrario, es NULL.|  
|datetime_precision|**smallint**|Precisión de la columna, si está basada en fecha y hora; en caso contrario, es NULL.|  
  
## <a name="remarks"></a>Comentarios  
 Utilice sys.sp_cdc_get_captured_columns para obtener información acerca de las columnas capturadas devueltas consultando las funciones de consulta de la instancia de captura [cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) o [cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md). Los nombres de columna, Id. y posición siguen siendo constantes para la duración de la instancia de captura. Solo el tipo de datos de columna cambia cuando el tipo de datos de la columna de origen subyacente en la tabla de la que se ha realizado un seguimiento cambia. Las columnas que se agregan o se quitan de una tabla de origen tienen ningún impacto en las columnas capturadas de instancias de captura existente.  
  
 Use [sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) para obtener información acerca de la definición de datos de las instrucciones de DDL (lenguaje) aplicadas a una tabla de origen. Cualquier cambio de DDL que ha modificado la estructura de una columna de origen de la que se ha realizado un seguimiento se devuelve en el conjunto de resultados.  
  
## <a name="permissions"></a>Permissions  
 Requiere pertenencia al rol fijo de base de datos db_owner. Para el resto de usuarios, requiere el permiso SELECT en todas las columnas capturadas en la tabla de origen y, si se ha definido un rol de acceso para la instancia de captura, la pertenencia a ese rol de base de datos. Cuando el autor de la llamada no tiene permiso para ver los datos del origen, la función devuelve el error 22981 (El objeto no existe o se ha denegado el acceso).  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve información acerca de las columnas capturadas en la instancia de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
