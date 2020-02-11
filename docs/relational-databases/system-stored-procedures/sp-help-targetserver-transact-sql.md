---
title: sp_help_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1eb9a4d1a19f54f9e57e988b350594ce6031b243
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085084"
---
# <a name="sp_help_targetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra todos los servidores de destino en una lista.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server_name'`Nombre del servidor del que se va a devolver información. *SERVER_NAME* es de tipo **nvarchar (30)** y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si no se especifica *SERVER_NAME* , **sp_help_targetserver** devuelve este conjunto de resultados.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Número de identificación del servidor.|  
|**server_name**|**nvarchar(30**|Nombre de servidor.|  
|**Cód**|**nvarchar(200)**|Ubicación del servidor especificado.|  
|**time_zone_adjustment**|**int**|Ajuste de zona horaria, en horas, según la hora del meridiano de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Fecha de alta del servidor especificado.|  
|**last_poll_date**|**datetime**|Fecha del último sondeo del servidor en busca de trabajos.|  
|**estatus**|**int**|Estado del servidor especificado.|  
|**unread_instructions**|**int**|Indica si el servidor tiene instrucciones no leídas. Si se han descargado todas las filas, esta columna es **0**.|  
|**local_time**|**datetime**|Fecha y hora locales del servidor de destino, que están basadas en la hora local del servidor de destino según el último sondeo del servidor maestro.|  
|**enlisted_by_nt_user**|**nvarchar(100**|Usuario de Microsoft Windows dado de alta en el servidor de destino.|  
|**poll_interval**|**int**|Frecuencia, en segundos, con la que el servidor de destino sondea el servicio SQLServerAgent principal para descargar trabajos y cargar el estado de los trabajos.|  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. Presentar información de todos los servidores de destino registrados  
 En este ejemplo se presenta información de todos los servidores de destino registrados.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. Presentar información de un servidor de destino específico  
 En este ejemplo se presenta información del servidor de destino `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [DBO. sysdownloadlist &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
