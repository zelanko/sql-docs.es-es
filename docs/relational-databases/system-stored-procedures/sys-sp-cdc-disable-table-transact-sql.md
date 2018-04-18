---
title: Sys.sp_cdc_disable_table (Transact-SQL) | Documentos de Microsoft
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
- sys.sp_cdc_disable_table
- sp_cdc_disable_table
- sys.sp_cdc_disable_table_TSQL
- sp_cdc_disable_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_disable_table
- sys.sp_cdc_disable_table
- change data capture [SQL Server], disabling tables
ms.assetid: da2156c0-504e-4d76-b9a0-4448becf9bda
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4364f6cba3a5eb28cfac72e4f5f727ddf1bd1ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysspcdcdisabletable-transact-sql"></a>sys.sp_cdc_disable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deshabilita la captura de datos modificados para la tabla de origen especificada y la instancia de captura en la base de datos actual. La captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_disable_table   
  [ @source_schema = ] 'source_schema' ,   
  [ @source_name = ] 'source_name'  
  [ , [ @capture_instance = ] 'capture_instance' | 'all' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_schema=** ] **'***source_schema***'**  
 Es el nombre del esquema en el que está incluido la tabla de origen. *source_schema* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 *source_schema* debe existir en la base de datos actual.  
  
 [  **@source_name=** ] **'***source_name***'**  
 Es el nombre de la tabla de origen de la que se va a deshabilitar la captura de datos de cambio. *source_name* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 *source_name* debe existir en la base de datos actual.  
  
 [  **@capture_instance=** ] **'***capture_instance***'** | **'**todos los**'**  
 Es el nombre de la instancia de captura que se deshabilitará para la tabla de origen especificada. *capture_instance* es **sysname** y no puede ser NULL.  
  
 Cuando se especifica 'all', todas las instancias de captura definidas para *source_name* están deshabilitados.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **Sys.sp_cdc_disable_table** quita la captura de datos modificados cambiar funciones del sistema y de la tabla asociadas a la instancia de captura y la tabla de origen especificado. Elimina cualquier fila asociada a la instancia de captura especificada desde la tablas de sistema de captura de datos de cambio y establece el **is_tracked_by_cdc** columna para la entrada de la tabla en la [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) vista de catálogo en 0.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_owner** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se deshabilita la captura de datos modificados para la tabla `HumanResources.Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_disable_table   
    @source_schema = N'HumanResources',   
    @source_name = N'Employee',  
    @capture_instance = N'HumanResources_Employee';  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)  
  
  
