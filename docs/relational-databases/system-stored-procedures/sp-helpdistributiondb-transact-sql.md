---
title: sp_helpdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c97fec403da1913f7f39f1da706d107cd964aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902917"
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
`[ @database = ] 'database_name'` Es el nombre de la base de datos para el que se devuelven las propiedades. *database_name* es **sysname**, su valor predeterminado es **%** para todas las bases de datos asociados con el distribuidor y en el que el usuario tiene permisos.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de la base de datos de distribución.|  
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
|**log_file**|**nvarchar(255)**|Nombre del archivo de registro.|  
|**log_file_size**|**int**|Tamaño inicial del archivo de registro en megabytes.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistributiondb** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Los miembros de la **db_owner** rol fijo de base de datos o el **replmonitor** rol en una base de datos de distribución y los usuarios en la lista de acceso de publicación de una publicación con la base de datos de distribución pueden ejecutar **sp_helpdistributiondb** para devolver información relacionada con el archivo. Los miembros de la **pública** pueden ejecutar **sp_helpdistributiondb** para devolver información no relacionada con el archivo para las bases de datos de distribución a las que tengan acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
