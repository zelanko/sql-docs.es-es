---
title: sp_help_downloadlist (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b864f94e3c0925088e64e34a2c2e57695c5dc515
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdownloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enumera todas las filas de la **sysdownloadlist** tabla del sistema para el trabajo especificado o todas las filas si no se especifica ningún trabajo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 Número de identificación del trabajo para el que se va a devolver información. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name=** ] **'***job_name***'**  
 Nombre del trabajo. *job_name* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no pueden especificarse ambos.  
  
 [  **@operation=** ] **'***operación***'**  
 Operación válida del trabajo especificado. *operación* es **varchar(64)**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**DAR DE BAJA**|Operación del servidor que solicita al servidor de destino para dar de baja del servidor maestro **SQLServerAgent** servicio.|  
|**DELETE**|Operación de trabajo que quita un trabajo completo.|  
|**INSERT**|Operación de trabajo que inserta un trabajo completo o actualiza un trabajo existente. Esta operación incluye todos los pasos y programaciones del trabajo, si corresponde.|  
|**VOLVER A DAR DE ALTA**|Operación del servidor que hace que el servidor de destino vuelva a enviar la información de alta, incluidos el intervalo de sondeo y la zona horaria del dominio multiservidor. El servidor de destino también vuelve a descargar el **MSXOperator** detalles.|  
|**SET-POLL**|Operación del servidor que establece el intervalo, en segundos, con el que los servidores de destino sondean el dominio multiservidor. Si se especifica, *valor* se interpreta como el valor de intervalo necesario y puede ser un valor de **10** a **28.800**.|  
|**INICIO**|Operación de trabajo que solicita el inicio de la ejecución del trabajo.|  
|**DETENER**|Operación de trabajo que solicita la detención de la ejecución del trabajo.|  
|**HORA DE SINCRONIZACIÓN**|Operación de servidor que hace que el servidor de destino sincronice su reloj del sistema con el dominio multiservidor. Como ésta es una operación muy costosa, ejecútela de forma limitada, con poca frecuencia.|  
|**UPDATE**|Operación de trabajo que actualiza solo el **sysjobs** información para un trabajo, no los pasos de trabajo o las programaciones. Se llama automáticamente a **sp_update_job**.|  
  
 [  **@object_type=** ] **'***object_type***'**  
 Tipo de objeto del trabajo especificado. *object_type* es **varchar(64)**, su valor predeterminado es null. *object_type* puede ser JOB o SERVER. Para obtener más información acerca de cómo válido *object_type*valores, consulte [sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md).  
  
 [  **@object_name=** ] **'***object_name***'**  
 Nombre del objeto. *object_name* es **sysname**, su valor predeterminado es null. Si *object_type* es JOB, *object_name*es el nombre del trabajo. Si *object_type*es servidor, *object_name*es el nombre del servidor.  
  
 [  **@target_server=** ] **'***target_server***'**  
 El nombre del servidor de destino. *target_server* es **nvarchar (128)**, su valor predeterminado es null.  
  
 [  **@has_error=** ] *has_error*  
 Indica si el trabajo tiene que reconocer errores. *has_error* es **tinyint**, su valor predeterminado es null, lo que indica que no se debe reconocer ningún error. **1** indica que se deben reconocer todos los errores.  
  
 [  **@status=** ] *estado*  
 Estado del trabajo. *estado* es **tinyint**, su valor predeterminado es null.  
  
 [  **@date_posted=** ] *date_posted*  
 Fecha y hora desde las que se van a presentar las entradas en el conjunto de resultados. *date_posted* es **datetime**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**valor de instance_id**|**int**|Número de identificación entero único de la instrucción.|  
|**source_server**|**nvarchar(30)**|Nombre de equipo del servidor del que proviene la instrucción. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0, esto siempre es el nombre del equipo del servidor principal (MSX).|  
|**operation_code**|**nvarchar(4000)**|Código de operación de la instrucción.|  
|**object_name**|**sysname**|Objeto afectado por la instrucción.|  
|**object_id**|**uniqueidentifier**|Número de identificación del objeto afectado por la instrucción (**job_id** para un objeto de trabajo, o 0 x 00 para un objeto de servidor) o un valor de datos específico de la **operation_code**.|  
|**target_server**|**nvarchar(30)**|Servidor de destino que va a descargar esta instrucción.|  
|**error_message**|**nvarchar(1024)**|Mensaje de error (si existe) del servidor de destino si se encontró algún problema al procesar la instrucción.<br /><br /> Nota: Cualquier mensaje de error bloquea todas las posteriores descargas del servidor de destino.|  
|**date_posted**|**datetime**|Fecha en que la instrucción se envió a la tabla.|  
|**date_downloaded**|**datetime**|Fecha en que el servidor de destino descargó la instrucción.|  
|**status**|**tinyint**|Estado del trabajo:<br /><br /> **0** = no se ha descargado<br /><br /> **1** = descargado correctamente.|  
  
## <a name="permissions"></a>Permissions  
 Los permisos de ejecución para este procedimiento corresponden de forma predeterminada a los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestran las filas de `sysdownloadlist` para el trabajo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
