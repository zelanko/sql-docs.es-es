---
title: managed_backup.sp_get_backup_diagnostics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_backup_diagnostics_TSQL
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics_TSQL
- smart_admin.sp_get_backup_diagnostics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_backup_diagnostics
- smart_admin.sp_get_backup_diagnostics
ms.assetid: 2266a233-6354-464b-91ec-824ca4eb9ceb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 84fe7cea5418a022282958a7c16d263e5c7e9604
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399839"
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve los eventos extendidos registrados por Smart Admin.  
  
 Utilice este procedimiento almacenado para supervisar los eventos extendidos registrados por Smart Admin. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] eventos se registran en este sistema y se pueden revisar y supervisar mediante este procedimiento almacenado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @xevent_channel  
 Tipo de evento extendido. El valor predeterminado se establece para devolver todos los eventos registrados durante los 30 minutos anteriores. Los eventos registrados dependen del tipo de Eventos extendidos habilitados. Puede utilizar este parámetro para filtrar el procedimiento almacenado para mostrar solo los eventos de un tipo determinado. Puede especificar el nombre completo del evento o bien especificar una subcadena como: **'Admin'**, **'Analytic'**, **'Operational'**, y **'Debug'**. El @event_channel es **VARCHAR (255)**.  
  
 Para obtener una lista de eventos habilitados actualmente tipos uso el **managed_backup.fn_get_current_xevent_settings** función.  
  
 [@begin_time  
 El inicio del período de tiempo cuyos eventos se deben mostrar. El @begin_time parámetro es DateTime y su valor predeterminado es null. Si esto no se especifica, se muestran los eventos de los últimos 30 minutos.  
  
 @end_time  
 El fin del período de tiempo cuyos eventos se deben mostrar. El @end_time parámetro es DateTime con un valor predeterminado es NULL.  Si esto no se especifica, se muestran los eventos hasta la hora actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
 Este procedimiento almacenado devuelve una tabla con la siguiente información:  
  
||||  
|-|-|-|  
|Nombre de la columna|Tipo de datos|Descripción|  
|event_type|NVARCHAR (512)|Tipo de evento extendido.|  
|Evento|NVARCHAR (512)|Resumen de los registros de eventos.|  
|Timestamp|timestamp|Marca de tiempo de evento que muestra si el evento se ha producido.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere **EXECUTE** permisos en el procedimiento almacenado. También requiere **VIEW SERVER STATE** permisos desde que llama internamente a otros objetos del sistema que requieren este permiso.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los eventos registrados durante los últimos 30 minutos  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics  
  
```  
  
 El ejemplo siguiente devuelve todos los eventos registrados durante un intervalo de tiempo especificado.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Admin',  
  @begin_time = '2013-06-01', @end_time = '2013-06-10'  
  
```  
  
 El ejemplo siguiente devuelve todos los eventos analíticos durante los últimos 30 minutos  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_get_backup_diagnostics @xevent_channel = 'Analytic'  
  
```  
  
  
