---
title: managed_backup.sp_get_backup_diagnostics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql-non-specified
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
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 088d3232ef47888c0615e7b8a7638eb26f2817a2
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="managedbackupspgetbackupdiagnostics-transact-sql"></a>managed_backup.sp_get_backup_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve los eventos extendidos registrados por Smart Admin.  
  
 Utilice este procedimiento almacenado para supervisar eventos extendidos registrados por Smart Admin. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] eventos se registran en este sistema y se puede revisar y supervisan a través de este procedimiento almacenado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @xevent_channel  
 Tipo de evento extendido. El valor predeterminado se establece para devolver todos los eventos registrados durante los 30 minutos anteriores. Los eventos registrados dependen del tipo de Eventos extendidos habilitados. Puede utilizar este parámetro para filtrar el procedimiento almacenado para mostrar solo los eventos de un tipo determinado. Puede especificar el nombre completo del evento o especifique una subcadena como: **'Admin'**, **'Analytic'**, **'Operational'**, y **'Debug'** . El @event_channel es **VARCHAR (255)**.  
  
 Para obtener una lista de tipos habilitados actualmente de evento, utilice la **managed_backup.fn_get_current_xevent_settings** (función).  
  
 [@begin_time  
 El inicio del período de tiempo cuyos eventos se deben mostrar. El @begin_time parámetro es DateTime y su valor predeterminado es null. Si esto no se especifica, se muestran los eventos de los últimos 30 minutos.  
  
 @end_time  
 El fin del período de tiempo cuyos eventos se deben mostrar. El @end_time parámetro es DateTime y su valor predeterminado es NULL.  Si esto no se especifica, se muestran los eventos hasta la hora actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
 Este procedimiento almacenado devuelve una tabla con la siguiente información:  
  
||||  
|-|-|-|  
|Nombre de la columna|Tipo de datos|Description|  
|event_type|NVARCHAR(512)|Tipo de evento extendido.|  
|Evento|NVARCHAR(512)|Resumen de los registros de eventos.|  
|Timestamp|TIMESTAMP|Marca de tiempo de evento que muestra si el evento se ha producido.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere **EXECUTE** permisos en el procedimiento almacenado. También requiere **VIEW SERVER STATE** permisos ya que internamente llama a otros objetos del sistema que requieren este permiso.  
  
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
  
  
