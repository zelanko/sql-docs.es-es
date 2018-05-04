---
title: sp_helpdistributiondb (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9d52dfc8be41dc8a86fc87803a50939f03558691
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las propiedades de la base datos de distribución especificada. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] **'***database_name***'**  
 Es el nombre de la base de datos cuyas propiedades se devuelven. *database_name* es **sysname**, su valor predeterminado es **%** para todas las bases de datos asociados con el distribuidor y en el que el usuario tiene permisos.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la base de datos de distribución.|  
|**min_distretention**|**int**|Período mínimo de retención, en horas, antes de que se eliminen las transacciones.|  
|**max_distretention**|**int**|Período máximo de retención, en horas, antes de que se eliminen las transacciones.|  
|**retención de historial**|**int**|Número de horas que se conserva el historial.|  
|**history_cleanup_agent**|**sysname**|Nombre del Agente de limpieza del historial.|  
|**distribution_cleanup_agent**|**sysname**|Nombre del Agente de limpieza de distribución.|  
|**status**|**int**|Exclusivamente para uso interno.|  
|**data_folder**|**nvarchar(255)**|Nombre del directorio que se utiliza para almacenar los archivos de base de datos.|  
|**data_file**|**nvarchar(255)**|Nombre del archivo de la base de datos.|  
|**data_file_size**|**int**|Tamaño inicial del archivo de datos en megabytes.|  
|**log_folder**|**nvarchar(255)**|Nombre del directorio del archivo de registro de la base de datos.|  
|**ArchivoDeRegistro**|**nvarchar(255)**|Nombre del archivo de registro.|  
|**log_file_size**|**int**|Tamaño inicial del archivo de registro en megabytes.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistributiondb** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Los miembros de la **db_owner** rol fijo de base de datos o la **replmonitor** rol en una base de datos de distribución y los usuarios en la lista de acceso de la publicación de una publicación con la base de datos de distribución pueden ejecutar **sp_helpdistributiondb** para devolver información relacionada con el archivo. Los miembros de la **público** pueden ejecutar **sp_helpdistributiondb** para devolver información no relacionado con el archivo de bases de datos de distribución a los que tienen acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
