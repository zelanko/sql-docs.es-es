---
title: Sys.sp_cdc_help_change_data_capture (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_change_data_capture_TSQL
- sys.sp_cdc_help_change_data_capture_TSQL
- sp_cdc_help_change_data_capture
- sys.sp_cdc_help_change_data_capture
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sys.sp_cdc_help_change_data_capture
- sp_cdc_help_change_data_capture
ms.assetid: 91fd41f5-1b4d-44fe-a3b5-b73eff65a534
author: rothja
ms.author: jroth
ms.openlocfilehash: fdf0086fe3a87823a419f3535888ea3211ee9ef1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905170"
---
# <a name="sysspcdchelpchangedatacapture-transact-sql"></a>sys.sp_cdc_help_change_data_capture (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la configuración de captura de datos del cambio para cada tabla habilitada para la captura de datos del cambio en la base de datos actual. Se pueden devolver hasta dos filas para cada tabla de origen, una fila para cada instancia de captura. La captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_help_change_data_capture   
  [ [ @source_schema = ] 'source_schema' ]  
  [, [ @source_name = ] 'source_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_schema =] '*source_schema*'  
 Es el nombre del esquema al que pertenece la tabla de origen. *source_schema* es **sysname**, su valor predeterminado es null. Cuando *source_schema* se especifica, *source_name* también debe especificarse.  
  
 Si no es NULL, *source_schema* debe existir en la base de datos actual.  
  
 Si *source_schema* es distinto de NULL, *source_name* también debe ser distinto de NULL.  
  
 [ @source_name =] '*source_name*'  
 Es el nombre de la tabla de origen. *source_name* es **sysname**, su valor predeterminado es null. Cuando *source_name* se especifica, *source_schema* también debe especificarse.  
  
 Si no es NULL, *source_name* debe existir en la base de datos actual.  
  
 Si *source_name* es distinto de NULL, *source_schema* también debe ser distinto de NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Nombre del esquema de la tabla de origen.|  
|source_table|**sysname**|Nombre de la tabla de origen.|  
|capture_instance|**sysname**|Nombre de la instancia de captura.|  
|object_id|**int**|Id. de la tabla de cambios asociada a la tabla de origen.|  
|source_object_id|**int**|Id. de la tabla de origen.|  
|start_lsn|**binary(10)**|Número de flujo de registro (LSN) que representa el extremo bajo para consultar la tabla de cambio.<br /><br /> NULL = no se ha establecido el extremo bajo.|  
|end_lsn|**binary(10)**|LSN que representa el extremo alto para consultar la tabla de cambio. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta columna siempre es NULL.|  
|supports_net_changes|**bit**|Se habilita la compatibilidad del cambio de red.|  
|has_drop_pending|**bit**|No se usa en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|role_name|**sysname**|Nombre del rol de base de datos utilizado para controlar el acceso a los datos de cambio.<br /><br /> NULL = no se utiliza un rol.|  
|index_name|**sysname**|Nombre del índice utilizado para identificar de forma exclusiva las filas en la tabla de origen.|  
|filegroup_name|**sysname**|Nombre del grupo de archivos en que reside la tabla de cambio.<br /><br /> NULL = la tabla de cambio está en el grupo de archivos predeterminado de la base de datos.|  
|create_date|**datetime**|Fecha en que se habilitó la instancia de captura.|  
|index_column_list|**nvarchar(max)**|Lista de las columnas de índice utilizada para identificar de forma exclusiva las filas en la tabla de origen.|  
|captured_column_list|**nvarchar(max)**|Lista de las columnas de origen capturadas.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando ambos *source_schema* y *source_name* NULL de forma predeterminada, o se establecen explícitamente en NULL, este procedimiento almacenado devuelve información para todos los de la base de datos de instancias de captura que ha seleccionado el llamador acceso a. Cuando *source_schema* y *source_name* son distintos de NULL, se devuelve información solo en la tabla habilitada con nombre específica.  
  
## <a name="permissions"></a>Permisos  
 Cuando *source_schema* y *source_name* son NULL, la autorización del llamador determina qué tablas habilitadas se incluyen en el conjunto de resultados. Los autores de las llamadas deben tener el permiso SELECT en todas las columnas capturadas de la instancia de captura y también ser miembros de cualquier rol de acceso definido para la información de la tabla que se va a incluir. Los miembros del rol de la base de datos db_owner pueden ver información sobre todas las instancias de captura definidas. Cuando se solicita información para una tabla habilitada concreta, para la tabla con nombre se aplican los mismos criterios de pertenencia y SELECT.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-change-data-capture-configuration-information-for-a-specified-table"></a>A. Devolver la información de configuración de captura de datos de cambio para una tabla especificada  
 El siguiente ejemplo devuelve la configuración de captura de datos del cambio para la tabla `HumanResources.Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee';  
GO  
```  
  
### <a name="b-returning-change-data-capture-configuration-information-for-all-tables"></a>b. Devolver la información de configuración de captura de datos de cambio para todas las tablas  
 En el ejemplo siguiente se devuelve información de configuración para todas las tablas habilitadas en la base de datos que contiene los datos de cambios a los que el autor de las llamadas tiene autorizado el acceso.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_help_change_data_capture;  
GO  
```  
  
  
