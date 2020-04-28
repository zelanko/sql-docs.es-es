---
title: managed_backup. sp_get_backup_diagnostics (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 5e967ae5b46ec703da4e8b1fff64f298fdf8a081
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942045"
---
# <a name="managed_backupsp_get_backup_diagnostics-transact-sql"></a>managed_backup. sp_get_backup_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve los eventos extendidos registrados por Smart Admin.  
  
 Utilice este procedimiento almacenado para supervisar los eventos extendidos registrados por Smart admin. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] los eventos se registran en este sistema y se pueden revisar y supervisar mediante este procedimiento almacenado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.sp_get_backup_diagnostics [@xevent_channel = ] 'event type' [, [@begin_time = ] 'time1' ] [, [@end_time = ] 'time2'VARCHAR(255) = 'Xevent',@begin_time DATETIME = NULL,@end_time DATETIME = NULL  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @xevent_channel  
 Tipo de evento extendido. El valor predeterminado se establece para devolver todos los eventos registrados durante los 30 minutos anteriores. Los eventos registrados dependen del tipo de Eventos extendidos habilitados. Puede utilizar este parámetro para filtrar el procedimiento almacenado para mostrar solo los eventos de un tipo determinado. Puede especificar el nombre de evento completo o especificar una subcadena como: **' admin**', ' **Analytics '**, **' Operational '** y **' Debug '**. @event_channel Es **VARCHAR (255)**.  
  
 Para obtener una lista de tipos de eventos habilitados actualmente, use la función **managed_backup. fn_get_current_xevent_settings** .  
  
 [@begin_time  
 El inicio del período de tiempo cuyos eventos se deben mostrar. El @begin_time parámetro es de tipo DateTime y su valor predeterminado es NULL. Si esto no se especifica, se muestran los eventos de los últimos 30 minutos.  
  
 @end_time  
 El fin del período de tiempo cuyos eventos se deben mostrar. El @end_time parámetro es de fecha y hora con un valor predeterminado de NULL.  Si esto no se especifica, se muestran los eventos hasta la hora actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
 Este procedimiento almacenado devuelve una tabla con la siguiente información:  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Descripción|  
|event_type|NVARCHAR (512)|Tipo de evento extendido.|  
|evento|NVARCHAR (512)|Resumen de los registros de eventos.|  
|Timestamp|timestamp|Marca de tiempo de evento que muestra si el evento se ha producido.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere permisos **Execute** en el procedimiento almacenado. También requiere permisos **View Server State** , ya que internamente llama a otros objetos del sistema que requieren este permiso.  
  
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
  
  
